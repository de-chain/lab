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
viene creata automaticamente, invece con il partizionamento manuale occorre selezionare la voce che corrisponde al disco con il livello più alto e premere Invio. Sui sistemi UEFI il tipo
di tabella predefinito è «gpt», sui sistemi più vecchi con BIOS il tipo predefinito è «msdos». I valori predefiniti sono utilizzati automaticamente quando l’installazione procede con la priorità standard.

Quando viene scelta una tabella delle partizioni di tipo «gpt» (il valore predefinito sui
sistemi UEFI), viene automaticamente aggiunto uno spazio libero da 1 MB all’inizio
del disco. Ciò è intenzionale e necessario per poi inserirci il bootloader GRUB 2.
Se si usa già un altro sistema operativo come DOS o Windows e si intende preservarlo mentre si installa Debian,
potrebbe essere necessario ridimensionare la sua partizione per liberare spazio per l’installazione di Debian. L’installatore supporta il ridimensionamento dei file system FAT e NTFS: arrivati alla fase di partizionamento, occorre
selezionare l’opzione Manuale e poi scegliere la partizione esistente da ridimensionare.
Sebbene i moderni sistemi UEFI non abbiano le limitazioni elencate in seguito, i vecchi PC con BIOS hanno
alcuni vincoli riguardanti il partizionamento del disco. C’è un limite al numero di partizioni «primarie» e «logiche»
che possono essere contenute in un disco. Inoltre, i BIOS anteriori al periodo 1994–98 contengono limitazioni sulla
posizione del disco che può essere avviata dal BIOS. È possibile trovare maggiori informazioni nel Linux Partition
HOWTO anche se questo capitolo contiene una breve panoramica utile nella maggior parte delle situazioni.
Le partizioni «primarie» sono il tipo di partizione tradizionale per i dischi dei PC. Tuttavia, possono esisterne
al massimo quattro per ogni disco; per superare questa limitazione, sono state introdotte le partizioni «estese» e
«logiche». Impostando una partizione primaria come partizione estesa, è possibile suddividere ulteriormente lo spazio
allocato a questa partizione in più partizioni logiche. È possibile creare fino a 60 partizioni logiche per ogni partizione
estesa, ma è possibile avere solo una partizione estesa per ogni disco.
Linux limita il numero delle partizioni per disco a 255 partizioni sui dischi SCSI (3 partizioni primarie e 252
partizioni logiche), e a 63 partizioni sui dischi IDE (3 partizioni primarie, 60 partizioni logiche). Tuttavia, il sistema
Debian GNU/Linux standard fornisce solo 20 file di device per rappresentare le partizioni, quindi se si intende creare
più di 20 partizioni occorrerà prima creare manualmente i device per le nuove partizioni.
Se si possiede un disco IDE grande e non si sta usando né l’indirizzamento LBA, né i driver talvolta forniti dai
produttori di hard disk, allora la partizione di avvio (quella che contiene l’immagine del kernel) deve trovarsi all’interno
dei primi 1024 cilindri del disco (di solito circa 524 MB, senza traduzione da parte del BIOS).
Questa restrizione non è rilevante se si possiede un BIOS più recente del periodo 1995–98 (a seconda del produttore) che supporta la «Enhanced Disk Drive Support Specification». Il programma alternativo a Lilo di Debian
mbr deve affidarsi al BIOS per leggere il kernel dal disco e caricarlo nella RAM. Se il BIOS supporta le estensioni
int 0x13 per l’accesso ai dischi grandi, queste verranno utilizzate; altrimenti occorrerà utilizzare la vecchia interfaccia
di accesso al disco, che non può accedere porzioni del disco che si trovano oltre il 1023-esimo cilindro. Una volta
avviato Linux, qualsiasi sia il BIOS del computer, queste restrizioni non sono più vincolanti, visto che Linux non usa
il BIOS per accedere al disco.
Se si ha un disco grande, è possibile che si debbano usare tecniche di traduzione del numero di cilindri da attivare
nel proprio BIOS, come ad esempio l’LBA (Logical Block Addressing) o la modalità CHS («Large»). È possibile
trovare maggiori informazioni su questo problema nel Large Disk HOWTO. Se si usa uno schema di traduzione del
numero di cilindri e il BIOS non supporta le estensioni per l’accesso ai dischi grandi, allora la partizione di avvio deve
essere compresa all’interno del 1024-esimo cilindro nella sua rappresentazione tradotta.
Il modo consigliato di risolvere questo problema consiste nel creare una piccola partizione (25–50MB dovrebbero
essere sufficienti) all’inizio del disco, da usare come partizione di avvio, e di creare tutte le altre partizioni nello spazio
rimanente. Questa partizione di avvio deve essere montata su /boot, la directory destinata a contenere i kernel
Linux. Questo tipo di configurazione funzionerà su tutti i sistemi, sia che venga usato l’LBA o la traduzione CHS, e
a prescindere dal fatto che il proprio BIOS supporti le estensioni per l’accesso ai dischi grandi.


Bibliografia

[Ubuntu partizioni](https://wiki.ubuntu-it.org/Hardware/DispositiviPartizioni/Partizioni)<br>
[Cos'è una partizione HOWTO](https://tldp.org/HOWTO/Partition/intro.html#howtos)