SSH è l’acronimo di Secure Socket Shell. Il protocollo è stato creato nel 1995 da un ricercatore universitario finlandese. La seconda versione è stata creata 10 anni dopo e ad oggi non presenta vulnerabilità.

Questo protocollo consente agli amministratori di sistema di accedere in modo sicuro a un computer remoto. In quanto interprete di comandi permette agli amministratori di sistema di impartire comandi e avviare applicazioni.

In pratica questo protocollo ci permette di stabilire una sessione remota con un altro computer usando un’interfaccia a riga di comando.

Tramite SSH impartiamo dei comandi al server usando il linguaggio Shell Scripting.
<br>Questi script Shell sono eseguiti da degli interpreti del kernel di linux. L’interprete più comune è bash, ma ne esistono altri come csh e zsh.

È possibile fare tutto tramite bash. Installare applicazioni, aggiornarle, rimuoverle, controllare la configurazione, verificare quali processi sono attivi, ecc. In pratica un sistema linux può essere controllato interamente da linea di comando, e quindi tramite SSH.

## Connessione SSH
Per connetterci con SSH ad un server remoto ci basta il terminale di Linux o di Mac OSX, se usi Windows sarà necessario un client SSH come putty.

I dati necessari alla connessione sono:

1. Indirizzo IP del server.
2. Nome utente (può essere root o un altro nome utente).
3. Porta (di solito è la 22, nei nostri servizi usiamo la 2299).
4. Password o chiave asimmetrica


## Creare una chiave asimmetrica

La connessione con chiave è il metodo più sicuro per connettersi a un server.

Con questo sistema abbiamo due chiavi, una pubblica e una privata, che servono per creare un sistema di cifratura asimmetrico. Con questa cifratura i messaggi sono cifrati e decifrati con chiavi diverse.

Come dice il nome, le chiavi private sono segrete e mantenute soltanto dal proprietario e hanno una password. Queste chiavi sono usate per provare la propria identità.

Le chiavi pubbliche sono appunto pubbliche, e vengono distribuite su tutti i server con i quali vuoi comunicare in modo sicuro.


Apriamo il terminale e generiamo le chiavi:

ssh-keygen -t ed25519 -a 150

Salviamo le chiavi su una cartella

Inseriamo una passphrase,

Copia la chiave pubblica sul server usando ssh-copy-id, la chiave viene salvata in ~/.ssh/authorized_keys

Connettersi al server<br>
ssh user@123.123.123.123 -p 2299

Disabilita l’autenticazione con password al server

Cambiare la porta ssh

riavviare il server

