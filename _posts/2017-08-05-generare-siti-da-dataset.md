---
layout: post
title:  "Generare automaticamente pagine web con gli Opendata"
date:   2017-08-05 10:34:25
categories: blog
tags: blog
image: /assets/article_images/2017-08-05-generare-siti-da-dataset/2.jpeg
---


Ho già un po' parlato della mia simpatia per l'ambiente [Jekyll](https://jekyllrb.com/) in [questo post](https://medium.com/@iltempe/incorporare-i-video-in-jekyll-senza-plugin-64a2d7ef4e54). Tra le caratteristiche di Jekyll c'è la possibilità di poter usare automaticamente pagine web da file contenenti dati. L'unico vincolo come spiegato nelle [istruzioni](https://jekyllrb.com/docs/datafiles/) è che i file siano in formato CSV, YAML o JSON.
Un sito sviluppato con Jekyll può infatti contenere una cartella denominata "_data" all'interno della quale il sito stesso attinge a dati contenuti in file presenti nella folder, in particolare all'interno di pagine web si può addirittura usare direttamente i dati dei file!
E' quindi possibile pensare di poter sviluppare servizi basati su dataset aperti importando tali dataset nella cartella _data del proprio sito e usare i dati direttamente nello sviluppo in modo tale che il sito web a cui lavorate sia direttamente popolato dai dati che state riusando. Sarà sufficiente importare i file di cui avete bisogno nella folder "_data" e usare i dati secondo le istruzioni di Jekyll. Ricordatevi ovviamente di rispettare i termini di riuso dei dati rispettando i crediti di chi li produce.

Fatta questa introduzione vi riporto un semplice caso d'uso che mi è venuto in mente e vi riporto come esempio. Ovviamente diamo per scontato che abbiate un minimo di dimestichezza nel costruire un sito con Jekyll. In caso contrario vi consiglio di leggervi [questa guida](https://webdesign.tutsplus.com/it/tutorials/setting-up-jekyll-for-github-pages-in-60-seconds--cms-27256) che vi permette di prendere dimestichezza con questo ambiente tramite Github e poi tornare al mio tutorial. Supponiamo di voler sviluppare un servizio web per la gestione della consegna e restituzione dei libri per le biblioteche di una città. Il comune di Prato rilascia in formato open [questo dataset](http://odn.comune.prato.it/dataset/biblioteche) contenente l'elenco delle Biblioteche del mio comune con le informazioni di base di ciascuna. Come si vede il dataset è rilasciato in formato CSV che è uno dei formati "digeribili" da Jekyll. Una volta scaricato il dataset è quindi possibile inserirlo nella cartella _data dalla quale Jekyll preleva i dati. Fate attenziona al nome che date al file perchè sarà il nome della struttura dati che Jekyll assegnerà ai vostri dati.

![](/assets/article_images/2017-08-05-generare-siti-da-dataset/1.png)

Per usare i dati nel proprio sito web sarà a questo punto sufficiente usare la struttura `site.data` ovvero la struttura dove Jekyll memorizza i dati contenuti nella folder _data una volta che effettuate la costruzione del sito web con il comando `bundle exec jekyll serve`.

Supponiamo adesso di dove stampare la lista delle biblioteche presenti nella città e il relativo indirizzo in una pagina web. Vi basterà usare il seguente codice, dove la struttura `site.data.puntidiinteressebiblioteche` punta direttamente ai vostri dati importati.

```
    <ul>
    {% for member in site.data.puntidiinteressebiblioteche %}
    <li>
    {{ member.nome }} : {{ member.indirizzo }}
    </li>
    {% endfor %}
    </ul>
```
Il codice viene renderizzato nella pagina web in questo modo.

<ul>
{% for member in site.data.puntidiinteressebiblioteche %}
  <li>
      {{ member.nome }} : {{ member.indirizzo }}
  </li>
{% endfor %}
</ul>

Se poi si volesse anche creare una mappa di tutte le biblioteche direttamente nella pagina web.




