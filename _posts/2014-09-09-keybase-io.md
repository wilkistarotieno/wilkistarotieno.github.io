---
title:  "Keybase.io"
date:   2014-09-09 22:37:00
categories: Kryptographie osbn
---
Wer seine Kommunikation verschlüsseln und authentisieren möchte, der kommt um [asymmetrische Verschlüsselung](http://de.wikipedia.org/wiki/Asymmetrisches_Kryptosystem) nicht herum. Diese funktioniert auch bestens, solange sichergestellt ist, dass der Public-Key des Empfängers auch wirklich zum Empfänger gehört und nicht zu einem Angreifer, der die Verbindung manipuliert haben könnte.

Bei Personen, die man kennt, ist es kein Problem festzustellen, ob der Schlüssel auch zum Empfänger gehört, man kann sie einfach nach Dingen fragen, die der Angreifer nicht wissen kann ([OTR](http://de.wikipedia.org/wiki/Off-the-Record_Messaging)) oder den Public-Key persönlich abgleichen ([PGP](http://de.wikipedia.org/wiki/Pretty_Good_Privacy)).

Schwieriger wird es bei Personen, die man nicht kennt, man ihnen also nur indirekt über kommerzielle [Zertifizierungsstellen](http://en.wikipedia.org/wiki/Certificate_authority) (z.B. Verisign) oder ein [Web-of-Trust](http://de.wikipedia.org/wiki/Web_of_Trust) vertrauen kann. Was man nicht unbedingt [tun sollte](http://www.heise.de/security/meldung/Neuer-SSL-Gau-Falsches-Google-Zertifikat-blieb-fuenf-Wochen-unentdeckt-1333070.html).

Hier setzt [keybase.io](https://keybase.io/) an. Statt sich auf eine zentrale Instanz zu verlassen, wird der Schlüssel mit mehreren (derzeit: Twitter, Github, Reddit, Hacker News, DNS) dieser abgeglichen, in der Annahme, dass nicht auf allen ein manipulierter Schlüssel vorliegt.


_Aber, was, wenn keybase.io selbst manipuliert?_

```bash
$ whois keybase.io

Domain : keybase.io
Status : Live
Expiry : 2019-09-06
    
NS 1   : ns-1016.awsdns-63.net
NS 2   : ns-1722.awsdns-23.co.uk
NS 3   : ns-1095.awsdns-08.org
NS 4   : ns-337.awsdns-42.com
    
Owner  : Krohn, Maxwell
Owner  : CrashMix.org
Owner  : 902 Broadway, 4th Floor
Owner  : New York
Owner  : NY
Owner  : United States
```

Keybase.io liegt auf Amazon-Servern in den USA. Und bekanntlich gibt es in den USA einen Geheimdienst, der [Seitenmanipulationen](http://www.theguardian.com/commentisfree/2014/may/20/why-did-lavabit-shut-down-snowden-email) natürlich strikt ablehnt ^^

Für diesen Fall kann man Personen [tracken](https://keybase.io/docs/tracking) und somit bestätigen, dass die verlinkten Accounts zu diesem Zeitpunkt auch wirklich zu der entsprechenden Person gehörten.

_Aber, ich kann dort meinen privaten Schlüssel hochladen!_

Kann man aber auch sein lassen. Oder selbst nachprüfen, dass die Passphrase / der entsperrte Schlüssel auch im Browser bleibt.

Siehe auch die Beiträge auf [thomas-leister.de](https://thomas-leister.de/internet/pgp-keys-hosten-mit-keybase-io/) und [mspr0.de](http://mspr0.de/?p=4078)

Wer interessiert ist: Ich habe 5 invites zu vergeben, lasst einen Kommentar da, die ersten 5 bekommen eine.
