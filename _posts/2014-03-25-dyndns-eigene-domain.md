---
title:  "DynDNS mit eigener Domain"
date:   2014-03-25 17:21:00
categories: Web osbn
---
Es gibt mehrere Möglichkeiten, seiner Domain eine dynamische IP Adresse zuzuweisen.

**Eigener Nameserver**

Dafür trägt man bei seinem Domain Registrar als Nameserver einen [selbst gehosteten Server](http://www.thesysadmin.net/eigenen-dyndns-server-betreiben/) ein. Problem hierbei ist, dass um den Nameserver (ns1.example.com) zu erreichen, auch die Domain (example.com) erreichbar sein muss. Diese ist aber auf dem Nameserver definiert. Umgangen wird dies durch [Glue Records](https://de.wikipedia.org/wiki/NS_Resource_Record#Zonendelegation). Ein Glue Record weist einem Nameserver in der zu example.com gehörigen Zonendatei eine IP-Adresse zu.


**Externer Nameserver**

Es gibt ebenfalls einige DNS-Hoster, die einem Nameserver und DynDNS-Client zur Verfügung stellen. Dies dürfte für die meisten die einfachste Option sein. [Namecheap](https://www.namecheap.com/domains/freedns.aspx) bietet einen solchen Service kostenlos an. (Natürlich kann man seine Domain auch direkt dort kaufen.)

**CNAME auf Subdomain**

Man kann natürlich auch einfach einen Alias seiner Subdomain auf eine DynDNS-Subdomain legen. Mir sind allerdings keine wirklich guten, kostenlosen DynDNS-Anbieter bekannt.

    www.example.com. IN CNAME subdomain.no-ip.com.
