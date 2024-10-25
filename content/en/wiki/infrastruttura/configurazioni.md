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

## Maintainers (`maintainers.json`)

In `maintainers.json`, the Telegram contacts of some of the maintainers for our projects are listed.
