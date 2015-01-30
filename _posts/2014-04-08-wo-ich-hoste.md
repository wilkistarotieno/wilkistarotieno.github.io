---
title:  "Wie dieser Blog gehostet wird"
date:   2014-04-08 02:01:00
categories: Web
---
**[Openshift](https://www.openshift.com/)**

Die Wordpressinstallation liegt bei openshift, einer Platform von Redhat, wo Anwendungen wie Wordpress in der Cloud gehostet werden können.

Warum?

Ein Blog ist bis auf die Kommentare statisch, es wird also keine große Rechenleistung benötigt, allenfalls Bandbreite bei hohen Benutzerzahlen. Die Leistung von openshift reicht hier aus, immerhin bekommt man drei kleine Instanzen kostenlos.

Es gibt hier natürlich auch einige andere Anbieter wie [Heroku](https://www.heroku.com/), ich fand Redhat klang am sympathischsten ;-)


Oder man setzt ganz klassisch auf ein VPS. Wer hierbei nicht auf eine vorkonfigurierte Installation verzichten will, sollte sich bei [Digital Ocean](https://www.digitalocean.com/features/one-click-apps/) (bzw. [bithost](https://bithost.io/)) umsehen.

**[Cloudflare](https://www.cloudflare.com/)**

Die Seiten des Blogs werden von cloudflare für je zwei Stunden gecacht, komprimiert und über die Welt verteilt. Damit der Benutzer bei Versenden von Kommentaren Feedback bekommt benutze ich das Wordpress-Plugin [ajaxify-comments](https://wordpress.org/plugins/wp-ajaxify-comments/).

Warum?

*   Bei cloudflare gecachte HTML-Dateien brauchen bei mir nur 30ms zur Auslieferung, ein beeindruckender Wert. Alle anderen Dateien bleiben nach erstmaligem Herunterladen für ein Jahr  im Cache des Browsers, wobei ich bezweifle, dass irgendwer seinen Browsercache so lange nicht löscht.
*   Ich kann einen CNAME-Eintrag auf die Hauptdomain legen. (Nimm das, DNS-Protokoll!)
*   SSL-Verschlüsselung, egal auf welcher Domain der Blog liegt. Laut [Ankündigung](https://twitter.com/CloudFlare/status/450390445365800961) soll 2014 auch für die Nutzer der kostenlosen Version SSL nutzbar sein.
*   Die Bandbreitenauslastung der Wordpress-Installation sinkt deutlich.

Wer lieber selbst hostet kann auch [Varnish](https://www.varnish-cache.org/) benutzen.

**[Mailgun](http://www.mailgun.com/)**

Es gibt genug Auswahl an [Email-as-a-Service](http://www.sitepoint.com/email-as-a-service-part-2-sendgrid-mailgun-and-postmark/) Anbietern, oder man betreibt seinen eigenen Mailserver.

Warum Mailgun?

Keine Ahnung, aber es hat eine coole API.

**[Freenom](http://freenom.com/en/index.html)**

Bei Freenom bekommt man einige exotische Domains wie .cf, .ml oder .tk gratis.

Warum?

Man spart sich das Geld für [WHOIS Privacy](https://en.wikipedia.org/wiki/Domain_privacy).

**[Github](https://pages.github.com/)**

Alternativ kann man statische Seiten auch bei Github Pages hosten, für Kommentare wird dann eine externe Lösung wie [disqus](https://disqus.com/) benötigt. Die Geschwindigkeit ist hierbei auch excellent, da Github die Dateien über das CDN von [fastly](https://github.com/blog/1715-faster-more-awesome-github-pages) verteilt.
