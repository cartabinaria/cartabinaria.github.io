---
title: "Configurazioni"
date: 2023-04-29T15:13:05+02:00
---

Talvolta, gli stessi valori di configurazione possono essere usati più volte in
progetti diversi di CartaBinaria. Per esempio, le informazioni sui corsi di laurea
e sugli insegnamenti sono usate sia da `cartabinaria/dynamik` (per la
visualizzazione delle risorse in rete) che da `cartabinaria/informabot`.

In un'ottica di riuso del codice, queste configurazioni sono centralizzate
su [cartabinaria/config](https://github.com/cartabinaria/config).

### Modifiche alla repository

Se avvengono delle modifiche nella repository puoi aprire una PR per aggiornare 
cartabinaria/config per i servizi che ti interessano urgentemente. Per tutti gli 
altri abbiamo configurato Dependabot in modo che apra una PR in automatico nel 
giro di ventiquattr'ore.

## CI/CD (`.github/workflows/`)

In `.github/workflows`, sono presenti le procedure di CI/CD riutilizzate da
ogni insegnamento.

## Nomenclatura (`*.synta`)

Le grammatiche che descrivono le regole di nomenclatura da adottare per i nomi
delle risorse sono memorizzate nei file `.synta`. Synta è un formato interno
ad-hoc. La correttezza di questi file è verificata automaticamente a ogni
modifica di `main`.

## Insegnamenti (`teachings.json`)

In `teachings.json` sono raccolti tutti gli insegnamenti (obbligatori e
opzionali) per cui CartaBinaria offre strumenti.

## Corsi di laurea (`degrees.json`)

I vari corsi di laurea del DISI sono elencati e internamente suddivisi in anni.
Ciascuno contiene anche gli identificativi dei rispettivi insegnamenti in
`teachings.json`.

## Uso da Go con `config-parser-go`

La libreria [config-parser-go](https://github.com/cartabinaria/config-parser-go)
espone il package `cparser`. Da un modulo Go, con Go 1.22.4 o successivo:

```sh
go get github.com/cartabinaria/config-parser-go@v0.3.4
```

Questa versione richiede `cartabinaria/config` v1.1.4. I JSON sono incorporati
in quel modulo con `embed.FS`: i parser non leggono una directory locale e non
scaricano configurazioni a runtime. I dati dipendono dalla versione di `config`
selezionata dal modulo del programma; per aggiornarli occorre aggiornare la
dipendenza e ricompilare.

```go
package main

import (
	"fmt"
	"log"

	cparser "github.com/cartabinaria/config-parser-go"
)

func main() {
	degrees, err := cparser.ParseDegrees()
	if err != nil {
		log.Fatal(err)
	}
	for _, degree := range degrees {
		fmt.Println(degree.Id, degree.Name)
	}
}
```

Tutti i parser restituiscono anche un `error` per gli errori di lettura o
decodifica JSON: controllalo prima di usare i dati.

| Funzione | Risultati |
| --- | --- |
| `ParseTeachings()` | `[]cparser.Teaching, error` |
| `ParseDegrees()` | `[]cparser.Degree, error` |
| `ParseTimetables()` | `map[string]cparser.Timetable, error` |
| `ParseMaintainers()` | `[]cparser.Maintainer, error` |
| `ParseRepresentatives()` | `map[string]cparser.Representative, error` |

`ParseMaintainers()` seleziona **solo il progetto `informabot`**, non tutti i
mantenitori di `maintainers.json`; restituisce un errore se il progetto manca.

Per filtrare `d.Teachings` di un `cparser.Degree`:

- `GetAllMandatoryTeachingsFromDegree(d)` e
  `GetAllElectivesTeachingsFromDegree(d)` selezionano obbligatori e opzionali;
- `GetYearMandatoryTeachingsFromDegree(d, year)` e
  `GetYearElectivesTeachingsFromDegree(d, year)` filtrano anche per anno
  (`year` è un `int64`).

Questi filtri restituiscono `[]cparser.DegreeTeaching`, senza `error`.
`GetYear(d, year)` cerca invece in `d.Years` e restituisce `(cparser.Year, error)`:
se l'anno manca, restituisce `cparser.Year{}` e un errore.
`MustGetYear(d, year)` restituisce `cparser.Year`, ma genera un **panic** se
l'anno manca; usalo solo quando la presenza dell'anno è garantita.

Riferimenti: [pkg.go.dev](https://pkg.go.dev/github.com/cartabinaria/config-parser-go)
e [sorgente con tipi e firme complete](https://github.com/cartabinaria/config-parser-go/blob/v0.3.4/main.go).

## Mantenitori (`maintainers.json`)

In `maintainers.json`, sono elencati i contatti Telegram di alcuni dei maintainers 
per i nostri progetti.
