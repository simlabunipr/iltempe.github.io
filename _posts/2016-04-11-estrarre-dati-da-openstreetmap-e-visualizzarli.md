---
layout: post
title:  "Estrarre dati da Openstreetmap e visualizzarli su Github"
date:   2016-04-11 10:10:25
categories: blog
tags: blog
image: /assets/article_images/2016-04-11-estrarre-dati-da-openstreetmap-e-visualizzarli/photo.jpg
---

Capita che con un paio di amici che praticano hacking civico, Andrea Borruso e Matteo Fortini, ci interroghiamo su come fare per estrarre dei dati dalla piattaforma [Openstreetmap](http://www.openstreetmap.org) e poterli archiviare per usarli per una possibile applicazione e per effettuarne una visualizzazione in modo rapido.

D'altra parte tutta questa sensibilità sui dati georeferenziati di Openstreetmap ha un suo senso se si divulgano anche metodi per riusare questi dati. Ricordo che Openstreetmap concede il riuso completo dei suoi dati anche per fini commerciali a patto che si rispettino le indicazioni nella pagina di [copyright](https://www.openstreetmap.org/copyright).

Sicuramente consultando le community troverete molti modi per estrarre i dati. Qui oggi ve ne illustro uno per elaborare una richiesta alla piattaforma Openstreetmap, salvare i risultati in un file e visualizzare in modo rapido i risultati archiviando questi dati su un vostro repository [Github](http://www.github.com). Tutto in modo "programmatico" così che possa essere automatizzato. Questo metodo può essere molto utile se si vuole repidamente visualizzare certi dati su mappa, ma soprattutto se volete realizzare una applicazione che periodicamente voglia aggiornare questi dati in un vostro repository, così da assicurare un "dato sempre fresco".

Occorrente
- Account Github (è gratuito);
- Un repository pubblico su Github;
- Un computer con possibilità di eseguire comandi BASH (io uso un server con una distribuzione linux Debian, ma può andare bene un qualunque commputer connesso ad internet, potete farlo anche tramite una schedina Raspberry);
- Un minimo di confidenza con i [tag Openstreetmap](http://wiki.openstreetmap.org/wiki/IT:Etichette);

E' tutto, possiamo iniziare.

Installate sul vostro computer [NodeJS](https://nodejs.org/it/). Si tratta di un framework a eventi in grado di eseguire codice Javascript, per farlo implementa il V8 JavaScript Engine (il motore di Google Chrome) e vanta una elevata performance nel compilare codice Javascript. NPM è un Package Manager per node (Node Package Manager) ovvero di un software che consente di installare applicazioni per NodeJS. Le istruzioni per installare NodeJS e NPM le trovate al [link](https://nodejs.org/it/) in italiano. NPM dovrebbe autoinstallarsi sul vostro PC in modo automatico.

Installate l'applicazione [Query-Overpass](https://github.com/perliedman/query-overpass) che vi consente di gestire query su Openstreetmap (l'autore è lo stesso della piattaforma [UMAP](https://umap.openstreetmap.fr/it/)). Overpass Turbo è un software che permette di gestire interrogazioni dei dati di Openstreetmap. E' possibile ad esempio chiedere qualcosa tipo "dimmi tutti i negozi presenti a Prato". Per installare
Query-Overpass questo vi basta digitare il comando

```bash
$ npm install -g query-overpass
```

L'utilità di Query-Overpass è che potete chiamarla direttamente a riga di comando per cui a questo punto potete interrogare Openstreetmap con una qualunque richiesta che usi le query sui TAG Openstreetmap.

Per creare una query vi consiglio di recarvi sul sito [Overpass Turbo](https://overpass-turbo.eu/) ed usare il Wizard specie se la vostra richiesta è semplice. Supponiamo di voler cercare i negozi di Prato: nel wizard digitate "shop in Prato" dove shop è il [tag ufficiale](http://wiki.openstreetmap.org/wiki/Key:shop) Openstreetmap per ricercare negozi. Potete studiare i vari TAG Openstreetmap e cercare quello relativo al dato che più vi interessa estrarre.

Esportate la query che avete creato facendo click su Esporta->Query->Compatta e copiate la stringa che rappresenta la query. Nel caso specifico avrete questa stringa

```bash
[out:json][timeout:25];area(3600280245)->.searchArea;(node["shop"](area.searchArea);way["shop"](area.searchArea);relation["shop"](area.searchArea););out body;>;out skel qt;
```
A questo punto componiamo lo script che cerca i negozi su openstreetmap, salva i dati georiferiti in un file e successivamente facciamone un upload in un repository su Github.

Create un file denominato negozi.json in un vostro repository Github.

Componete sul vostro computer uno script upload.sh come questo (per fare l'upload del file). Per fare questo ho usato [questo tutorial](https://medium.com/mai-piu-senza/pubblicare-e-aggiornare-file-su-github-tramite-curl-5253cb139b86#.gx7rfu9p6) di Andrea Borruso.

```bash
# update a file to github repo
curl -i -X PUT -H 'Authorization: token XXXXXXXXXXXXXXXXX' -d "{\"path\": \"$1\", \
\"message\": \"update\", \"content\": \"$(openssl base64 -A -in $1)\", \"branch\": \"master\",\
\"sha\": $(curl -X GET https://api.github.com/repos/iltempe/opendataprato/contents/$1 | jq .sha)}" \
https://api.github.com/repos/iltempe/opendataprato/contents/$1

```

Componete sul vostro computer uno script osm.sh come questo ed eseguitelo.

```bash
#negozi
echo '[out:json][timeout:25];area(3600280245)->.searchArea;(node["shop"](area.searchArea);way["shop"](area.searchArea);relation["shop"](area.searchArea););out body;>;out skel qt;' | query-overpass > negozi.geojson

./update.sh negozi.geojson

```

Fatto! Se aprite il file [negozi.geojson](https://github.com/iltempe/opendataprato/blob/master/negozi.geojson) su Github potrete visualizzarlo come dati su una mappa!



Se eseguite questo script periodicamente aggiornerete il file su Github con i dati aggiornati di Openstreetmap. Per farlo potete usare la [CronTab](https://it.wikipedia.org/wiki/Crontab) del vostro server ed impsotare ad esempio di aggiornare il file geoJson ogni mese con un comando come questo:

```bash
0 0 1 * * ./osm.sh
```
