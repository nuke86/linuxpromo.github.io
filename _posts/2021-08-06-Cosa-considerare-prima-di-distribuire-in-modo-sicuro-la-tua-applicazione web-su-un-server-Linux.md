---
date: 2021-08-06
title: Cosa considerare prima di distribuire in modo sicuro la tua applicazione web su un server Linux?
categories: sicurezza
description: Scopri cosa dovresti considerare sul tuo server Linux prima di distribuire la tua applicazione web su un provider di servizi cloud per mantenere la tua applicazione e i tuoi dati al sicuro
type: Document
---


**Scopri cosa dovresti considerare sul tuo server Linux prima di distribuire la tua applicazione web su un provider di servizi cloud per mantenere la tua applicazione e i tuoi dati al sicuro**

Uno degli aspetti più importanti su cui riflettere a fondo prima di distribuire la tua applicazione nel mondo è la sicurezza del tuo server. Vuoi mantenere i tuoi dati e il codice sorgente al sicuro. Le violazioni dei dati possono costare milioni di dollari alle aziende. Un esempio recente è la violazione dei dati di Facebook Cambridge Analytica all'inizio del 2018, quando milioni di dati degli utenti di Facebook sono stati utilizzati per pubblicità politica senza il loro consenso.

Questo articolo è destinato alle persone che non conoscono la distribuzione di applicazioni sul server Linux, dove raccolgono dati dagli utenti e li memorizzano in un database. Il tuo obiettivo è mantenere i dati al sicuro.

1.  Considera la protezione della tua rete. Dovresti configurare il tuo firewall per consentire solo le richieste di traffico di cui hai bisogno e negare tutto il resto. Uno dei modi più semplici per configurare il firewall è utilizzare **UFW o Uncomplicated Firewall**. Per impostazione predefinita, UFV è installato su Ubuntu e nega le connessioni in entrata e consente le connessioni in uscita. È necessario creare regole che consentano esplicitamente connessioni in entrata legittime come SSH o HTTPS.
  
3.  Utilizza la rete di distribuzione dei contenuti (CDN) di **Cloudflare** per evitare ritardi nel caricamento del contenuto della pagina Web e impedire che richieste dannose, come attacchi DDoS, raggiungano il tuo server.
  
5.  Usa **Nginx** sul **server** web **Apache** . _"NGINX è un server Web ad alte prestazioni, altamente scalabile e altamente disponibile, un server proxy inverso e un acceleratore Web (che combina le funzionalità di un bilanciatore del carico HTTP, cache dei contenuti e altro)."_ Nginx consente più utenti connessi per server, un migliore utilizzo della larghezza di banda, meno CPU e RAM consumate.
  
7.  Non distribuire l'applicazione come utente root. È necessario prima disabilitare l'accesso dell'utente root utilizzando una password e assicurarsi di abilitare l'accesso basato su chiave pubblica/privata. L'applicazione deve essere sempre ospitata su un altro account utente con meno privilegi di un utente root. In questo modo, se nella tua applicazione è presente un codice non sicuro che potrebbe consentire a un hacker di accedere all'account del server in cui è ospitata l'app, l'hacker non otterrà l'accesso root perché l'app non esegue l'account utente root.

Questi erano alcuni dei suggerimenti che seguo prima di distribuire qualsiasi applicazione web. Se hai altri suggerimenti, condividili con me.
