---
title:  "Man-in-the-Middle ohne zentrale Instanz vermeiden"
date:   2014-03-22 18:27:00
categories: Web osbn
---
Derzeit sieht es so aus, dass der öffentliche Schlüssel einer SSL-geschützten Website von einer Certificate Authrority durch eine digitale Signatur bestätigt sein muss, sonst akzeptieren die meisten Browser das SSL-Zertifikat nicht.

Dafür hat jeder Browser eine Liste solcher CAs vorgegeben. Wird nun einer dieser Firmen der Schlüssel geklaut, sind alle Verbindungen zu den entsprechenden Seiten durch eine Man-in-the-Middle Attacke angreifbar, und wenn kein Widerrufungsschlüssel bekannt ist, bleibt dies solange, bis die Browserhersteller das Zertifikat manuell entfernen (siehe *DigiNotar*).

Und man bedenke, wie viele CAs aus den USA kommen und damit amerikanischem Recht unterliegen, was es der NSA ermöglicht, die entsprechenden Schlüssel anzufordern.


Eine alternative Möglichkeit Man-in-the-Middles auszuschließen besteht darin, jedes von einer Website empfangene Zertifikat mit mehreren anderen Personen abzugleichen.

Dafür speichert man sich die SSL-Fingerprints dieser Leute, die einen solchen Service betreiben fest ein und lässt sich von ihnen das Zertifikat der aufgerufenen Seite nochmals schicken.

Solange diese nicht alle das selbe, gefälschte Zertifikat untergejubelt bekommen, kann man nachvollziehen, ob man gerade von einem Man-in-the-Middle betroffen ist, also mindestens zwei Zertifikate sich voneinander unterscheiden.

Erstmals wurde dieses Konzept bei [convergence.io](http://convergence.io) verwendet.Leider funktioniert das Addon bei mir nicht mehr.

[HTTPS Everywhere](https://www.eff.org/https-everywhere "HTTPS Everywhere") unterstützt dieses Konzept auch, dafür muss in den Einstellungen *ssl observatory* aktiviert werden.

Außerdem könnte man sich so ein teures Zertifikat sparen - eine entsprechende Verbreitung des Konzepts vorrausgesetzt - , was sicher zur Verbreitung von SSL beitragen würde. *StartCom* scheint derzeit die einzige Möglichkeit zu sein, an ein kostenloses SSL-Zertifkat zu kommen.

Letzten Endes wird dadurch zwar nicht sichergestellt, dass die Seite vertrauenswürdig ist, aber ob dafür CAs geeignet sind, wage ich zu bezweifeln. (Wofür gibt es denn ein Web-of-Trust?)
