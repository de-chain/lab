[Verifica firme di Musumeci](https://www.youtube.com/watch?v=loi7XTrw7tE "verifica firme by Musumeci")
[verifica software Linux Cinnemon](https://linuxmint-installation-guide.readthedocs.io/en/latest/verify.html) 

Preparazione alla verifica<br>
`cd Scaricati` mi posiziono nella directory dove scaricherò i file<br>
`wget SHA256SUMS` contains checksums for all the available images.<br>
`wget SHA256SUMS.gpg` GnuPG signature for that file .iso i will download<br>
`wget http://ftp.uni-kl.de/pub/linux/ubuntu-dvd/xubuntu/releases/24.04/release/xubuntu-24.04.1-desktop-amd64.iso` Desktop image for 64-bit PC (AMD64) computers (standard download)<br>

## sha256, verifica integrità file 

La checksum di un file è una sorta di *impronta digitale*  del contenuto del file, creata mediante una funzione di hash crittografico. Essa fornisce un valore univoco che può essere utilizzato per verificare l'integrità del file, ossia per assicurarsi che non sia stato 
* modificato da una terza parte
* danneggiato durante il download

Esempio di Hash<br>
c333806173558ccc2a95f44c5c7b57437ee3d409b50a3a5a1367bcf7eaf3ef90 *xubuntu-24.04.1-desktop-amd64.iso

Come Funziona la Checksum: l'algoritmo di Hashing sha256

Una funzione di hash prende come input un file e genera un valore hash di lunghezza fissa, che rappresenta il contenuto del file in modo univoco.<br>
Se anche un singolo bit del file cambia, la checksum generata cambierà drasticamente. Questo significa che anche la minima modifica del file produce un valore di checksum completamente diverso.

### Generare una checksum dal file .ISO scaricato e confrontarlo con la Checksum SHA256SUMS.

* metodo 1<br>
`sha256sum xubuntu-24.04.1-desktop-amd64.iso` sha256sum should then print out a single line after calculating the hash:<br>
c01b39c7a35ccc3b081a3e83d2c71fa9a767ebfeb45c69f08e17dfe3ef375a7b *xubuntu-24.04.1-desktop-amd64.iso.<br>
Compare the hash (the alphanumeric string on left) that your machine calculated with the corresponding hash in the **SHA256SUMS** file.

* metodo 2<br>
`sha256sum -c SHA256SUMS 2>&1 | grep OK`<br>
`xubuntu-24.04.1-desktop-amd64.iso: OK`<br>
If you get no results (or any result other than that shown above) then the ISO file does not match the checksum. This could be because the ISO has been altered, or it downloaded incorrectly - either way you should download a fresh ISO from a known good source.

## gnugpg, verifica autenticità del file

`gpg --list-keys` If this is the first time you have run gpg, this will create a trust database for the current user.<br>
nella home troveremo la directory .gnupg con all interno:
* pubring.kbx e copia di backup pubring kbx~  detto keyring pubblico, contiene le chiavi pubbliche conosciute dall'utente. Queste chiavi sono usate per cifrare messaggi indirizzati al destinatario ( un messaggio viene cifrato con la chiave pubblica del destinatario) o verificare le firme di un messaggio
* trustdb.gpg che contiene info sulla fiducia relativa alle chiavi pubbliche
* private-keys-v1.d contiene le chiavi private in formato cifrato gestite da GnuPg. E' un luogo sicuro in cui vengono conservate le chiavi private associate agli utenti utilizzate per decriptare messaggi o firmare digitalmente i dati.<br>

`dechain@dechain-HPeliteD:~/Scaricati$ gpg --list-keys`<br>
gpg: directory '/home/dechain/.gnupg' creata<br>
gpg: keybox '/home/dechain/.gnupg/pubring.kbx' creato<br>
gpg: /home/dechain/.gnupg/trustdb.gpg: creato il trustdb<br>

`gpg --keyid-format long --verify SHA256SUMS.gpg SHA256SUMS`<br>
Se non abbiamo alcuna chiave pubblica presente nel nostro file pubring.kbx avro il seguente messaggio:
```
gpg: Signature made Thu Apr  5 22:19:36 2018 EDT
 using DSA key ID 46181433FBB75451
gpg: Can't check signature: No public key
gpg: Signature made Thu Apr  5 22:19:36 2018 EDT
  using RSA key ID D94AA3F0EFE21092
gpg: Can't check signature: No public key
```
This is actually a really useful message, as it tells us which key or keys were used to generate the signature file. Knowing these ID numbers (46181433FBB75451 and D94AA3F0EFE21092 in the example), means we can request them from the Ubuntu key server.

This is done with the following command. Note that the ID numbers are hexadecimal, so we prefix them with 0x:

`gpg --keyid-format long --keyserver hkp://keyserver.ubuntu.com --recv-keys 0x46181433FBB75451 0xD94AA3F0EFE21092` This command should retrieve the keys we want and add them to your keyring. You should see a message like this:
```
gpg: requesting key 46181433FBB75451 from hkp server keyserver.ubuntu.com
gpg: requesting key D94AA3F0EFE21092 from hkp server keyserver.ubuntu.com
gpg: /root/.gnupg/trustdb.gpg: trustdb created
gpg: key 46181433FBB75451: public key "Ubuntu CD Image Automatic Signing Key <cdimage@ubuntu.com>" imported
gpg: key D94AA3F0EFE21092: public key "Ubuntu CD Image Automatic Signing Key (2012) <cdimage@ubuntu.com>" imported
gpg: no ultimately trusted keys found
gpg: Total number processed: 2
gpg:               imported: 2  (RSA: 1)
```
You can now inspect the key fingerprints by running:

`gpg --keyid-format long --list-keys --with-fingerprint 0x46181433FBB75451 0xD94AA3F0EFE21092` …which should produce the following output:

```
pub   dsa1024/46181433FBB75451 2004-12-30 [SC]
      Key fingerprint = C598 6B4F 1257 FFA8 6632  CBA7 4618 1433 FBB7 5451
uid                  Ubuntu CD Image Automatic Signing Key <cdimage@ubuntu.com>

pub   rsa4096/D94AA3F0EFE21092 2012-05-11 [SC]
      Key fingerprint = 8439 38DF 228D 22F7 B374  2BC0 D94A A3F0 EFE2 1092
uid                  Ubuntu CD Image Automatic Signing Key (2012) <cdimage@ubuntu.com>
```



