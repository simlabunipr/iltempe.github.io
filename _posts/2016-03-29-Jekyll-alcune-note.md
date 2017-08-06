---
layout: post
title:  "Jekyll alcune note"
date:   2016-03-29 13:34:25
categories: blog
tags:
  - jekyll
  - github
  - opensource
---

Digitando su Google la parola Jekyll troverete molti link relativi alla storia di Dr.Jekyll e Mr Hyde. Jekyll di cui parlo qui è però lo strumento con cui ho creato questo blog. E' quindi un'altra cosa.

[Jekyll](http://jekyllrb.com/) è un generatore di siti statici, cioè un sito creato con Jekyll non ha bisogno di un database per funzionare, Jekyll si occupa di creare la struttura necessaria per il funzionamento del sito. Tutti gli articoli e le pagine sono archiviati come file, quando si vuole creare o aggiornare il sito si esegue un comando ed il sito sarà generato all'interno di una particolare directory. Tutto il contenuto di questa cartella dovrà poi essere caricato sul server che ospiterà il sito.

Jekyll è un applicazione creata con il linguaggio Ruby, necessita di avere Ruby installato e funzionante sulla propria macchina. Si sceglie dove installare il nuovo sito e all'interno di quella directory si esegue il comando "jekyll new nomesito". Per vedere il sito sempre da terminale scrivere "jekyll serve" e verrà lanciato un server web locale con indirizzo standard localhost:4000.

Ogni singola modifica ai contenuti verrà riportata sul sito. Per creare un articolo basta creare un nuovo file (scritto in formato [Markdown](https://it.wikipedia.org/wiki/Markdown)) all'interno della cartella "_post", le pagine invece possono essere inserite liberamente nella directory principale del sito.
E' anche possibile ospitare il proprio sito creato direttamente su [Github](https://github.com/) seguendo [questa guida](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/). Per fare un setting di una pagina in locale si può usare  [questa guida](https://help.github.com/articles/setting-up-your-pages-site-locally-with-jekyll/).

Se volete quindi creare un blog senza nessun database e senza nessun backend. Ecco, Jekyll fa esattamente questo, automatizzando però tutte le operazioni che sarebbe impossibile e improbabile mantenere a mano, lasciandovi tutto il tempo per concentrarvi sui contenuti.

Jekyll è un sistema di blogging fatto e pensato per sviluppatori, ma è anche piuttosto facile da usare. Consiglio vivamente di provare ad usarlo la prima volta in questo modo:
- Creare un nuovo repository Github
- Forkare all'interno di tale repository un sito/template già archiviato su Github
- Impostare il proprio repository come [Github Page](https://pages.github.com/) in modo che si azioni il motore per processare il sito e renderlo visibile all'indirizzo xxx.github.io
- Aggiungere i post nella folder "post" ed iniziare a bloggare

In rete troverete molti post sul fatto che Jekyll sia necessariamente meglio di Wordpress. Io dico che effettivamente lo trovo un ottimo strumento per realizzare un blog. Ma per realizzare un blog. Wordpress è da tempo diventato uno strumento che, oltre ad avere qualche limite in termini di preformance e sicurezza, è anche "sovraaccessoriato" di plugin; questo ne fa un CMS che non è solo blogging ma anche altro, molto altro, forse troppo altro. Se avete bisogno di un framework di lavoro che vi consenta di fare blog concentrandovi sui contenuti di quello che scrivete, Jekyll è sicuramente più adeguato agli scopi. Vi obbliga a lavorare come uno scrittore, senza farvi perdere tempo con layout di ogni post, i plugin, i menu e senza mischiare quindi la forma con i contenuti del vostro blog. Una volta messo in piedi "il motore" ed il suo layout i post saranno la vostra unica preoccupazione. Non solo: nel caso vogliate un giorno modificare la forma del vostro blog non sarete costretti a rivere i contenuti perchè Jekyll "disaccoppia" completamente la parte di layout rispetto ai post del vostro blog.