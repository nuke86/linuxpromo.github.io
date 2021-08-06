---

date: 2021-08-06
title: Docker Container Networking - Esposizione delle porte
categories: programmazione
description: Networking con host, container docker multipli, porte espositive, comunicazione TCP/UDP
type: Document
---


**Networking con host, container docker multipli, porte espositive, comunicazione TCP/UDP**


Docker viene utilizzato per eseguire servizi di rete come server Web e database. Docker dispone di opzioni di rete per connettere i contenitori tra loro. È possibile inserire contenitori in reti private in cui ogni contenitore sulla rete privata può comunicare tra loro, ma sono isolati dal resto dei contenitori in esecuzione sul computer. Puoi anche esporre le porte di rete all'invio di dati in entrata e in uscita dal sistema. Tratteremo il networking docker con alcuni esempi.

* Esempio 1 - Invia dati dal contenitore al computer host specificando le porte interne ed esterne come viste dall'interno del contenitore e dall'esterno.
* Esempio 2 - Invia dati dal contenitore al computer host ma lascia che la finestra mobile scelga le porte dalle porte inutilizzate.
* Esempio 3 - Invia dati dal contenitore ad altri contenitori.
* Esempio 4 - Utilizzo di UDP per la comunicazione.

**Esempio 1** : creare un container docker e aprire le porte. Il server accetterà i dati da un client e poi li passerà a un altro client. Useremo il netcat (nc)comando linux per inviare dati da un client locale al server container che inoltrerà i dati a se stesso e successivamente li passerà a un altro client. netcat è un'utilità di rete per computer per lo spostamento di bit da un luogo a un altro tramite connessioni di rete tramite TCP o UDP. È un modo semplice per mostrare la rete senza dover avviare un server web.

La prima cosa da fare è creare il container docker e aprire le porte per la comunicazione. Apri una schermata del terminale e crea un contenitore usando il seguente comando:

```
docker run --rm -ti -p 45678:45678 -p 45679:45679 --name serverOne ubuntu:14.04 bash
```

Questo comando apre le porte 45678 e 45679, il nome del contenitore è serverOne, utilizza Ubuntu 14.04 per questo esempio. Questo comando aprirà la shell bash del contenitore. In questa shell bash esegui il seguente comando per far passare i dati nel nostro sistema su una porta e poi sputare su un'altra porta.

```
nc -lp 455678 | nc -lp 45679
```

Quindi, apri altre due schermate del terminale. Nella prima schermata, esegui:

```
nc localhost 45678
```

Nella seconda schermata del terminale eseguire:

```
nc localhost 45679
```

L'immagine sotto mostra la configurazione.
![](https://1.bp.blogspot.com/-FNbfn4gZ_E4/XsFT6XSGKkI/AAAAAAAAJek/l0MLptLgcIoiPVAXGZ2GsdAk6g9UVQAVACLcBGAsYHQ/s1600/docker-networking.png)


Ora possiamo inviare i dati dal client 1 al server e il server passerà i dati al client 2

![](https://3.bp.blogspot.com/-u9v6X_sKPHE/XsFUlg6El7I/AAAAAAAAJes/E-huSfAYpckRUQgWPr--LLGhsrwdUwX7QCLcBGAsYHQ/s1600/docker-networking-2.png)

A questo punto puoi cancellare tutti i terminali e chiudere il terminale mobile.

**Esempio 2**: Faremo lo stesso dell'esempio 1 ma lasceremo che la finestra mobile scelga dalle porte inutilizzate. Apri tre schermate del terminale.

Esegui il seguente comando per avviare il contenitore (server) nel primo terminale:

```
docker run --rm -ti -p 45678 -p 45679 --name serverOne ubuntu:14.04 bash
```

Nota, non abbiamo specificato la porta esterna. Avvia il netcat per l'ascolto sulle porte:

```
nc -lp 45678 | nc -lp 45679
```

Esegui i seguenti comandi per vedere le porte esterne assegnate da docker:

```
docker port serverOne
```

**serverOne** è il nome del container docker che abbiamo creato in precedenza. Emetterà le porte esterne.

```
45678/tcp -> 0.0.0.0:32769
45679/tcp -> 0.0.0.0:32768
```

Eseguire il seguente comando nel secondo terminale per avviare netcat e connettersi con il server:

```
nc localhost 32769
```

Eseguire il seguente comando nel terzo terminale per avviare netcat e connettersi con il server:

```
nc localhost 32768
```

Ora i client possono parlare tra loro attraverso il server. Vedere l'immagine sotto delle tre schermate del terminale.

![](https://2.bp.blogspot.com/-foqpgxClKhk/XsFpSnqzArI/AAAAAAAAJfI/LyqgGKLjP2smt98h5QPesCJ3xRyjTMv6ACLcBGAsYHQ/s1600/docket-networking-5.png)

**Esempio 3**: In questo esempio, faremo lo stesso dell'ultimo esempio, ma anche i nostri clienti saranno contenitori. Questo è utile quando il tuo computer locale non ha netcat, quindi devi eseguire netcat dall'interno del contenitore.

Avremo tre terminali anche in questo esempio, ciascuno in esecuzione in un contenitore. Il primo contenitore è il server e gli altri due sono i client.

Eseguire il comando seguente per avviare il primo contenitore (server) nel primo terminale:

```
docker run --rm -ti -p 45678:45678 -p 45679:45679 --name serverOne ubuntu:14.04 bash
```
Avviare netcat per l'ascolto sulle porte:

```
nc -lp 45678 | nc -lp 45679
```


Eseguire il comando seguente per avviare il secondo contenitore (client 1) nel secondo terminale e avviare netcat:

```
docker run --rm -ti ubuntu:14.04 bash
```

Avviare netcat per fare riferimento al computer host:

```
nc host.docker.internal 45678
```


Eseguire il comando seguente per avviare il terzo contenitore (client 2) nel terzo terminale:

```
docker run --rm -ti ubuntu:14.04 bash
```

Avviare netcat per fare riferimento al computer host:

```
nc host.docker.internal 45679
```

![](https://4.bp.blogspot.com/-WviDClPuzzY/XsFjpH9Q3II/AAAAAAAAJe8/-qG_Y2pWz-UhNS71AVzzVy6YVUUAesE7wCLcBGAsYHQ/s1600/docker-networking-4.png)

**Esempio 4**: In questo esempio, utilizzeremo la comunicazione UDP invece della comunicazione TCP predefinita. Useremo due schermate di terminale in questo esempio per semplificarci. Il client invierà i dati al server tramite UDP.

Creare il server utilizzando il seguente comando:

```
docker run --rm -ti -p 45678/udp --name serverOne ubuntu:14.04 bash
```

Avviso udpdopo il numero di porta. Eseguire il comando seguente nel contenitore per la comunicazione UDP:

```
nc -ulp 45678
```

Esegui il seguente comando nel secondo terminale per visualizzare la porta esterna assegnata dalla finestra mobile:

```
docker port serverOne
```

Verrà visualizzato:

```
45678/udp -> 0.0.0.0:32768
```

Esegui il seguente comando per iniziare a comunicare su UDP:

```
nc -u localhost 32768
```

Ora il client può inviare un messaggio al server.

![](https://4.bp.blogspot.com/-ur5BzjDBufE/XsGDKnE0E9I/AAAAAAAAJfU/IHjpjFOs4skeHG_ilqCqeRcwy0Ckn4SrwCLcBGAsYHQ/s1600/docker-networking-6.png)

