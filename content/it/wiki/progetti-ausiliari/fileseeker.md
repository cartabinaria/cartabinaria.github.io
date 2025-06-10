---
title: "Fileseeker"
date: 2025-06-10T16:11:38+02:00
---

- [Repository GitHub](https://github.com/cartabinaria/fileseeker)

## Descrizione
`fileseeker` è un adattore WebDAV per le risorse presenti su [Risorse](https://risorse.vercel.app/).
Espone quindi tutti i contenuti di Risorse attraverso un sevrer WebDAV.
Per informazioni maggiori sul protocollo WebDAV, consultare [webdav.org](http://www.webdav.org/).

Il programma è essenzialmente strutturato in due componenti principali:
- aggiornamento periodico delle risorse del filesystem
- esposizione del filesystem tramite server WebDAV

Per ragioni di sicurezza il file system è accessbile solo in lettura.
Qualsiasi richiesta con metodi diversi da `GET`, `HEAD`, `OPTION`, `PROPFIND`
verrà rifiutata.

## Utilizzo
Ottenere una qualsiasi risorsa tramite fileseeker è molto semplice.
Qui in seguito un esempio di richiesta per scaricare la soluzione
per l'esame scritto di logica per l'informatica del 2024-02-16.

```bash
curl -O https://dav.students.cs.unibo.it/logica-per-informatica/prove/scritto-2024-02-16-1-soluzione.pdf
```

Il motivo per cui fileseeker è stato scritto (e la scelta del protocollo WebDAV), risiede nella possibilità
di accedere al filesystem remoto direttamente dal proprio dispositivo, senza dover accedere a siti
esterni. Questo è fattibile tramite file manager o `rclone`.

Qui in seguito viene riportata una guida di Nextcloud per accedere a file system remoti che fanno
uso del protocollo WebDAV: [Guida](https://docs.nextcloud.com/server/latest/user_manual/it/files/access_webdav.html)
