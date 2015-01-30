---
title: "Callback Hells"
date: 2015-01-26 16:13:00
categories: Web osbn
---

Möchte man in *node.js* programmieren, muss man sich von der synchronen Schreibweise von Programmen verabschieden und die asynchronen *Callback*-basierten APIs benutzen.

Ein Beispiel, zwei Werte werden aus einer Datei und einer Datenbank gelesen und dann über eine REST-API weitergegeben.

```javascript
// Die guten alten Zeiten

var wert1 = fs.read('file.txt');
var wert2 = db.fetch('something');

http.request('domain.tdl', [wert1, wert2]);

console.log('succeeded');
```


Das Problem bei asynchronen Aufrufen ist, dass man nicht von außen auf die Callback-Funktion zugreifen kann, entweder man verschachtelt die Callbacks oder man schreibt die Werte in einen höheren Scope.

```javascript
// Callback-Hell

fs.read('file.txt', function (wert1) {
    db.fetch('something', function (wert2) {
        http.request('domain.tdl', [wert1, wert2], function () {
            console.log('succeeded');
        });
    });
});
```

```javascript
// Auch nicht besser

var wert1, wert2;

function done (wert1, wert2) {
    http.request('domain.tdl', [wert1, wert2], function () {
        console.log('succeeded');
    });
}

fs.read('file.txt', function (wert1) {
    wert1 = wert1;
    if (wert2)
        done(wert1, wert2);
});

db.fetch('something', function (wert2) {
	wert2 = wert2;
	if (wert1)
		done(wert1, wert2);
});
```

Hilfreich sind libraries wie [async.js](https://github.com/caolan/async), allerdings müssen die asynchronen Funktionen (fs.read / db.fetch) manuell gewrappt werden.

```javascript
async.parallel([
    function(callback){
        fs.read('file.txt', function (wert1) {
            callback(wert1);
        });
    }, 
    function(callback){
        db.fetch('something', function (wert1) {
            callback(wert2);
        });
    }], function(results){
    // Endlich
    http.request('domain.tdl', results, function () {
        console.log('succeeded');
    });
});
```

Mit APIs, die die mit ES6 erschienenen [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) unterstützen kann das entfallen.

```javascript
var tasks = [fs.read('file.txt'), db.fetch('something')];

Promise.all(tasks).then(function(results) {
    http.request('domain.tdl', results, function () {
        console.log('succeeded');
    });
});
```

Zusammen mit den ebenfalls seit ES6 existierenden Generatoren ist es möglich, Code zu pausieren, während auf asynchrone Funktionen gewartet wird.

```javascript
runGenerator(function *main(){
    var tasks = [fs.read('file.txt'), db.fetch('something')];
    var results = yield Promise.all(tasks);
    
    yield http.request('domain.tdl', results);

    console.log('succeeded');
});
```

Womit wir fast wieder beim Anfang wären, da man damit Code schreiben kann, der fast wie synchroner aussieht.

```javascript
// Und der Kreis schließt sich

runGenerator(function *main(){
    var wert1 = yield fs.read('file.txt');
    var wert2 = yield db.fetch('something');
    
    yield http.request('domain.tdl', [wert1, wert2]);

    console.log('succeeded');
});
```

Von Kyle Simpson gibt es dazu einen [interessanten Artikel](http://davidwalsh.name/async-generators).

Fein raus sind funktionale Sprachen ohne Seiteneffekte wie Haskell, bei denen man seinen Code einfach wie eh und je schreibt und der Compiler dafür sorgt, dass sich nichts gegenseitig blockiert.
