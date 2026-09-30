---
title: "LaTeX"
date: 2023-03-18T18:05:34+01:00
---

> "Se stai pensando ma senza scrivere, stai solo pensando di star pensando."
> Leslie Lamport

## Introduzione

[Questo modello per tesi in LaTeX](https://github.com/cartabinaria/latex-thesis)
combina il frontespizio e l'esempio, entrambi in LaTeX, proposti dal
dipartimento.

## Uso

Clicca su "Use this template" per creare una nuova tesi basata su questo
modello. Poi, clicca su Actions per accedere alle funzioni di CI/CD. Se vuoi
che la tua tesi venga autonomamente ripubblicata in PDF ogni volta che `main`
viene aggiornata, sotto "Settings"/"Pages"/"Build and deployment" imposta
"Source" a "GitHub Actions".

## CI/CD

Ogni volta che aggiungi un _commit_ su una PR aperta verso `main`, viene
controllata la corretta compilazione di `tesi/tesi.tex`. Ogni volta che `main`
subisce modifiche, il risultato della compilazione viene pubblicato su
`https://<nome-utente>.github.io/<nome-repository>/tesi.pdf`.
