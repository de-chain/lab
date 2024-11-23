## Definizione
GnuPG (GNU Privacy Guard), spesso abbreviato come GPG, è uno strumento di crittografia a chiave pubblica che permette di cifrare, decifrare e firmare digitalmente file e messaggi, garantendo privacy e autenticità delle comunicazioni. È un'implementazione libera dello standard OpenPGP (Pretty Good Privacy), uno dei principali protocolli per la crittografia end-to-end.

Installare Gnupg  
` sudo apt-get install gnupg2 `

## Generare nuova coppia di chiavi  
Crea la directory .gnupg e il file che contiene la pubkey .gnupg/pubring.kbx\
`gpg --full-generate-key`

* Il programma ti chiederà quattro opzioni di chiavi:  
Opzione 1 RSA - RSA (default piu usata).  
Opzione 2  DSA and Elgamal, crea due coppie di chiavi: una coppia di chiavi di tipo DSA che rappresenta la coppia di chiavi primaria ed è utilizzabile solo per firmare; una coppia di chiavi subordinata di tipo ElGamal, usata per criptare.  
Opzione 3 DSA (firma solo), è simile alla precedente ma crea solo una coppia di chiavi DSA. L’opzione 3 crea una singola coppia di chiavi ElGamal utilizzabile sia per firmare che per criptare. In tutti i casi è possibile in un secondo momento creare sotto-chiavi addizionali per cifrature e firme.<br> 
Opzione 4  RSA (firma solo).

* La dimensione, 4096 è la dimensione che rende compatibile la chiave anche con altri strumenti.

* Expire date, scelgo una data di scadenza per la chiave o lascio senza scadenza

* Dati personali, il sistema chiederà di inserire nomi, commenti e indirizzi e-mail, che verranno usati per la costruzione della chiave; questi potranno essere modificati in parte anche successivamente.

* Passphrase, infine, occorre scegliere una password (di solito si usa il termine passphrase, frase segreta, visto che sono ammessi gli spazi), che andrà immessa ogni volta che si useranno funzionalità che richiedono la chiave privata. Deve essere abbastanza robusta.


Dopo aver immesso tutti i dati, il sistema inizia a generare le chiavi. Questa operazione richiede un po’ di tempo, durante il quale il sistema deve raccogliere molti dati casuali. Si può aiutare a generare dati casuali ad esempio lavorando su un’altra finestra. Ogni chiave generata è diversa dalle altre: se si genera una chiave e dopo cinque minuti se ne genera un’altra fornendo gli stessi dati (nome, email, passphrase, ecc.), si otterrà una chiave diversa.

Comandi Gpg<br>
`gpg --version`  
`gpg --list-keys` lista chiavi  
`gpg --list-sigs` lista firme  
`gpg --fingerprint` mostra le impronte digitali o fingerprint.  Vedere le impronte digitali serve ad assicurarsi che la chiave appartenga davvero alla persona che sostiene di esserne il proprietario.<br>
L’output di questo comando è una breve lista di numeri.<br>
**Non ha alcuna utilità vedere firme o impronte digitali di chiavi private**<br>  
`gpg --list-secret-keys` lista chiavi private<br>
`gpg --delete-key [UID]` cancella una chiave pubblica<br>
`gpg --delete-secret-key` cancella chiave privata<br>
`gpg --edit-key [UID]` è possibile modificare la data di scadenza di una chiave, 
aggiungere UID o firmare una chiave.<br> 
Dopo aver eseguito il comando si otterrà un prompt interattivo da cui digitare i comandi successivi.

## Rete di fiducia 

La diffusione delle chiavi pubbliche nella rete è un punto debole della cittografia asimmetrica. Un utente malintenzionato potrebbe intercettare il messaggio, modificarlo, crittografarlo con la propria chiave privata e la chiave pubblica del destinatario, spacciandosi per il vero mittente. Il destinatario non si accorgerebbe dello scxambio di persona perchè usando la chiave pubblica del malintenzionato, la firma digitale risulterà corretta.
La soluzione adottata da PGP (e quindi da GnuPG)<br>*è la firma delle chiavi: una chiave pubblica può essere firmata da altre persone, certificando così` che la chiave appartiene veramente alla persona che sostiene di esserne il proprietario.*<br> In questo modo io conosco la vera chiave pubblica della persona.
La decisione su quanta fiducia riporre nelle firme spetta all’utente di GnuPG: sostanzialmente la fiducia in una firma dipende dalla fiducia che si ha nella chiave della persona che ha apposto la firma. Per essere assolutamente sicuri che una chiave appartenga a una certa persona, è consigliabile fare un controllo della cosiddetta impronta digitale della chiave ("fingerprint") usando un canale di comunicazione sicuro.

### Firmare le chiavi
Come accennato nell’introduzione, il principale tallone d’Achille del sistema è l’autenticità delle chiavi pubbliche: se si usa una chiave pubblica contraffatta si può dire addio alla crittografia sicura. Per evitare questo rischio, c’è la possibilità di firmare le chiavi, ossia di porre la propria firma digitale sulla chiave, certificandone la validità. In pratica, la firma certifica che lo user ID menzionato nella chiave corrisponde alla persona che possiede la chiave. Una volta che si è certi di questo, si può usare la chiave in tutta sicurezza.
Per firmare una chiave, si usi il comando `gpg --edit-key [UID]` e successivamente il comando `sign`.
Bisogna firmare una chiave solo quando si è ASSOLUTAMENTE CERTI della sua autenticità!!!
Questa condizione può verificarsi quando si è ricevuta la chiave direttamente da una persona (ad esempio durante un key signing party, un raduno per la firma delle chiavi) o quando la si è ricevuta per altri mezzi e se ne è controllata l'autenticità col metodo dell’impronta digitale (ad esempio al telefono). Non si dovrebbe mai firmare una chiave a priori.

## Cifrare/firmare un messaggio con la criptografia a chiave pubblica-privata

Sono entrambi cifrature ma hanno utilizzo diverso

* Scenario nr 1: firma del messaggio con la sola chiave privata del mittente garantisce l'autenticità del messaggio.
  1. autenticità perchè solo il mittente con la sua  chiave privata può firmare il messaggio.<br>
In questo scenario la chiave privata produce una *firma digitale* che consente di garantire che il messaggio provenga effettivamente dal possessore della chiave privata e che non sia stato alterato.
Per firmare un messaggio è necessario avere una chiave privata nel proprio keyring, *directory private-keys-v1.d.* 

`gpg --list-keys` If this is the first time you have run gpg, this will create a trust database for the current user.<br>
nella home troveremo la directory .gnupg con all interno:
* pubring.kbx e copia di backup pubring kbx~  detto keyring pubblico, contiene le chiavi pubbliche conosciute dall'utente. Queste chiavi sono usate per cifrare messaggi indirizzati al destinatario ( un messaggio viene cifrato con la chiave pubblica del destinatario) o verificare le firme di un messaggio
* trustdb.gpg che contiene info sulla fiducia relativa alle chiavi pubbliche
* private-keys-v1.d contiene le chiavi private in formato cifrato gestite da GnuPg. E' un luogo sicuro in cui vengono conservate le chiavi private associate agli utenti utilizzate per decriptare messaggi o firmare digitalmente i dati.

### firma messaggio
`gpg --list-secret-keys` elenca le chiavi disponibili nella directory private/keys<br>
`gpg --sign messaggio.txt` firmare un messaggio (ad esempio messaggio.txt)<br>
`gpg --default key "ID Chiave" --sign messaggio.txt` firmare un messaggio con una chiave specifica dall-elenco delle mie chiavi private<br>
`gpg --clearsign messaggio.txt` --clearsign aggiunge la firma digitale al testo, ma lascia il contenuto leggibile. Il risultato sarà un file con il testo del messaggio e la firma, che può essere facilmente verificato da chiunque abbia la tua chiave pubblica.

Questi comandi creeranno un nuovo file chiamato *messaggio.txt.gpg o messaggio.txt.asc*, che contiene il messaggio firmato digitalmente.<br>


### verifica della firma
`gpg --verify messaggio.txt.gpg`


* Scenario nr 2 firmare il messaggio con la chiave privata del mittente e cifrare il messaggio con la chiave pubblica del destinatario, garantisce autenticità e confidenzialità del messaggio.
   1. autenticità perchè solo il mittente con la sua  chiave privata può firmare il messaggio
   2. confidenzialità perchè solo il destinatario può con la propria chiave privata decriptare il messaggio

  [Vai alla firma messaggio](###-firma-messaggio) 

### cifrare il messaggio
`gpg --import chiave_pubblica_destinatario.asc` importa la chiave  nel mio pubring.kbx<br>
`gpg --recv-keys ID_ChiavePubblica` importa la chiave da un keyring pubblico<br>
`gpg --sign --encrypt --recipient destinatario@example.com messaggio.txt`
  * --sign: Firma il messaggio con la tua chiave privata, garantendo che provenga da te.
  * --encrypt: Cifra il messaggio con la chiave pubblica del destinatario, in modo che solo lui possa decifrarlo.
  * --recipient destinatario@example.com: Specifica l'email (o l'ID della chiave pubblica) del destinatario, che è la chiave pubblica che verrà usata per la cifratura.
  * messaggio.txt: È il file che contiene il messaggio che desideri cifrare e firmare.

Questo comando genererà un file cifrato e firmato, ad esempio *messaggio.txt.gpg.*

### decifrare il messaggio
`gpg --decrypt messaggio.txt.gpg`





   







DA QUI IN POI DA SISTEMARE

gpg –expert -edit-key  [pub key]
Fornisce info complete e prepara il comando di edit sulla chiave.  gpg> 


Creazione subkey addizionale 
Da usare per esempio solo per la firma
gpg> addkey

Esportare chiavi  GPG Encryption Come si usa e come si verificano le firme 7 min

Privata
gpg –export-secret-key –armor  [chiave pubblica] > fabio.priv
(crea un file fabio.prv “armor” lo scrive sotto forma di testo”)
cat fabio.priv (apro e leggo il contenuto del file)

Pubblica
gpg –export –armor  [chiave pubblica] > fabio.pub
(crea un file fabio.pub “armor” lo scrive sotto forma di testo”)
cat fabio.pub (apro e leggo il contenuto del file)
Le chiavi vanno salvate su supporto esterno con partizione cifrata
Scambiarsi le chiavi

Per comunicare con altre persone è necessario scambiarsi le chiavi pubbliche. Per elencare le chiavi presenti nel proprio portachiavi pubblico utilizzare l’opzione a linea di comando. 
gpg --list-keys

Importare una chiave

Quando si riceve la chiave pubblica di qualcuno, prima di usarla occorre importarla nel proprio portachiavi
gpg --import [nomefile]
Esportare una chiave
Il comando per esportare la chiave di un utente è:
gpg --export [UID]
gpg --export [UID]-o   
gpg --export [UID]-a
Se non si indica un UID (User ID), verranno esportate tutte le chiavi presenti nel portachiavi. L'output predefinito è lo stdout, ma è possibile dirigere l'output su un file usando l'opzione -o. In molti casi è consigliabile usare l'opzione -a per scrivere la chiave in un file ASCII a 7 bit, invece che in un file binario.
Per allargare il proprio orizzonte e permettere ad altri di inviare messaggi in modo sicuro, occorre esportare la propria chiave pubblica e pubblicarla sulla propria home page, o tramite finger, oppure caricarla su un key server.







