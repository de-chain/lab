# Partizione


Il partizionamento è un mezzo per dividere un singolo disco rigido in molte unità logiche. Una partizione è un insieme contiguo di blocchi su un'unità trattati come un disco indipendente. Una tabella delle partizioni (la cui creazione è l'argomento di questo howto) è un indice che mette in relazione le sezioni del disco rigido con le partizioni.

I dispositivi di memoria di uso più comune (hard disk o SSD con standard PATA o SATA, dischi o memorie flash USB) vengono identificati come /dev/sda, /dev/sdb, /dev/sdc, ecc.
Le partizioni, aree delimitata e ben definite del disco in cui vengono memorizzati dati, vengono identificate aggiungendo un numero alla sigla del dispositivo.
Ad esempio se nel proprio computer è presente un unico hard disk, esso sarà individuato come /dev/sda e le partizioni al suo interno come /dev/sda1, /dev/sda2, ecc..

Perché avere più partizioni?

1. Incapsula i tuoi dati. Poiché il danneggiamento del file system è locale in una partizione, rischi di perdere solo alcuni dei tuoi dati in caso di incidente.

2. Aumentare l'efficienza dello spazio su disco. Puoi formattare partizioni con dimensioni di blocco variabili, a seconda dell'utilizzo. Se i tuoi dati sono contenuti in un gran numero di file di piccole dimensioni (meno di 1k) e la tua partizione utilizza blocchi di dimensioni 4k, stai sprecando 3k per ogni file. In generale, si spreca in media metà di un blocco per ogni file, quindi è importante far corrispondere la dimensione del blocco alla dimensione media dei file se si hanno molti file.

3. Limitare la crescita dei dati. Processi fuori controllo o utenti maniacali possono consumare così tanto spazio su disco che il sistema operativo non ha più spazio sul disco rigido per le sue operazioni contabili. Ciò porterà al disastro. Segregando lo spazio, ti assicuri che elementi diversi dal sistema operativo muoiano quando lo spazio su disco allocato viene esaurito.

Gnu Linux ha bisogno di una partizione che contiene il sistema operativo, le applicazioni e i file personali dell’utente.

La partizione di swap separata è consigliata ma
non è obbligatorio averla. **Lo «swap» è uno spazio a disposizione del sistema operativo, da usare come «memoria virtuale»;** usare una partizione separata per lo swap, permette a Linux di usarlo in modo molto più efficiente. 

La maggior parte degli utenti sceglie di avere più partizioni per GNU/Linux:
1. per la sicurezza: se si verifica un guasto che corrompe il file
system, di solito viene colpita solo una partizione; quindi per ripristinare il funzionamento, basterà sostituire solo una porzione del proprio sistema (utilizzando la copia di backup conservata con cura). Come minimo è consigliabile creare quella che si chiama in gergo «partizione root», che contiene le componenti fondamentali del sistema. Se qualche altra partizione viene corrotta, sarà ancora possibile avviare GNU/Linux per riparare il sistema, evitando di dover reinstallare il sistema da capo.
2. Il secondo motivo di solito è più rilevante in un contesto di lavoro, ma in generale dipende dall’uso che si fa del computer

L’unico vero difetto nell’uso di più partizioni consiste nel fatto che spesso è difficile conoscere in anticipo le proprie
necessità. 
## l'albero delle directory
Debian GNU/Linux è conforme al Filesystem Hierarchy Standard per la denominazione dei file e delle directory.
Questo standard consente agli utenti e ai programmi di predire la posizione di file e directory sul sistema. La directory
«root» (principale) del sistema è rappresentata semplicemente dal carattere «slash»: /. A questo livello, tutti i sistemi
Debian contengono le seguenti directory:

bin - File binari dei comandi essenziali
boot - File statici del boot loader
dev - File di device
etc - Configurazioni di sistema specifiche per l’host
home - Directory home degli utenti
lib - Librerie condivise essenziali e moduli del kernel
media - Punti di montaggio per dispositivi rimovibili
mnt - Punti di montaggio per montare un file system
temporaneamente
proc - Directory virtuale per le informazioni di sistema
root - Directory home dell’utente root
run - Dati variabili dei programmi in esecuzione
sbin - File binari essenziali per il sistema
sys - Directory virtuale per le informazioni di sistema
tmp - File temporanei
usr - Gerarchia secondaria
var - Dati variabili
srv - Dati dei servizi forniti dal sistema
opt - Pacchetti software applicativi opzionali

- La partizione «root» / deve sempre contenere fisicamente /etc, /bin, /sbin, /lib, /dev e /usr, altrimenti non sarà possibile avviare il sistema. Ciò vuol dire che occorrono circa 600–750MB di spazio disco per la partizione root quando contiene /usr oppure 5–6GB per una installazione workstation o server.
-  /var: dati variabili, come code di posta e di messaggi news, siti web, database, la cache del sistema di gestione dei pacchetti, ecc. verranno conservati in questa directory. La dimensione da scegliere dipende fortemente dal tipo di uso che si farà del sistema, ma per la maggior parte degli utenti il fattore principale di cui tenere conto è il funzionamento del sistema di gestione dei pacchetti: se si intende installare in una sola sessione tutto il
software fornito da Debian, dovrebbero bastare 2 o 3 GB di spazio per /var. Se invece si intende installare il sistema a più riprese (ad esempio, installare le utilità di sistema, poi quelle per la gestione dei documenti, poi
il sistema X, ecc), è sufficiente riservare da 300 a 500 MB.
- /tmp: i dati temporanei creati dai programmi vengono scritti prevalentemente in questa directory. Di solito è
sufficiente riservare da 40 a 100 MB. Alcune applicazioni (tra cui gestori di archivi, strumenti per la creazione
di CD e DVD, e software multimediale) utilizzano /tmp per scrivere file di immagine temporanei; se si intende
utilizzare questo tipo di applicazioni, occorrerà scegliere una dimensione adeguata per la directory /tmp.
- /home: ogni utente conserverà i propri dati personali in una sotto-directory di questa directory. La sua dimensione dipende dal numero di utenti che utilizzeranno il sistema e dal tipo di file che saranno conservati
nelle loro directory


## schema di partizionamento
Per i nuovi utenti, i sistemi Debian personali, per l’uso casalingo, o per altre situazioni mono-utente, probabilmente la
soluzione più semplice è costituita da una sola partizione / (più lo swap). Il tipo di partizione raccomandato è ext4.
Per i sistemi multi-utente, o i sistemi con molto spazio su disco, la soluzione migliore consiste nel mettere /var,
/tmp e /home ognuna sulla propria partizione separata dalla partizione /.
Potrebbe essere necessario avere una partizione /usr/local separata, se si ha intenzione di installare molti
programmi che non sono compresi nella distribuzione Debian. Se il computer sarà un server di posta, può essere
consigliabile avere una partizione separata per /var/mail. Se il sistema sarà un server con molti account utente, è
consigliabile avere una grande partizione /home separata. In generale, lo schema di partizionamento ottimale varia
da computer a computer, a seconda dell’uso che si farà.

Il programma di partizionamento usato nel installatore Debian è abbastanza versatile, permette di creare
diversi schemi di partizionamento, di usare varie tabelle di partizione, file system e device a blocchi.

L’Installatore supporta
- LVM (Logical Volume Management)
- RAID Software
È supportato il RAID di livello 0, 1, 4, 5, 6 e 10.
- Cifratura
- Multipath (sperimentale)

Sono supportati i seguenti file system.
- ext2, ext3, ext4
Nella maggior parte dei casi il file system predefinito è ext4; per le partizioni /boot viene scelto ext2 quando
è usato il partizionamento guidato.
- jfs (non disponibile su tutte le architetture)
- xfs (non disponibile su tutte le architetture)
- reiserfs (opzionale; non disponibile su tutte le architetture)
Il supporto per il file system Reiser non è più disponibile in modo predefinito. È possibile attivarlo usando
l’Installatore a priorità media o bassa e selezionando il componente partman-reiserfs. È supportata solo
la versione 3 del file system.
- qnx4
Le partizioni esistenti sono riconosciute ed è possibile assegnare loro un punto di mount. Non è possibile creare
nuove partizioni qnx4.
- FAT16, FAT32
- NTFS (solo-lettura)
Le partizioni NTFS esistenti possono essere ridimensionate ed è possibile assegnare loro un punto di mount.
Non è possibile creare nuove partizioni NTFS

## Nomi dei dispositivi in Linux

- Il primo disco rilevato è chiamato /dev/sda.
- Il secondo disco rilevato è chiamato /dev/sdb, e così via.
- Il primo CD-ROM SCSI è chiamato /dev/scd0, o anche /dev/sr0.

Le partizioni su ciascun disco sono identificate aggiungendo un numero decimale al nome del disco: sda1 e sda2 rappresentano la prima e la seconda partizione del primo disco SCSI sul sistema.

Ecco un esempio realistico. Ipotizzando di avere un sistema con 2 dischi SCSI, uno con indirizzo SCSI 2 e l’altro con indirizzo SCSI 4. Il primo disco (con indirizzo 2) si chiamerà sda, il secondo sdb. Se il disco sda ha 3 partizioni, queste si chiameranno sda1, sda2 e sda3. Le stesse regole valgono per il disco sdb e per le sue partizioni.

## Programmi Debian per il partizionamento
Gli sviluppatori Debian hanno adattato vari programmi per il partizionamento in modo che funzionino su vari tipi
di hard disk e su varie architetture di sistema. Quello che segue è un elenco dei programmi disponibili a seconda
dell’architettura.
1. partman Lo strumento di partizionamento raccomandato da Debian. Questo «coltellino svizzero» dai mille usi, può
anche ridimensionare le partizioni, creare file system (ossia «formattarli» nel gergo di Windows) e assegnarli ai punti di montaggio.
2. fdisk Il partizionatore originale di Linux, riservato ai guru.
Occorre fare attenzione se si hanno partizioni FreeBSD sulla propria macchina: i kernel del sistema d’installazione comprendono il supporto per queste partizioni, ma all’interno di fdisk esse potrebbero avere dei nomi di device diversi. 

Si veda il [Linux+FreeBSD HOWTO](https://tldp.org/HOWTO/Linux+FreeBSD-2.html)

3. cfdisk Un partizionatore semplice, con interfaccia a schermo intero, adatto a tutti.
Si noti che cfdisk non riconosce le partizioni FreeBSD, quindi anche in questo caso i nomi dei dispositivi
potrebbero risultare diversi da quanto ci si aspetta



## Partizionare per PC 64 bit
Per utilizzare un nuovo disco fisso (oppure per cancellare completamente l’intera tabella delle partizioni del proprio disco) è necessario creare una nuova tabella delle partizioni. Con il «Partizionamento guidato» la tabella delle partizioni
viene creata automaticamente, invece con il partizionamento manuale occorre selezionare la voce che corrisponde al disco con il livello più alto e premere Invio.  
Sui sistemi UEFI il tipo
di tabella predefinito è «gpt», sui sistemi più vecchi con BIOS il tipo predefinito è «msdos».

Quando viene scelta una tabella delle partizioni di tipo «gpt» (il valore predefinito sui sistemi UEFI), viene automaticamente aggiunto uno spazio libero da 1 MB all’inizio
del disco. Ciò è intenzionale e necessario per poi inserirci il bootloader GRUB 2.  

Sebbene i moderni sistemi UEFI non abbiano le limitazioni elencate in seguito, i vecchi PC con BIOS hanno
alcuni vincoli riguardanti il partizionamento del disco. C’è un limite al numero di partizioni «primarie» e «logiche»
che possono essere contenute in un disco.  
Inoltre, i BIOS anteriori al periodo 1994–98 contengono limitazioni sulla
posizione del disco che può essere avviata dal BIOS.  
Le partizioni «primarie» sono il tipo di partizione tradizionale per i dischi dei PC. Tuttavia, possono esisterne
al massimo quattro per ogni disco, per superare questa limitazione, sono state introdotte le partizioni «estese» e
«logiche». Impostando una partizione primaria come partizione estesa, è possibile suddividere ulteriormente lo spazio
allocato a questa partizione in più partizioni logiche. È possibile creare fino a 60 partizioni logiche per ogni partizione
estesa, ma **è possibile avere solo una partizione estesa per ogni disco.**  

## Partizione manuale disco fisso

Il partizionamento manuale è il modo più tradizionale di installare Linux e fornisce maggior controllo e flessibilità in tanti tipi di scenari differenti. 

Le partizioni obbligatorie per installare Linux sono solo due. Diverse ragioni connesse spesso alla scelta di fare partizionamenti manuali, sono legate all'opportunità di separare le componenti operative delle parti del sistema, con partizioni che non sono obbligatorie.

1 Partizione EFI per il boot loader (l'avvio)

2 Partizione radice per il sistema e i programmi

* Partizione opzionale swap  
Si tratta di uno spazio su hard-disk in cui sono temporaneamente parcheggiate informazioni quando la memoria RAM non basti a contenerle tutte. Lo swap è utile se un bug in un programma esaurisce la RAM rendendo instabile il sistema, o, più spesso, quando cerchi di far compiere operazioni troppo impegnative ad un computer inadeguato e con troppa poca RAM.  La partizione di swap non è obbligatoria. Infatti l'installazione automatica di Linux Mint crea automaticamente solo un file di swap nella stessa partizione del sistema. In ambiente Windows è previsto lo stesso meccanismo.  
In Debian questo non viene fatto, quindi è consigliabile crearla

| Ram Sistema | Spazio Swap |
|-------------|-------------|
| 4GB         | 2GB         |
| 4-16GB      | 4GB         |
| 16-64GB     | 8GB         |
| 64-256GB    | 16GB        |

* Partizione home
Inserire la cartella home con le singole cartelle di documenti degli utenti in apposita partizione separata dal sistema e dai programmi. 
Si tratta di una partizione non obbligatoria per far funzionare Linux. E' utile se viene reinstallato spesso il sistema operativo 
o se viene posizionata in un disco dati differente.

Gparted è il programma utilizzato durante l'installazione del sistema.  
Con i moderni SSD non ha molto senso la sequenza e posizione delle partizioni come invece influiva con i dischi meccanici. 

1 Identificare lo spazio libero del disco.  
2 Creiamo la prima partizione obbligatoria, la partizione di sistema in formato Efi. bastano 300 mb

![alt text](<Images/Partizione EFI.png>)

Diciamo al sistema che il boot loader deve essere posizionato li

![alt text](<Images/Posizione boot loader.png>)

2 Creiamo la seconda partizione obbligatoria, la partizione radice in formato Ext
Se creeremo una apposita partizione per la cartella /home, riserviamo alla partizione root almeno 60 GB per far stare comodo il sistema e diversi programmi

![alt text](<Images/Partizione Radice.png>)

3 Creiamo la partizione Swap in formato area Swap "vedi tabella sopra per definire la grandezza".

![alt text](<Images/Partizione Swap.png>)

4 Creiamo la partizione Home con lo spazio rimasto libero in formato Ext

![alt text](<Images/Partizione Home.png>)

Bibliografia

[Ubuntu partizioni](https://wiki.ubuntu-it.org/Hardware/DispositiviPartizioni/Partizioni)<br>
[Cos'è una partizione HOWTO](https://tldp.org/HOWTO/Partition/intro.html#howtos)
[Alternativalinux](https://www.alternativalinux.it/come-installare-linux-mint-con-partizioni-manuali/simplenote
)