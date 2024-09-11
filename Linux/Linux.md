
### Introduzione

Un sistema operativo è composto da:
- Un kernel, programma che gestisce l’hardware al livello più basso e si occupa ad esempio di interagire con memoria, CPU, periferiche.
- Delle applicazioni utente, che si appoggiano al kernel per interagire con le varie
funzionalità (ad esempio, utilizzare memoria e/o mostrare un’immagine a video).

Esempi: 
- Windows `e composto del kernel NT e l’interfaccia grafica, 
- Mac OS X ha un kernel di nome XNU, e sistemi come Ubuntu
- Distribuzioni Linux utilizzano il
Kernel di Linux

Linux è nato, rispetto a sistemi commerciali come Windows e MacOS X, come sistema free opensource.

Linus Torvalds
Tutto `e iniziato da un’email del 1991:
![alt text](../Images/Mail_nascita_linux.JPG)

Nel 1991, al progetto GNU avevano un compilatore, delle applicazioni utente, ma gli
mancava un kernel. Quando Linux `e nato, era solamente un kernel; da qui sono nati i sistemi GNU/Linux.

Poco dopo il primo rilascio di Linux, sono nate le prime distribuzioni Linux, come Debian
e Slackware.
Ubuntu, una delle distribuzioni oggi più utilizzatanei personal computer, è basata su
Debian.

I computer hanno molte interfacce attraverso cui dar loro comandi.
Per usare al massimo gli strumenti che il computer  offre, dobbiamo usare la “vecchia” interfaccia a riga di comando, la shell.
La shell non è che un programma come tutti gli altri.
Attraverso la shell è possibile compiere diverse operazioni come: interagire con i file, avviare programmi, installare e gestire i pacchetti. 

### Un pò di storia
I sistemi operativi che esistevano prima di Linux e di Unix (ricordiamo che Linux e' un clone di Unix) possedevano già degli interpreti di comandi al loro interno, ma tali interpreti avevano un difetto: non erano modificabili. Quando Ken Thompson e Dennis Ritchie cominciarono a scrivere Unix, decisero di creare una interfaccia utente modificabile a seconda delle esigenze che si potevano presentare di volta in volta. Cio' che venne fuori fu un tipo di shell programmabile, contenente istruzioni simili a quelle del linguaggio C. Questo non e' un caso visto che la prima versione di Unix venne scritta in linguaggio assembler, ma fu successivamente riscritta in linguaggio C (ricordiamo che Dennis Ritchie e' insieme a Brian Kerninghan l'inventore del linguaggio C). L'interprete dei comandi creato sotto Unix venne chiamato shell. Una delle prime shell venne creata agli inizi degli anni 70 presso i Bell Laboratories AT&T ad opera di Steven R. Bourne e venne chiamata appunto Bourne shell (sh). Verso la fine degli anni 70 presso l'università di Berkley venne creata la C shell (csh) allo scopo di estendere la shell Bourne e renderla più simile al linguaggio di programmazione C. Successivamente vennero sviluppate altre shell, come la Korn shell (ksh) e la TC shell (tcsh). A causa dei problemi di copyright, l'organizzazione GNU decise di sviluppare una shell completamente libera da restrizioni e nacque cosi' la shell BASH, cioè Bourne Again SHell. Esistono molteplici versioni di shell, la shell ash, la shell csh, la shell ksh, la shell pdksh, la shell tcsh, la shell zsh ed altre ancora, ma la shell BASH e' senza dubbio la piu' famosa ed usata in tutti i sistemi Linux. La shell BASH e' conforme allo standard POSIX. Posix sta per Portable Operating System Interface for uniX, cioè interfaccia standard per il sistema operativo Unix e si tratta di uno standard creato verso la fine degli anni 80 allo scopo di uniformare le varie versioni di Unix. Successivamente, ad opera del gruppo IEEE (Institute of Electrical and Electronics Engineers, cioe' istituto degli ingegneri elettrotecnici ed elettronici) lo standard POSIX venne adottato anche da altri sistemi operativi non Unix come VMS, MVS, NT etc.


### Il kernel 
è il componente centrale di ogni sistema operativo.  Fa da ponte tra le componenti hardware di un computer – come processore, RAM e hard disk – e i programmi in esecuzione sul computer stesso.
Un sistema GNU LInux  è un kernel che inizializza l’hardware e fornisce le primitive per usarlo. 

Il kernel ha il pieno controllo su tutto nel sistema. Ogni operazione di hardware e software è gestita e amministrata dal kernel. Funziona come un ponte tra le applicazioni e l'elaborazione dei dati effettuata a livello hardware. 
Risiede sempre nella memoria del computer.. Viene caricato per primo all'avvio del sistema (dopo il bootloader). Una volta caricato, gestisce i restanti avviamenti. 
Gestisce inoltre le richieste di memoria, periferiche e I/O dal software. 
Un kernel viene mantenuto e solitamente caricato in uno spazio di memoria separato, noto come spazio kernel protetto. È protetto dall'accesso da parte di programmi applicativi o parti meno importanti del sistema operativo.
Altri programmi applicativi come browser, elaboratori di testi, lettori audio e video utilizzano uno spazio di memoria separato noto come spazio utente.Grazie a questi due spazi separati, i dati dell'utente e quelli del kernel non interferiscono tra loro e non causano alcuna instabilità e lentezza.

![alt text](../Images/Kernel.JPG)

### la Riga di Comando
Shell, terminale e riga di comando sono termini che indicano in maniera equivalente un dispositivo a interfaccia testuale. Può servire a svolgere gran parte delle mansioni in un sistema operativo: muoversi attraverso il file system per creare, cancellare o rinominare file, scaricare, installare o rimuovere programmi, per configurare l'hardware, per creare script e molto altro.

Tante delle azioni sopra elencate, come noto alla maggior parte degli utenti, possono essere svolte tramite programmi a interfaccia grafica. La riga di comando può essere utile qualora sussistano dei malfunzionamenti di tali programmi e si vogliano tracciare eventuali bug, nel caso non esistano programmi a interfaccia grafica o semplicemente perché l'utente ritiene comodo usarla.

### BASH   “Bourne Again Shell”
Non esiste una sola shell, ma nella maggior parte delle distribuzione viene utilizzata in maniera predefinita la shell bash.
Bash è sviluppata nell'ambito del progetto GNU come alternativa libera di Bourne shell. Il nome è un calembour poiché Bourne again (un'altra Bourne [shell]) è omofono a born again (rinascita).
Bash è una "Unix shell", vale a dire un'interfaccia a linea (o riga) di comando che permette l'interazione con sistemi operativi derivati da Unix. È disponibile su gran parte dei sistemi operativi moderni di questo tipo, essendo la shell predefinita di molte distribuzioni GNU/Linux, nonché di Mac OS X.

### Leggere la riga di comando

Quando avviamo il terminale vedremo una riga come questa:<br>

mario@mario-desktop:~$

L'utente mario, all'interno del computer mario-desktop, si trova attualmente nella propria Home, cioè /home/mario/, indicata con il simbolo ~ chiamato Tilde.

È attiva la modalità utente, indicata dal simbolo $.<br>Esiste anche una modalità amministratore, attivabile con il comando sudo -s e caratterizzata dal simbolo #.<br> 
[Amministratore di sistema](https://wiki.ubuntu-it.org/AmministrazioneSistema/PrivilegiDiAmministrazione/Sudo)


Il file system, inteso come la directory che contiene tutte le altre, è rappresentato dal simbolo / chiamato root (da non confondere con la cartella /root la Home dell'amministratore)

## la directory home

È la directory che contiene tutte le Home degli utenti presenti nel sistema. Ogni home porta il nome dell'utente, nel nostro caso mario.

A disposizione di ogni utente all'interno della cartella /home, ci sarà quindi una cartella con il suo stesso nome, nel nostro esempio mario. Il suo percorso completo sarà /home/mario, che nel terminale può essere sinteticamente rappresentato dal simbolo ~ chiamato tilde.
Tale cartella riveste una grande importanza all'interno del sistema, dato che al suo interno sotto forma di file nascosti, sono memorizzati tutti i file di configurazione dei programmi.<br>
Per esempio, nella sottocartella ~/.mozilla vengono memorizzati i dati riguardanti il browser Firefox: segnalibri, estensioni, impostazioni menu, ecc.<br>
Per nascondere un file è sufficiente preporre un punto prima del nome. Ad es. per nascondere il file script.sh è sufficiente rinominarlo in .script.sh.


Per avere la conferma di essere nella cartella /home/mario/ è utile eseguire il comando pwd, il quale stamperà a schermo il percorso corrente.<br>
Invece digitando il comando ls si ottiene l'elenco dei file presenti nella cartella /home/mario/.

Alla destra della riga, dopo $ troveremo<br>
 #### 1.Comando  
 #### 2.Opzioni  
 #### 3.Argmoenti


 1. Ogni comando è il nome di un programma, che viene ricercato in alcune cartelle pre-determinate. Solitamente queste sono 
 * /bin, 
 * /usr/bin, 
 * e talvolta /usr/local/bin.<br>In quest'ultima cartella è usuale installare nuovi comandi creati dall'utente, oppure installati come applicazioni di terze parti.

 2. Ogni comando può accettare delle opzioni o flag, ovvero una sequenza di caratteri successive al nome del comando, che si possono utilizzare per specificare delle azioni che il comando può effettuare.<br> Tipicamente i flag si distinguono in quelli brevi, identificati da una linea ed una sola lettera, e quelli lunghi, che iniziano con due linee seguita poi da parola chiave più lunga. Le opzioni si possono combinare tra loro cosicché, invece di dover scrivere -r -v, possiamo utilizzare -rv.

 3. Ogni comando può essere eseguito su un argomento inteso come oggetto su cui eseguire il comando.





### I Percorsi
Per agire sui file occorre indicare sempre i percorsi completi oppure spostarsi all'interno della cartella in cui si trova il file interessato. 

Supponiamo di voler rimuovere attraverso il comando rm il file canzone.ogg, memorizzato in /home/mario/Scrivania. A tale scopo è possibile digitare il seguente comando, nel quale viene specificato il percorso completo del file:

rm /home/mario/Scrivania/canzone.ogg

In alternativa è possibile spostarsi nella cartella Scrivania per poi procedere alla rimozione del file con i seguenti comandi:

cd /home/mario/Scrivania<br>
rm canzone.ogg

Alcuni comandi non necessitano della digitazione di alcun percorso. Ad esempio, per installare un pacchetto con apt-get è sufficiente specificarne solo il nome. La sintassi del comando sarà dunque simile alla seguente:

sudo apt-get install nome_pacchetto

[Guida Ubuntu](https://wiki.ubuntu-it.org/AmministrazioneSistema)








