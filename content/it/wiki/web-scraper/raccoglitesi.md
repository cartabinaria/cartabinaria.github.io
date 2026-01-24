---
title: "Raccoglitesi"
date: 2023-03-18T13:13:34+01:00
---

> "Dimenticare come zappare la terra e curare il terreno significa dimenticare
> se stessi."
> Mahatma Gandhi

## Introduzione

Raccoglitesi è una _utility_ command line per studenti Unibo: trova tutte le
tesi triennali e magistrali offerte da un certo dipartimento. Raccoglitesi si
aggiorna in automatico e quotidianamente.

Il progetto è ospitato su [GitHub](https://github.com/cartabinaria/raccoglitesi).
La versione più recente dell'elenco generato è sempre consultabile
[qui in PDF](https://cartabinaria.github.io/raccoglitesi/disi.pdf) o [qui come
pagina web](https://cartabinaria.github.io/raccoglitesi/disi).

## Come funziona

Raccoglitesi è un web scraper scritto in golang, basato sul
[progetto](https://github.com/giammirove/raccoglitesi_unibo) omonimo di
[@giammirove](https://github.com/giammirove). Trova informazioni su certe pagine
del sito, come:

- `https://www.unibo.it/it/ateneo/sedi-e-strutture/dipartimenti`, per scoprire i
  dipartimenti presenti;
- `https://{{dip}}.unibo.it/it/dipartimento/persone/docenti-e-ricercatori` per
  trovare i nomi delle persone in dipartimento;
- `https://www.unibo.it/sitoweb/gianluigi.zavattaro/didattica?tab=tesi` per
  trovare le tesi listate sul sito.

È da notare che tutte queste informazioni potrebbero cambiare nel tempo (come
URL delle risorse, tags HTML mediante il quale si trovano le informazioni
volute). È quindi importante continuare a monitorare se lo script funziona
ancora. Per questo motivo il programma è eseguito ogni giorno, a mezzanotte.

## Dipartimenti analizzati
- [DISI: Dipartimento di Informatica - Scienza e
  Ingegneria](https://cartabinaria.github.io/raccoglitesi/disi)
- [DEI: Ingegneria dell’Energia elettrica e dell’Informazione "Guglielmo
  Marconi"](https://cartabinaria.github.io/raccoglitesi/dei)
- [DIFA: Fisica e Astronomia "Augusto Righi"](https://cartabinaria.github.io/raccoglitesi/fisica-astronomia)
