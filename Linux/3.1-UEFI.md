# UEFI. 

## Introduzione



 UEFI Acronimo di Unified Extensible Firmware Interface (si pronuncia uify), è il successore del tradizionale BIOS, l’insieme di routine,scritte in una memoria non volatile presente sulla scheda madre, che forniscono le funzionalità basilari per l’accesso e l’utilizzo delle varie componenti del computer.

 Le specifiche di UEFI sono state pensate per rendere “il nuovo BIOS” indipendente dall’hardware e per mettere a disposizione del sistema operativo servizi di boot e runtime direttamente accessibili.

 Linux supporta UEFI già dal 2002

 Con l'introduzione dello UEFI (BIOS di nuova generazione), lo standard di riferimento per la gestione delle partizioni di un disco fisso è GPT (GUID Partition Table). È tuttavia ancora frequente l'utilizzo dell'MBR (Master Boot Record).


 Caratteristiche di GPT:

 * Utilizzo di sole partizioni primarie.
 * Superamento del limite delle 4 partizioni primarie
 * Superamento del limite dei 2 Terabyte per partizione.
 * architettura indipendente da CPU e driver
 * ambiente preOS (accessibile cioè all’infuori del sistema operativo, prima della fase di boot di quest’ultimo) molto più completo e versatile rispetto al passato. Si pensi che di solito UEFI offre anche il supporto della connettività di rete.
 *  eliminazione della necessità di un bootloader (fatta eccezione per utilizzi più avanzati)
 * esecuzione di moduli firmati (funzionalità Secure Boot)
 * conserva le informazioni sull’organizzazione del disco non solo all’inizio dell’hard disk ma anche alla fine dell’unità.
 Questo permette di ripristinare il corretto caricamento dei sistemi operativi nel caso in cui i dati stivati nel blocco d’intestazione iniziale dovessero rovinarsi per un qualunque motivo.
 Una serie di controlli sull’integrità del contenuto dell’header GPT di testa (CRC32 checksum) consentono un’immediata rilevazione di eventuali errori nell’intestazione e/o nella tabella delle partizioni.

 ## Formato delle partizioni
 Esistono diversi tipi di formato per le partizioni di un disco.

 In ambiente Linux il formato ext4 è il formato predefinito su Ubuntu. In alternativa possono essere utilizzati i file system ext3, ext2, ReiserFS, ZFS e Btrfs.

 In ambiente Windows i formati predefiniti sono NTFS e FAT32. È bene conoscere anche questi ultimi due, in quanto non è raro trovare un sistema Linux in dual boot con Windows. Per NTFS e FAT32 non è possibile da Ubuntu cambiare i permessi dei file. Nel caso si usufruisca del dual boot, è consigliato creare una partizione per l'archiviazione e scambio di dati fra i due sistemi in formato NTFS, più moderno di FAT32.

 ## Utilizzo delle partizioni

 EFI

 È richiesta dai Bios di nuova generazione UEFI. Si tratta di un'area di avvio in formato fat32 le cui dimensioni possono arrivare oltre i 500Mib. Nei computer in commercio è collocata a seconda dei casi:
 * nella prima partizione /dev/sda1;
 * nella seconda partizione /dev/sda2 se nella /dev/sda1 è presente la partizione nascosta di ripristino di Windows.

 grub_bios

 Si tratta di un area priva di formato con dimensioni variabili da 1 a 2 MB che deve essere contrassegnata dal flag grub_bios. Quest'area è utilizzata da Grub per la gestione del boot dei sistemi. L'omissione dell'area grub_bios può rappresentare un problema su installazioni con più sistemi

 Filesystem "/"
  file system comunemente indicato con il simbolo "/" è l'area che accoglie il sistema operativo in formato ext4 (vedere formati alternativi).
 Il filesystem può essere suddiviso in modo tale che ogni singola directory possa essere destinata ad una partizione a se stante. Particolarmente comune è il caso in cui la directory /home viene assegnata  a una partizione a se per fungere da partizone dati e preservare i dati personali e impostazioni dei software in successive reinstallazioni del sistema.

 swap
 Per swap si intende un'area di appoggio alla memoria RAM che utilizza un formato a se stante linux-swap. Può essere sostituita dal file di swap che, in assenza di una partizione di swap, verrà creato internamente al filesystem durante l'installazione del sistema.
 La creazione di un'area di swap può in alcuni casi risultare ancora utile, ad esempio nel caso si abbiano più sistemi installati sul medesimo disco e magari su partizioni poco capienti. In tal caso creare un'unica area sfruttabile dai vari sistemi può rappresentare un'ottimizzazione delle risorse.

## La funzionalità Secure Boot
Se attivata (lo è, di solito, in maniera predefinita su UEFI), s’incarica di prevenire il caricamento dei driver o dei loader per il sistema operativo che non sono firmati utilizzando una firma digitale valida e riconosciuta (non presente nel database delle firme conservate nel firmware della scheda madre).

Il Secure Boot mira in primis a bloccare malware che tentassero di prendere possesso del sistema nella base pre-boot ma potrebbe costituire un problema se si volesse installare una distribuzione Linux.

## UEFI e modalità legacy
UEFI consente, su richiesta dell’utente, di attivare la modalità legacy. Si tratta di una speciale modalità che consente di disabilitare tutte le funzionalità proprie di UEFI e ripristinare un BIOS “standard”.
La modalità legacy consente di permettere il corretto avvio di tutti quei sistemi operativi (ad esempio Windows 7) e quegli strumenti software che non supportano UEFI.