# Introduzione a La Tex

20240915091708

[editor Latex on line](https://it.overleaf.com/)
Latex è un programma che prende il testo che scriviamo, lo compila e lo converte in Pdf.
I documenti di latex hanno estensione ``.TeX``.
In un documento di latex ci sono tre tipi di contenuti:

1. Testo
2. Comandi
    1. su una linea solo ``\nome comando[parametri opzionali]{parametro 1}{parametro 2}``
    2. a blocchi
```tex
\begin{equation}
1=1
\end{equation}
```
3. Commenti
   	scrivi un commento anteponendo il carattere ``%`` al testo.

## Il preambolo

La parte del documento sopra il testo "quella che si trova prima del comando
` \begin{document}` è chiamata **preambolo**. Il preambolo contiene tutti i comandi e le istruzioni per configurare il documento, come
- pacchetti,
- la definizione di stili,
- impostazioni di formattazione
- e altro ancora. 
 
### documentclass
`\documentclass[a4paper, 12pt]{article}` specifica la classe del documento (es. article, report, book)
### userpackage
`\usepackage[utf8]{inputenc}` pacchetto per il supporto dei caratteri UTF-8
`\usepackage{amsmath}` pacchetto per simboli matematici avanzati
`\usepackage{graphicx}` pacchetto per l'inserimento di immagini
`\usepackage[T2A]{fontenc}` % кодировка
`\usepackage[utf8]{inputenc}` % кодировка исходного текста
`\usepackage[english,russian]{babel}` % локализация и переносы
`\usepackage{cite}`  % Per citare
`\usepackage{url}` % Per gestire gli URL correttamente
`\usepackage[colorlinks=true, linkcolor=blue, urlcolor=blue, citecolor=red]{hyperref}` % formattazione dei link
### i titoli
`\title{Titolo del Documento}` definisce il titolo del documento
`\author{Nome dell'Autore}` definisce l'autore del documento
`\date{\today}` imposta la data (usa il comando \today per la data corrente)
`\maketitle` genera il titolo e va inserito subito dopo \begin{document}

## L'indice
Per creare un **indice** in LaTeX, puoi utilizzare il comando `\tableofcontents`. Questo comando genera automaticamente l'indice del documento includendo tutte le sezioni, sottosezioni e altri titoli che sono stati definiti con i comandi `\section`, `\subsection`, ecc.
```tex
\documentclass{article}
\begin{document}

\tableofcontents Questo comando genera l'indice
\newpage Questo comando crea una pagina dedicata all'indice
\section{Introduzione}
Questa è la sezione introduttiva.
\subsection{Motivazione}
Descrizione della motivazione.
\section{Metodi}
Spiegazione dei metodi utilizzati.
\end{document}
```
## Il testo
La parte del documento che contiene  testo ha un inizio e una fine.
```tex
\begin{document}
il mio primo documento
\end{document}
```
## Le sezioni
* **\section{titolo}**: Crea una **sezione principale** numerata automaticamente con 1,2,3
* **\subsection{titolo}**: Crea una **sottosezione** all'interno di una sezione numerata automaticamente con 1.1, 1.2, 1.3
* **\subsubsection{titolo}**: Crea una **sottosottosezione** all'interno di una sottosezione numerata automaticamente con 1.1.1, 1.1.2, 1.1.3. LA sottosottosezione non è riportata nell'indice tableofcontants
* **\paragraph{titolo}**: Crea un **paragrafo**, ovvero un livello gerarchico ancora inferiore non numerato di default
* **\subparagraph{titolo}**: Crea una **sotto-paragrafo** non numerato di default

Ridefinizione della numerazione delle sezioni per usare numeri romani 
```tex
\renewcommand{\thesection}{\Roman{section}}
\renewcommand{\thesubsection}{\Roman{section}.\Roman{subsection}}
```


## I link
Non sono nativamente supportati da tex. Richiede un pacchetto da scrivere nel preambolo.
`\usepackage{hyperref}`
```tex
\begin{document}
\href{www.google.it}{link a Google}
\end{document}
```

## Le immagini
`\usepackage{graphicx}`  % Pacchetto per gestire le immagini

`\begin{document}`
`\begin{figure}`  % Inizia l'ambiente "figure" dove gestire l'immagine.
`\begin{figure}[h]` `[h]` per indicare che l'immagine dovrebbe essere posizionata "qui" (qui, h = "here"), `[t]` per posizionare nslla parte superiore della pagina,`[b]` per posizionare  nella parte inferiore.


`\includegraphics{nomefile}`: Inserisce l'immagine chiamata `nomefile`.<br>Assicurati che l'immagine si trovi nella stessa directory del file `.tex`, oppure fornisci il percorso completo.
`\centering`  % Centra l'immagine
\includegraphics[width=0.5\textwidth]{Images/Dante.jpg}  % Inserisce l'immagine e ne imposta la larghezza
`\caption{Questa è una didascalia dell'immagine.}`  % Aggiunge una didascalia
`\label{fig:esempio}`  % Aggiunge un'etichetta per riferirsi all'immagine nel testo
`\end{figure}`

## Liste
Puntata
```tex
\begin{itemize}
    \item Primo elemento della lista
    \item Secondo elemento della lista
    \item Terzo elemento della lista
\end{itemize}
```
Numerata
```tex
\begin{enumerate}
    \item Primo elemento
    \begin{itemize}
        \item Sotto-elemento puntato
        \item Sotto-elemento puntato
    \end{itemize}
    \item Secondo elemento
    \begin{itemize}
        \item Sotto-elemento puntato
    \end{itemize}
\end{enumerate}
```
## Note a piè di pagina o footnote

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean aliquet magna et semper fringilla at a urna.`\footnote{Questa è la nota a piè di pagina.}` Nullam eros quam, ullamcorper sodales ante a, mollis porttitor elit. Donec aliquet metus sed blandit sodales.\footnote{Questa è un'altra footnote.} Maecenas lacinia urna eu mi mattis, sit amet sodales sem vulputa. 

* `\footnote{...}`: Inserisce una footnote nel punto in cui viene usato. Il testo scritto all'interno delle parentesi graffe viene visualizzato in fondo alla pagina.
* Il numero della footnote viene generato automaticamente e viene posizionato sopra al testo nel punto in cui viene inserita la footnote.
* Le footnote aggiornano il numero progressivo in base alla posizione e non a quando le inserisco.

## Bibliografia
E' composta da tre comandi:
 1. nel preambolo `\userpackage{biblatex}` Importa il pacchetto della bibliografia
 2. sempre nel preambolo inseriamo una risorsa` \addbibresource{bibliografia.bib}`
 3. alla fine del documento prima di end `\printbibliography `
[[20240915174116]]
   Bibliografia
  [Youtube video](https://www.youtube.com/watch?v=QY2zdhSY48M)