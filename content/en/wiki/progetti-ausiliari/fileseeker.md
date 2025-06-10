---
title: "Fileseeker"
date: 2025-06-10T16:11:38+02:00
---

- [GitHub Repository](https://github.com/cartabinaria/fileseeker)

## Description
`fileseeker` is a WebDAV adapter for the resources available on CartaBinaria.
It exposes all of CartaBinaria's content through a WebDAV server.
For more information on the WebDAV protocol, see [webdav.org](http://www.webdav.org/).

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
```h
