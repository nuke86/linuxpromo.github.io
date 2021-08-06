---

date: 2021-08-06
title: Come sincronizzare file e cartelle su Linux?
categories: linux-generic
description: Linux sincronizza due directory usando rsync e inotify
type: Document
---


**Linux sincronizza due directory usando rsync e inotify**

Linux dispone di potenti strumenti che consentono di sincronizzare file o cartelle da una directory di origine a un'altra directory di destinazione.

#### 1. Installa gli strumenti inotify

```
sudo apt-get install inotify-tools
```

Maggiori informazioni possono essere trovate sul loro wiki: https://github.com/rvoicilas/inotify-tools/wiki

#### 2. Installa rsync

```
sudo apt-get install ssh rsync
```

#### 3. Crea un nuovo file di script bash chiamato sync.sh

```
nano sync.sh
```

#### 4. Incolla il codice seguente nel file sync.sh

```
#!/bin/sh  
while inotifywait -r -e modify,create,delete,move /home/amrit/rsync-test/source_folder; do  
rsync -avz /home/amrit/rsync-test/source_folder /home/amrit/rsync-test/destination_folder --delete  
done
```

È necessario modificare le posizioni delle cartelle di origine e di destinazione evidenziate nel file di script della shell sopra in modo che corrispondano alla propria configurazione.

#### 5. Rendi eseguibile lo script della shell

```
chmod +x sync.sh
```

#### 6. Esegui lo script della shell

```
./sync.sh
```

Ecco fatto, hai finito! A questo punto, se si apportano modifiche alla directory di origine, verranno applicate anche alla directory di destinazione.
