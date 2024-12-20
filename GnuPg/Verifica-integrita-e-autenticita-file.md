
Quando scarichiamo un file prima di eseguirlo sul nostro Pc è buona norma controllare:  
1 integrità  
2 autenticità  

Per fare queste verifiche dobbiamo scaricare 3 file:  
1 file che vogliamo utilizzare es. linuxmint-22-cinnamon-64bit.iso   
2 file sha256sum.txt  
3 file sha256sum.txt.gpg  

## Verifica step by step  
* mi posiziono nella directory dove scaricherò i file<br>
`dechain@dechain-HPeliteD:~$ cd Scaricati`
* Scarico il file.iso  "copio il link da sito e lo incollo a terminale scrivendo prima il comando wget
`wget https://mirrors.edge.kernel.org/linuxmint/stable/22/linuxmint-22-cinnamon-64bit.iso`  
* scarico il file di hash del mio file .iso  
`wget https://mirrors.edge.kernel.org/linuxmint/stable/22/sha256sum.txt`  
* scarico il file sha256sum.txt crittografato con la chiave privata dello sviluppatore  
`wget https://mirrors.edge.kernel.org/linuxmint/stable/22/sha256sum.txt.gpg`  
Ora nella directory Scaricati o i miei file.
## Verifica integrità utilizzando algoritmo di hash SHA256
La checksum di un file è una sorta di *impronta digitale*  del contenuto del file, creata mediante una funzione di hash crittografico. Essa fornisce un valore univoco che può essere utilizzato per verificare l'integrità del file, ossia per assicurarsi che non sia stato   
1 modificato da una terza parte  
2 danneggiato durante il download

* eseguire il comando  
`dechain@dechain-HPeliteD:~/Scaricati$ sha256sum -b linuxmint-22-cinnamon-64bit.iso`  
questo comando esegue l'hash del file .iso il risultato sarà    
`7a04b54830004e945c1eda6ed6ec8c57ff4b249de4b331bd021a849694f29b8f *linuxmint-22-cinnamon-64bit.iso`  
* aprire il file sha256sum.txt e verificare visivamente che i due hash corrispondano  
`dechain@dechain-HPeliteD:~/Scaricati$ cat sha256sum.txt` 


Come Funziona l'algoritmo di Hash SHA256

Una funzione di hash prende come input un file e genera un valore hash di lunghezza fissa, che rappresenta il contenuto del file in modo univoco.<br>
Se anche un singolo bit del file cambia, la checksum generata cambierà drasticamente. Questo significa che anche la minima modifica del file produce un valore di checksum completamente diverso.

### Verifica dell'autenticità utilizzando Gnupg
Dobbiamo ora verificare l'autenticità dell'hash prodotto dal nostro file .iso che, come abbiamo visto corrisponde al file pubblicato dallo sviluppatore "sha256sum.txt". Per farlo dobbiamo estrarre dal file sha256sum.txt.gpg il file sha256sum.txt

Se avviamo per la prima volta Gpg dobbiamo digitare il comando  
`gpg --list-keys`  
Nella home verrà creata la directory .gnupg con all'interno:
* pubring.kbx e copia di backup pubring kbx~  detto keyring pubblico, contiene le chiavi pubbliche conosciute dall'utente. Queste chiavi sono usate per cifrare messaggi indirizzati al destinatario ( un messaggio viene cifrato con la chiave pubblica del destinatario) o verificare le firme di un messaggio

* trustdb.gpg che contiene info sulla fiducia relativa alle chiavi pubbliche

* private-keys-v1.d contiene le chiavi private in formato cifrato gestite da GnuPg. E' un luogo sicuro in cui vengono conservate le chiavi private associate agli utenti utilizzate per decriptare messaggi o firmare digitalmente i dati.<br>
Questo è quello che vedrò a terminale:  
`dechain@dechain-HPeliteD:~/Scaricati$ gpg --list-keys`<br>
gpg: directory '/home/dechain/.gnupg' creata<br>
gpg: keybox '/home/dechain/.gnupg/pubring.kbx' creato<br>
gpg: /home/dechain/.gnupg/trustdb.gpg: creato il trustdb<br>

* Primo step è scaricare la chiave pubblica dello sviluppatore, solitamente la troviamo nel sito.
`dechain@dechain-HPeliteD:~/Scaricati$ gpg --keyserver hkp://keys.openpgp.org:80 --recv-key 27DEB15644C6B3CF3BD7D291300F846BA25BAE09`
Vediamola...
```
dechain@dechain-HPeliteD:~/Scaricati$ gpg --list-keys
/home/dechain/.gnupg/pubring.kbx
--------------------------------
pub   rsa4096 2016-06-07 [SC]
      27DEB15644C6B3CF3BD7D291300F846BA25BAE09
uid           [ sconosciuto] Linux Mint ISO Signing Key <root@linuxmint.com>
```
* Ora verifichiamo l'autenticità del file sha256sum.txt.gpg
`gpg --verify sha256sum.txt.gpg sha256sum.txt`
Cosa fa questo comando...  
gpg --verify viene utilizzato per verificare la firma digitale del file sha256sum.txt. Questo tipo di verifica assicura che il file .txt e il file .txt.gpg non siano stati alterati e che provengano effettivamente dalla persona o entità che ha firmato il file.
Nello specifico:
*GPG verifica che la firma in sha256sum.txt.gpg corrisponda al contenuto di sha256sum.txt.  
* GPG verifica anche se la firma è stata generata con una chiave privata corrispondente alla chiave pubblica che abbiamo scaricato nel nostro portachiavi.

Il risultato sarà  
gpg: Firma effettuata Mon Jul 22 20:03:50 2024 CEST  
gpg:                utilizzando la chiave RSA   27DEB15644C6B3CF3BD7D291300F846BA25BAE09  
gpg: Firma valida da "Linux Mint ISO Signing Key <root@linuxmint.com>" [sconosciuto]  
gpg: ATTENZIONE: questa chiave non è certificata con una firma fidata.  
gpg:          Non ci sono indicazioni che la firma appartenga al proprietario.  
Impronta digitale chiave primaria: 27DE B156 44C6 B3CF 3BD7  D291 300F 846B A25B AE09


[Verifica firme di Musumeci](https://www.youtube.com/watch?v=loi7XTrw7tE "verifica firme by Musumeci")  
[Verifica software Linux Cinnamon](https://linuxmint-installation-guide.readthedocs.io/en/latest/verify.html) 

