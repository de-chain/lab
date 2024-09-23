20240915174116

Articolo
```
@article{etichetta,
  author  = {Nome Autore1 and Nome Autore2 and Nome Autore3},
  title   = {Titolo dell'Articolo},
  journal = {Nome della Rivista},
  year    = {Anno},
  volume  = {Volume},
  number  = {Numero},
  pages   = {PaginaIniziale--PaginaFinale},
  month   = {Mese},
  doi     = {DOI dell'Articolo},
  url     = {URL dell'Articolo}
}
```
Documento
```
@misc{etichetta,
  author       = {Nome Autore},
  title        = {Titolo del Documento},
  howpublished = {Descrizione di come è stato pubblicato (es. "Online", "Manoscritto", ecc.)},
  year         = {Anno},
  note         = {Eventuali note aggiuntive},
  url          = {URL del Documento},
  month        = {Mese},
  doi          = {DOI del Documento}
}
```

Sito web
```
@misc{latexwebsite,
  author       = {Leslie Lamport},
  title        = {LaTeX: A Document Preparation System},
  howpublished = {\url{https://www.latex-project.org}},
  year         = {2023},
  note         = {Accessed: 2024-09-12}
}
```

Documento non pubblicato
```
@misc{tesi2023,
  author       = {Mario Rossi},
  title        = {Studio sui Fenomeni Elettromagnetici},
  howpublished = {Manoscritto inedito},
  year         = {2023},
  note         = {Dipartimento di Fisica, Università di Roma}
}
```

Report on line
```
@misc{reportonline2024,
  author       = {Giulia Bianchi},
  title        = {Analisi del Clima Globale 2024},
  howpublished = {Online},
  year         = {2024},
  url          = {https://www.climareport2024.org},
  note         = {Accessed: 2024-09-12}
}
```
### Spiegazione dei campi:

* ...{nome riferimento bibliografico è l'etichetta che riporto nel comando cite
* **author**: Il nome dell'autore o degli autori del documento.
* **title**: Il titolo della risorsa.
* **howpublished**: Descrizione di come è stata pubblicata (es. "Online", "Manoscritto", "Presentato a una conferenza").
* **year**: L'anno di pubblicazione o di accesso al documento.
* **note**: Note aggiuntive (es. "Consultato il \[data]" o informazioni specifiche sulla pubblicazione).
* **url**: L'URL del documento se disponibile online.
* **month**: Il mese (opzionale).
* **doi**: DOI, se disponibile (opzionale).

### Uso in LaTeX:
Usa `\cite{etichetta}` per citare il riferimento  all'interno del documento.

Esempio:

```
Curabitur sagittis interdum tortor, at ultrices lacus auctor in. Nullam blandit, ex ac pretium auctor, purus elit pulvinar est, quis ultricies turpis tortor id sapien.\cite{latexwebsite} Praesent sit amet venenatis est.
```
E poi nella bibliografia apparirà la risorsa citata.
