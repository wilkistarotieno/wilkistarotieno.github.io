---
title: "Über Krytowährungen"
date: 2015-01-24 17:05:00
categories: Kryptographie osbn
---

*Eine kleine Erklärung der Funktionsweise moderner Kryptowährungen. Ich habe versucht, den Beitrag möglichst einfach zu halten, allerdings sollte man grob verstanden haben, wie Hashes und digitale Signaturen funktionieren.*

Eine dezentrale und sichere Währung zu entwickeln galt lange als unmöglich, bis Satoshi Nakamoto 2008 das Konzept des *Bitcoins* vorstelle.

Seit es *[asymmetrische Kryptographie](https://de.wikipedia.org/wiki/Asymmetrisches_Kryptosystem)* gibt, ist es möglich, sichere Signaturen zu erstellen. Mit diesen kann sichergestellt werden, dass Geld nur mit der digitalen Unterschrift des Besitzers überwiesen werden kann, und nicht im Namen eines anderen.


Wenn das Geld einmal verteilt ist, müssten alle ihre Überweisungen nur noch signieren und diese an alle anderen Knoten im Netzwerk verteilen. Dabei schickt einfach jeder die Überweisung an alle Knoten, die er kennt, und diese verschicken sie dann ebenfalls an alle ihnen bekannten Knoten weiter. *([Flooding](https://de.wikipedia.org/wiki/Flooding-Algorithmus))*

Überweisungen sind jetzt verifizierbar und allen Knoten bekannt, es muss aber auch (im Nachhinein) sichergestellt werden können, dass es Konsens darüber gibt, ob eine Überweisung akzeptiert wird oder nicht, ohne, dass eine valide Überweisung abgelehnt wird oder eine Überweisung des selben Geldes mehrfach akzeptiert wird *(double spending)*.

Ein Angreifer könnte beispielsweise etwas kaufen, woraufhin der Verkäufer, sobald ihn die Überweisung erreicht, die Ware verschickt. Der Angreifer würde dann das eben überwiesene Geld nochmals überweisen, allerdings auf sein eigenes Konto.

Welche der beiden Überweisungen ist jetzt gültig? Die Frage lässt sich bei einer zentralisierten Währung leicht beantworten: Es ist diejenige, die zuerst bei der Bank eingeht.

Für eine dezentralisierte Währung muss es nun eine andere Möglichkeit geben, sich auf eine Überweisung zu einigen, da es viele Knoten gibt, nicht nur eine Bank, und nicht jeden würde die gleiche Überweisung zuerst erreichen. Der Angreifer würde einfach dem Verkäufer die für ihn passende Überweisung schicken, und allen anderen die andere.

Auf welche der beiden man sich einigt, ist letztlich egal, solange alle diese Überweisung akzeptieren und die andere ablehnen. *([Problem der byzantinischen Generäle](https://de.wikipedia.org/wiki/Byzantinischer_Fehler))*

Der Verkäufer wird die Ware erst dann verschicken, wenn sicher ist, dass die an ihn gesendete Überweisung auch die allgemein annerkannte ist.

Es müsste nun also eine Art Abstimmung darüber geben, welche der Transaktionen die richtige ist. Und bei einer Abstimmung muss eine Mehrheit ausgemacht werden können, ohne etwas wie eine Einwohnermeldebehörde.

Es ist also nicht klar, wie viele Accounts es gibt, wie viele davon sich an einer Abstimmung beteiligen oder wie viele zu dem selben Besitzer gehören *([Sybil-Attacke](https://en.wikipedia.org/wiki/Sybil_attack))*.

### Proof-of-Work

Dieses Problem kann durch ein *[Proof-of-Work](https://de.wikipedia.org/wiki/Proof-of-Work)* Verfahren gelöst werden, wie es beim [Bitcoin](https://de.wikipedia.org/wiki/Bitcoin) verwendet wird.

Alle Knoten versuchen eine zufällige Zahl *(nonce)* zu finden, deren Hash kleiner als eine vorgegebene *difficulty*[^1] ist. *([Mining](https://de.wikipedia.org/wiki/Bitcoin#Mining))*

Die Wahrscheinlichkeit eine solche nonce zu finden steigt mit der Rechenleistung des eigenen Computers. Der Finder der nonce veröffentlicht nun einen Datenblock, welcher die nonce und eine Liste von Überweisungen, die ihn erreicht haben, enthält.

Jeder Knoten des Netzwerkes kann dann ohne Aufwand feststellen, ob die gefundene nonce gültig ist[^2] und keine Transaktionen des gleichen Geldes zweimal in diesem Block vorkommen.

Das Finden einer solchen nonce berechtigt einen also dazu, zu entscheiden, welche Transaktionen gültig sind.  Und da immer zufällige Knoten eine nonce finden wird es auch unmöglich, eine legitime Transaktion abzulehmen. 

Es kann jedoch später eine ebenfalls passende nonce für den Block gefunden / veröffentlicht werden. In diesem Block können dann natürlich auch andere Überweisungen vorkommen.

Wie stellt man fest, welcher Block jetzt akzeptiert werden soll? Was hat das Suchen nach einer nonce gebracht?

Der Vorteil ist, dass die einzelnen Blöcke miteinander verknüpft sind.[^3] Hat der Angreifer für den zu ersetzenden Block eine passende nonce gefunden, muss er diese auch für alle folgenden Blöcke finden, da diese alle bereits mit dem ersetzten Block verknüpft waren.

Je weiter eine Transaktion in der Blockkette *([blockchain](https://de.wikipedia.org/wiki/Bitcoin#Block-Chain))* zurückliegt, desto mehr Blöcke müsste der Angreifer ersetzten und desto unwahrscheinlicher ist es, dass ihm das gelingt.

Und während der Angreifer damit beschäftigt ist, nonces für die alten Blöcke zu finden, werden immer neue Blöcke generiert, die der Angreifer auch ersetzen müsste.

Es ist daher nur möglich, Blöcke nachträglich auszutauschen, wenn man mehr Rechenleistung zur Verfügung hat als der Rest des Netzwerks zusammen. *(51% Attacke)*

Neben der Möglichkeit als Miner eine Gebühr für die Aufnahme von Überweisungen in den Block zu verlangen, kann durch Geldschöpfung in den Blöcken ein Anreiz geschaffen werden, sich an der Suche nach diesen zu beteiligen.

Je höher dieser Anreiz ist, desto mehr Rechner werden sich beteiligen und desto aufwändiger wird ein Angriff.

Gleichzeitig ist das auch das Problem Proof-of-Work basierter Kryptowährungen. Es wird nur so viel Rechenleistung (-> Stromkosten ...) investiert, wie die Gewinne durch das Mining auch decken. Und nur so stark ist die Mehrheit des Netzwerkes.

### Proof-of-Stake

Es gibt daher den Ansatz des *[Proof-of-Stake](https://en.wikipedia.org/wiki/Proof-of-stake)*, welcher etwa beim [Peercoin](https://en.wikipedia.org/wiki/Peercoin/) verwendet wird.

Die Wahrscheinlichkeit, einen Block zu finden, ist dabei nicht mehr abhängig von der investierten Rechenleistung, sondern davon, wie viel Geld auf einem Account liegt[^4].

Dies verhindert eine *Sybil-Attacke*, da Accounts auf denen kein Geld liegt, auch keine Blöcke generieren können (difficulty = Hash * 0).

Möchte man einen erfolgreichen Angriff starten, muss man die Hälfte des verfügbaren Geldes besitzen, was je nach Marktkapitalisierung teuer ist, und durch den entstehenden Kursanstieg immer teurer wird.

Allerdings ist es bei Proof-of-Stake Algorithmen möglich, in mehreren Blockchains nach Blöcken zu suchen, ohne, dass sich die Wahrscheinlichkeit einen Block zu finden entsprechend aufteilt *(Nothing at Stake)*, weshalb dieses Vorgehen sanktioniert werden muss. [siehe [blog.ethereum.org](https://blog.ethereum.org/2014/11/25/proof-stake-learned-love-weak-subjectivity/) oder [wiki.nxtcrypto.org](https://wiki.nxtcrypto.org/wiki/Whitepaper:Nxt#Nothing_at_Stake)]

Scott Driscoll  hat zu dem Thema auf seinem Blog eine gute [Erklärung](http://www.imponderablethings.com/2013/07/how-bitcoin-works-under-hood.html) veröffentlicht.

*Lasst gerne Kommentare und Anmerkungen da, falls etwas unverständlich war oder ihr es anders erklären würdet.*

[^1]: Die difficulty ist dabei so gewählt, dass es ungefähr zehn Minuten dauert eine nonce zu finden, daher wird auch ungefähr alle zehn Minuten ein neuer Block mit Transaktionen veröffentlich.

[^2]: Hashing-Verfahren sind Einwegfunktionen, beispielsweise wäre es in einem Telefonbuch einfach zu überprüfen, ob ein Name (in dem Fall die nonce) zu einer Telefonnummer gehört, allerdings schwer, einen passenden Namen zu einer vorgegebenen Telefonnummer zu finden

[^3]: Der Hash wird dazu nicht aus der nonce alleine gebildet, sondern die nonce wird zusammen mit dem Hash des letzten Blocks gehasht.

[^4]: Der Hash wird nicht mehr aus einer nonce gebildet, sondern aus dem öffentlichen Schlüssel des Accounts und die difficulty mit dem Besitz und der seit dem letzten Block verstrichenen Zeit multipliziert. Accounts mit viel Geld werden dabei im Schnitt früher einen gültigen Block generieren.
