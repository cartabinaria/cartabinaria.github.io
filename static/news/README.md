# Banner del sito (dynamik)

Il file `banner.json` alimenta il banner delle novità sulla homepage di
[dynamik](https://github.com/cartabinaria/dynamik): a ogni visita la
applicazione scarica questo file e mostra i contenuti, senza bisogno di
modificare il codice di dynamik.

## Schema

```json
{
	"version": 2,
	"title": "Titolo breve della novità",
	"body": "Testo completo mostrato nel banner.",
	"href": "https://... (opzionale, null se non c'è)"
}
```

- `version`: numero intero crescente — va incrementato per far riapparire
  il banner a chi lo aveva già chiuso.
- `title`: titolo breve, mostrato in evidenza.
- `body`: testo della novità.
- `href`: opzionale; se valorizzato appare il link "leggi di più".

Dynamik valida i campi e, se il file non è raggiungibile o è malformato,
mostra un banner di fallback con l'ultima novità nota.
