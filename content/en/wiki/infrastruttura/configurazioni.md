---
title: "Configurations"
date: 2023-04-29T15:13:05+02:00
---

Sometimes, the same configuration values can be used multiple times in different projects at CartaBinaria. For example, information about degree courses and teachings is used both by `cartabinaria/dynamik` (for displaying resources online) and by `cartabinaria/informabot`.

In an effort to reuse code, these configurations are centralized on [cartabinaria/config](https://github.com/cartabinaria/config).

### Changes to the Repository

If there are changes in the repository, you can open a PR to update cartabinaria/config for the services that are urgently of interest to you. For all others, we have set up Dependabot to automatically open a PR within twenty-four hours.

## CI/CD (`.github/workflows/`)

In `.github/workflows`, there are CI/CD procedures reused by every teaching.

## Naming Convention (`*.synta`)

The grammars describing the naming convention rules to be adopted for resource names are stored in `.synta` files. Synta is an ad-hoc internal format. The correctness of these files is automatically verified with each `main` modification.

## Teachings (`teachings.json`)

All teachings (mandatory and optional) for which CartaBinaria provides tools are collected in `teachings.json`.

## Degree Courses (`degrees.json`)

The various degree courses at DISI are listed and internally divided into years. Each one also contains the identifiers of their respective teachings in `teachings.json`.

## Using `config-parser-go` from Go

The [config-parser-go](https://github.com/cartabinaria/config-parser-go) library
exposes the `cparser` package. From a Go module, with Go 1.22.4 or later:

```sh
go get github.com/cartabinaria/config-parser-go@v0.3.4
```

This version requires `cartabinaria/config` v1.1.4. The JSON files are embedded
in that module using `embed.FS`: the parsers neither read a local directory nor
download configurations at runtime. The data depends on the `config` version
selected by the application's module; updating it requires updating the
dependency and rebuilding.

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

All parsers also return an `error` for file reading or JSON decoding failures:
check it before using the data.

| Function | Results |
| --- | --- |
| `ParseTeachings()` | `[]cparser.Teaching, error` |
| `ParseDegrees()` | `[]cparser.Degree, error` |
| `ParseTimetables()` | `map[string]cparser.Timetable, error` |
| `ParseMaintainers()` | `[]cparser.Maintainer, error` |
| `ParseRepresentatives()` | `map[string]cparser.Representative, error` |

`ParseMaintainers()` selects **only the `informabot` project**, not all
maintainers in `maintainers.json`; it returns an error if the project is absent.

To filter `d.Teachings` of a `cparser.Degree`:

- `GetAllMandatoryTeachingsFromDegree(d)` and
  `GetAllElectivesTeachingsFromDegree(d)` select mandatory and elective teachings;
- `GetYearMandatoryTeachingsFromDegree(d, year)` and
  `GetYearElectivesTeachingsFromDegree(d, year)` also filter by year
  (`year` is an `int64`).

These filters return `[]cparser.DegreeTeaching`, without an `error`.
`GetYear(d, year)` instead searches `d.Years` and returns `(cparser.Year, error)`:
if the year is absent, it returns `cparser.Year{}` and an error.
`MustGetYear(d, year)` returns `cparser.Year`, but **panics** if the year is
absent; use it only when the year is guaranteed to exist.

References: [pkg.go.dev](https://pkg.go.dev/github.com/cartabinaria/config-parser-go)
and the [source with complete types and signatures](https://github.com/cartabinaria/config-parser-go/blob/v0.3.4/main.go).

## Maintainers (`maintainers.json`)

In `maintainers.json`, the Telegram contacts of some of the maintainers for our projects are listed.
