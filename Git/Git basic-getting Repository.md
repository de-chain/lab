
## Strumenti necessari
* Git
* Visual Studio Code
* una directory in locale dove creo o sposto i file della mia repo.

## Creare una Repository

1) mi sposto all'interno della directory che diventarà la mia Repository in questo caso Repo
```
~/Documenti/Git/Repo $
 ```

 2) Inizializzo la directory
 ```
 git init
 ```
 Compare la scritta main
 ```
 ~/Documenti/Git/Repo (main)
 ```

 main indica che la directory Repo è stata inizializzata e siamo sul ramo main.
Inizializzando, abbiamo creato una cartella    *.git* 

La Directory .git ha cinque sottocartelle:<br>
hooks/
info/
objects/
refs/
branches/
HEAD
config
description

[Le  cartelle di .git](https://www.manuelricci.com/guida/come-inizializzare-git-da-riga-di-comando)

```
git status
```
 mi permette di vedere lo stato della Repo e dei file al suo interno

3) lavoro creando i file sulla working directory con:  
* vscode
* editor vim da bash line
* touch o echo comandi da bash

4) inserire i file sulla staging area
```
git add
```
Variabili:
* . tutti i file
* .read.md read1.md file specifici
* *.md file con estensione md

5) Committare, dalla staging area alla Repo
```
git commit -m "first commit"
```
```
git commit -m "firstcommit" -m "creato file read.md"
```
la prima -m è il messaggio che vedrò su git status, il secondo - m è un commento nascosto


6) ** il comando ***git log*** 

```
git log --online
git log --online --reverse
```

git log mi darà come informazioni:
commit 7af9d9b89d196ca4be265dba20deeb648544c357
(HEAD -> main)
Author: SDechain <dechain.trade@gmail.com>
Date:   Sat Aug 24 08:32:00 2024 +0200

Attenzione: git log visualizza un elenco in modalità visualizzazione e non mostra la barra per inserire nuovi comandi.
Premere ***q*** per uscire.

### approfondimento SHA1
7af9d9b89d196ca4be265dba20deeb648544c357 

Qualsiasi cosa in Git è controllata.<br> Il meccanismo che Git usa per fare il commit è una hash SHA-1. Si tratta di una stringa di 40-caratteri, composta da caratteri esadecimali (0–9 ed a–f) e calcolata in base al contenuto dei file o della struttura della directory in Git.

L'hash contiene un checksum. Questo significa che è impossibile cambiare il contenuto di qualsiasi file o directory senza che Git lo sappia.

Ogni commit ha il suo hash che lo identifica.
```
$ git log --oneline --reverse
```
f73e7a0 first commit
7af9d9b (HEAD -> main) second Commit

### approfondimento posizione commit

(HEAD -> main)<br>
HEAD è il puntatore che indica la posizione del commit. Posso entrare nella crtella heads per vederlo
```
cat .git/HEAD
```

### Modificare un Commit solo da locale

```
git commit --amende
```
 apre editmsg dove posso modoficare il testo del commit, commento, eliminare file committati.

```
git reset --soft id commit "35a00b1
```
 torna alla staging area pre commit

```
git reset --mixed id commit "35a00b1" torna alla working directory

***git reset --hard id commit "35a00b1"
```
 torna alla commit precedente ATTENZIONE PERCE CANCELLA I FILE

Comandi utili per puntare al commit che mi interessa: o scrivo id o digito
```
git reset --soft HEAD^ 
```
 ogni accento circonflesso mi indica di quante commit torno indietro.
Consiglio utile: prima digito git log --oneline cosi vedo i commit e a quale mi interessa puntare.

## Caricare Repository su github

1) Creo la mia repo su Github e ne copio Url

2) 
```
git remote add origin https://github.com/..................
```
 origin è il nome che do al mio server

3) 
```
git push -u origin main
```

## Approfondimento: git remote

```
git remote -v
```
 ottengo il nome dei server registrati e url
 ```
cat .git/config
```
 apro file di configurazione server

```
git remote show [nome server]
```
 mi da il dettaglio server.
 Git remote rename origin
 ```
git remote rename [ nome server]  [nuovo nome]
git remote remove [nome server]
```

### Sincronizzare.
```
git push [nome server] main
```
 invia i commit dal ramo main del repository locale al ramo remoto

```
git pull [nome server] main
```
 invia i commit dal ramo main del repository in remoto al ramo locale


## Creare Repository da VSCode
Creo il mio repo quickstep su github cosi ottengo indirizzo https
```
mkdir [nome directory]
cd [nome directory]
echo "# Site" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/Dechainb/[nome Repository].git
git push -u origin main
```


or push an existing repository from the command line
```
git remote add origin https://github.com/Dechainb/DechainLabs.git
git branch -M main
git push -u origin main
```
