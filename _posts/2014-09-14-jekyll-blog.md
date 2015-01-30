---
title:  "Bloggen mit Jekyll"
date:   2014-09-14 19:26:00
categories: Web osbn
---

[Jekyll](http://jekyllrb.com/) ist ein Generator für statische Blogs. Man schreibt Beiträge mit einem Markdown-Editor seiner Wahl und Jekyll baut dann, nach Vorlage des HTML-Templates, eine fertige Seite daraus.

Dies ist natürlich eine sehr minimalistische Lösung, man hat kein Interface wie bei Wordpress, alles wird über einfache Textdateien geregelt und am Ende kann der Leser erstmal nicht mit der Seite interagieren, da dynamische Dinge wie Kommentare nicht möglich sind.

Dafür bekommt man eine sehr schnelle und einfache Seite, die nicht mit Konfigurationsmöglichkeiten und Plugins überladen ist. Trotzdem kann die Seite nach seinen Wünschen anpassen, schließlich hat man direkten Zugriff auf das HTML-Template.


Aus diesen Gründen habe ich meine Wordpress-Seite aufgegeben und bin zu Jekyll gewechselt.

[Github pages](https://pages.github.com/) und [Stackedit](https://stackedit.io/editor) machen das Bloggen mit Jekyll sehr komfortabel. Mit Stackedit kann man seine Beiträge auf einer [Ghost](https://ghost.org/)-ähnlichen Oberfläche schreiben und direkt auf Github hochladen, wo wiederum automatisch die fertige Seite ausgeliefert wird.

Kommentare sind nur über externe Lösungen möglich, ich habe mich aus Datenschutzgründen für [Isso](http://posativ.org/isso/) entschieden. Eine verlockend einfach einzurichtende Alternative ist hier [disqus](https://disqus.com/).

An Themes gibt es lange nicht so viel Auswahl wie bei Wordpress, ein paar sind auf [jekyllthemes.org](http://jekyllthemes.org/) zu finden.
Ich habe mir kurzerhand mein [eigenes Theme](https://github.com/niklasbuschmann/Contrast) geschrieben, was im Vergleich zur Entwicklung eines Wordpress-Themes deutlich angenehmer ist.
Es funktioniert out-of-the-box mit Github pages, nur die `_config.yml` muss angepasst werden.

Wer also ein minimalistisches Blogsystem sucht und gerne Texte in Markdown schreibt sollte sich Jekyll einmal anschauen. 
