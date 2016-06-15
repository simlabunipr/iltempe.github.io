---
layout: post
title:  "Capitalizzare il software opensource mappando i defibrillatori su Openstreetmap"
date:   2016-06-15 10:34:25
categories: blog
tags: featured
image: /assets/article_images/2016-06-15-capitalizzare-il-software-opensource-mappando-i-defribillatori-su-openstreetmap/0.jpg
---

Nelle aziende chi progetta per riusare di solito è premiato. Se inventi qualcosa riusando qualcos'altro di fatto stai innovando risparmiando e questo è segno evidente che sei uno bravo.
La PA italiana questo non lo ha ancora ben compreso. Progettare servizi per la PA è missione della PA stessa e deve essere fatto massimizzando il riuso. Solo cosi si capitalizzano gli sforzi di sviluppo. Come? Il software opensource è un modo. Ma non solo: se il software è open non è detto che tu possa riusare in toto l'applicazione o il servizio, ne hai la conoscenza e puoi progettarne uno per te, magari modificato. Invece progettare in modo generico un servizio è altra cosa. La domanda che mi faccio è: a che serve avere un servizio mobile che mi cerca i musei a Prato se posso farlo per l'Italia o il mondo intero nello stesso modo? Le PA hanno il dovere di porsi queste domande. I comuni stessi che sviluppano software dovrebbero farlo perchè farebbero risparmiare soldi a livello di "sistema italia". Ditelo in giro. Stesso dicasi per le migliaia di servizi (alcuni ottimi) per segnalare qualcosa a qualcuno.

Ecco quindi che oggi ho dato l'imbeccata al buon [Piersoft](https://twitter.com/Piersoft) per creare un BOT per trovare il defribillatore più vicino a te usando informazioni di [Openstreetmap](www.openstreemap.org) : incentivo a produrre dati aperti su una piattaforma disponibile a TUTTI (Openstreetmap appunto), servizio opensource e servizio USABILE a livello di Italia ma anche a livello di MONDO intero.

Come funziona? Ricordate quello che feci per i [musei](http://pratosmart.teo-soft.com/trovare-musei-vicini-a-te-con-telegram-e-openstreetmap/)? Il modo è analogo.

Il bot lo trovate [qui](https://telegram.me/defibrillatoribot), si usa semplicemente inviando la propria posizione tramite la “molletta” in basso a sinistra nella chat.

Nel momento in cui riceve la vostra posizione il robot interroga il database di Openstreetmap, andando a cercare i luoghi identificati con il TAG emergency=defibrillator e vi restituisce la loro posizione geografica.

Tutto tramite opendata di Openstreetmap per cui aggiungendo dati taggati come defibrillatori alla mappa di Openstreetmap permettete ai luoghi di essere visti.

![il bot per i defibrillatori](/assets/article_images/2016-06-15-capitalizzare-il-software-opensource-mappando-i-defribillatori-su-openstreetmap/1.png)

L’applicazione ricorda molto il principio dei social come Foursquare, ma la base dei dati in questo caso è completamente aperta e più viene aumentata dai mappatori Openstreetmap più il servizio diventa efficiente.

C’è un limite al raggio di defibrillatori che al momento vengono restituiti (nel raggio di 1km).

Non fate caso se vedete la mappa di Google dentro il robot (sono le mappe che nativamente usa Telegram sul vostro smartphone) i dati sono effettivamente prelevati da Openstreetmap.

Per chi vuol creare un servizio simile può partire da questi sorgenti su [Github](https://github.com/iltempe/TelegramMusei).

Per mappare un punto defibrillatore su Openstreetmap è possibile farlo registrandosi su Openstreetmap.

- Dispositivo IOS: usando la APP Go Map! e Mappando un punto con tag Emrgency di valore Defibrillator.
- Dispositivo Android: OSM Tracker e Vespucci, idem come sopra
- PC: andando sul sito [Openstreetmap](wwww.openstreetmap.org), imparando a mappare un [punto](http://wiki.openstreetmap.org/wiki/IT:Elementi) e taggarlo con il tag "emergency" con valore "defibrillator".

