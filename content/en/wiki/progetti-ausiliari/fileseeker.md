---
title: "Fileseeker"
date: 2025-06-10T16:11:38+02:00
---

- [GitHub Repository](https://github.com/cartabinaria/fileseeker)

## Description
`fileseeker` is a WebDAV adapter for the resources available on [Risorse](https://risorse.vercel.app/).
It exposes all of Risorse's content via a WebDAV server.
For more informations on the WebDAV protocol, see [webdav.org](http://www.webdav.org/).

The program is essentially structured into two main components:
- periodic updating of the filesystem's resources
- exposing the filesystem via a WebDAV server

For security reasons, the filesystem is read-only.
Any request using methods other than `GET`, `HEAD`, `OPTION`, `PROPFIND`
will be rejected.

## Usage
Obtaining any resource via fileseeker is very simple.
Below is an example request to download the solution
for the Logic for Computer Science written exam from 2024-02-16.

```bash
curl -O https://dav.students.cs.unibo.it/logica-per-informatica/prove/scritto-2024-02-16-1-soluzione.pdf
```

The reason `fileseeker` was written (and the choice of WebDAV protocol) consists in the possibility
of accessing the remote filesystem directly from your own device, without having to access external websites.
This can be done via file manager or `rclone`.

Below is a Nextcloud guide for accessing remote file systems that make
use of the WebDAV protocol: [Guide](https://docs.nextcloud.com/server/latest/user_manual/it/files/access_webdav.html)
