---
layout: default
title: "Scarica file di Google Drive di grandi dimensioni con Wget nel terminale"
tags: linux-generic
---

## Scarica file di Google Drive di grandi dimensioni con Wget nel terminale


**Questo comando ti consentirà di scaricare file da Google Drive utilizzando solo il tuo terminale Linux.**


Recentemente ho lavorato con Google Cloud Platform e ho utilizzato le macchine virtuali per lavorare su un progetto di data science. Mi sono imbattuto in un set di dati che devo scaricare da Google Drive nella mia macchina virtuale. Google non ti fornisce un link per il download diretto. Mi sono imbattuto in questo comando intelligente che mi ha permesso di scaricare il file dal mio terminale e voglio condividerlo con tutti voi.

Avremo bisogno del link condivisibile di Google Drive. Esempio di un link condivisibile di Google Drive:
https://drive.google.com/file/d/13oki4nUEp3z_6Sl4NovhldB90HZ1w1c-/view?usp=sharing

* Identificare FILEID nel link sopra. FILEID = 13oki4nUEp3z_6Sl4NovhldB90HZ1w1c-
* Identificare FILENAME nel link sopra. FILENAME = Linemod_and_Occlusion.zip

Sostituisci FILEID e FILENAME nel comando seguente:

```
wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=FILEID' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=FILEID" -O FILENAME && rm -rf /tmp/cookies.txt
```

Dopo aver sostituito FILEID e FILENAME, il comando sarà simile a:

```
wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=13oki4nUEp3z_6Sl4NovhldB90HZ1w1c-' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=13oki4nUEp3z_6Sl4NovhldB90HZ1w1c-" -O Linemod_and_Occlusion.zip && rm -rf /tmp/cookies.txt
```

Infine, questo scaricherà il file Google Drive sul tuo computer utilizzando solo lo schermo del terminale del tuo computer Linux.