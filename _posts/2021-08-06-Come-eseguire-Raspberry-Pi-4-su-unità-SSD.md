---
date: 2021-08-06
title: Come eseguire Raspberry Pi 4 su unità SSD?
categories: linux-generic
description: Avvio Raspberry Pi dall'unità SSD
type: Document
---


**Avvio Raspberry Pi dall'unità SSD**

In questo tutorial imparerai ad avviare da SSD su Raspberry Pi 4. Raspberry Pi 4 ha potenti porte USB 3.0 che ti consentono di ottenere le massime prestazioni quando esegui il suo sistema operativo su un'unità SSD esterna invece del metodo predefinito di avvio dalla scheda SD.

#### 1. Scarica Raspbian

Scarica l'ultimo file iso del sistema operativo Raspbian da [qui](https://www.raspberrypi.org/downloads/raspbian/). Sto lavorando con 2019-07-10-raspbian-buster.zip scaricato il 26 dicembre 2019. Estrai il file iso.

#### 2. Masterizza l'iso sia sulla scheda SD che sull'unità SSD

Scarica balenaEtcher per masterizzare l'immagine ISO sia sulla scheda SD che sull'unità SSD da [qui](https://www.balena.io/etcher/). Dopo aver sepolto il sistema operativo Raspbian sia sulla scheda SD che sull'unità SSD, inseriscili entrambi nel Raspberry Pi 4 e accendilo.

#### 3. Trova PARTUUID dell'unità SSD

Utilizzare il seguente comando per trovare il PARTUUID dell'unità SSD  

```
sudo lsblk -o PARTUUID,NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL
```
