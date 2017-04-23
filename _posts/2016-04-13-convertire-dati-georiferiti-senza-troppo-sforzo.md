---
layout: post
title:  "Convertire dati georiferiti senza troppo sforzo"
date:   2016-04-13 10:10:00
categories: blog
tags: blog
image: /assets/article_images/2016-04-13-convertire-dati-georiferiti-senza-troppo-sforzo/photo.jpg
---

Stasera un semplice tutorial per imparare a convertire file contenenti dati georiferiti in vari formati.
Il tutorial viene fuori da una bella scoperta (che io faccio solo adesso ma mi si dice sia conosciutissimo tra gli esperti): si chiama [GDAL](http://www.gdal.org/) ossia "Geospatial Data Abstraction Library" una libreria software che vi consente la manipolazione di dati geografici astraendovi dal loro formato, compreso la possibilità di passare dal un formato all'altro con un tool ad hoc che si chiama [ogr2ogr](http://www.gdal.org/ogr2ogr.html). La scoperta la faccio grazie ad "amici di dati" che si chiamano Matteo ed Andrea...gente che ne sa, molto più di me.

Scopro quindi questa libreria e trovo subito un modo per sperimentare come usarla su un caso reale. Si chiama [OpendataGentediPrato](http://iltempe.github.io/opendatagentediprato/) portale di dati aperti dal basso per la mia città.

Trovo sul portale Openda Data Network un [dataset](http://www.opendatanetwork.it/dataset/wi-fi-free) del Comune di Prato che indica dove si trovano le WIFI del comune georiferite come dati su mappa. Formato dei dati KML.
Mi chiedo come posso dare modo di vederle in modo semplice? Mi rispondo: "posso farlo convertendo il file KML in un formato GeoJSON con [questo mio tutorial](http://iltempe.github.io/blog/2016/04/11/estrarre-dati-da-openstreetmap-e-visualizzarli.html)" convertendo cioè prima i dati da KML in un formato che si chiama GeoJSON ed archiviandoli poi su Github dove c'è la possibilità di vederli in modo facile.

Ecco come potete procedere quindi.

* Installate la libreria sul vostro server con questo comando

```bash
$ sudo apt-get install gdal-bin
```

Per verificare di aver installato la libreria GDAL digitate

```bash
$ gdalinfo --version
```
Dovreste visualizzare la versione della libreria. A questo punto dovete rilfettere sulla conversione che dovete fare con ogr2ogr. Tutti i formati possibili che potete gestire con questo software sono elencati [qui](http://www.gdal.org/ogr_formats.html).

Un esempio semplicissimo di comando per una conversione è questo

```bash
$ ogr2ogr -f GeoJSON wifi-free.geojson wifi_copertura.kml
```
dove GeoJSON è il formato di destinazione del file che volete ottenere
wifi-free.geojson è il nome del file di destinazione che volete ottenere
wifi_copertura.kml è il file sorgente che volete convertire

Fatto! Cambiando i parametri potete divertirvi a convertire i dati in altri formati.

Se poi volete farvi uno script automatico per scaricare un file da remoto, convertirlo e farne l'aggiornamento su GITHUB
io uso in sequenza questi comandi

```bash
rm wifi-free.geojson
curl -L "http://odn.comune.prato.it/geonetwork/srv/en/resources.get?uuid=f7077224-bf61-4b1e-904b-f3668ef80859&fname=wifi_copertura.kml&access=private" > wifi_copertura.kml
ogr2ogr -f GeoJSON wifi-free.geojson /root/opendataprato/wifi_copertura.kml
 ./update.sh wifi-free.geojson
 ```
Dove il primo comando rimuove il geojson presente nella cartella (se esiste) il secondo comando effettua il download del file KML dal sito remoto, il terzo effettua la conversione del file scaricato in formato geoJSON ed il quarto comando consente l'upload del file convertito su GITHUB usando questo script [update] (https://github.com/iltempe/opendataprato/blob/master/tools/update%20sample.sh).

Lo script completo [eccolo qua](https://github.com/iltempe/opendataprato/blob/master/tools/wifi_semple.sh).

E qui sotto il file convertito, le parti evidenziate sono le aree coperte dal WIFI nel Comune di Prato.

<script src="https://embed.github.com/view/geojson/iltempe/opendataprato/master/wifi-free.geojson">&nbsp;</script>
