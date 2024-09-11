

Arguing that you don't care about the right to privacy because you have nothing to hide is no different from saying you don't care about free speech because you have nothing to say. – Edward Snowden

![alt text](Images/GnuPG.png)

OpenPGP (Pretty Good Privacy) è lo standard di crittografia,<br>
GNU Privacy Guard,spesso abbreviato con GPG o GnuPG è il programma che implementa lo standard.

Per utilizzare il sistema GnuPG, è necessario disporre di una chiave pubblica e di una chiave privata.<br>
La chiave privata è una lunga stringa univoca di numeri e lettere generata casualmente.<br>
La chiave pubblica è generata dala chiave privata secondo una specifica funzione matematica.

La tua chiave pubblica è appunto pubblica, memorizzata in una rubrica online chiamata keyserver dove è liberamente consultabile. Le persone dopo averla scaricata la usano per
1. crittografare le email che ti inviano perchè solo tu potrai decriptarle con la tua chiave privata
2. verificare l' identità delle mail che ricevono perchè solo la tua chiave pubblica puo decriptare le mail che hai criptato con la chiave privata.

La tua chiave privata è invece più simile a una vera chiave perché la tieni solo per te.

## Creare le chiavi da riga di comando
Controlliamo quale versione di Gpg abbiamo installato e se è installato
* gpg --version

Generiamo le chiavi
* gpg --full-generate-key<br>
o per alcune versioni 
* gpg --gen-key<br>
tipo di chiave<br>
opzione 1 RSA and RSA 4096 byte scadenza 2y mionome miamail

Si possono impostare ulteriori opzioni eseguendo il comando 
* gpg --edit-key [latua@email]

### Vedere le chiavi salvate
Le chiavi si trovano in una cartella nascosta della nostra Home "la nostra Tilde"<br>
.gnupg/  dove troviamo due cartelle 
* pubring.gpg
* secring.gpg
* private-keys-v1.d

I comandi per visualizzare le chiavi:

* gpg --list-keys
* gpg --list-key [mionomechiave]
* gpg --list-secret-key

I comandi per encrypt e decrypt

* gpg --encrypt --armor -r [mio_nome oppure mia_mail della mia chiave privata] [nomefile]<br>
Verrà creato un file [nomefile.asc]

* gpg nomefile.asc<br>
mi chiederà la passphrase della chiave privata per decriptare il documento





