## Elemento HTML
E' definito da un tag di apertura, del contenuto e un tag di chiusura e comprende tutto quello che è all'interno dei tag.

`<nomeTag>Il contenuto va qui...</nomeTag>`

L'elemento è annidato quando contiene più tag al suo interno.

L'elemento è vuoto se non ha un tag di chiusura. Questo perchè l'elemento non è in funzione al suo contenuto. Può essere un immagine, un link.....

### Markup and paragraph

```
<h1>Titolo</h1>

<h2>Sottotitolo</h2>

<h3>Titolo paragrafo</h3>

<strong>grassetto</strong>

<em>bold italic</em>

<p>paragrafo</p>

<div>sezione del paragrafo</div>

<br/> interruzione di riga; elemento vuoto senza tag di chiusura.
```

### Lists
```
<ol id="myListNumber">
  <li>pasta</li> "premere tasto tab per spostarsi e inserire <li> + elemento lista 
  <li>latte</li>
  <li>burro</li>
</ol>

Elenco casuale

<ul id="myList">
        <li>Elemento 1</li>
        <li>Elemento 2</li>
        <li>Elemento 3</li>
        <li>Elemento 4</li>
        <li>Elemento 5</li>
  
</ul>
```


## Images

```
 <figure>
      <img src="images/logo-dechain.JPG" alt="logo-dechain" />
      <figcaption>Logo dechainlabs</figcaption>
  </figure>

```