---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-16"

keywords: new features,updates to Natural Language Classifier,what's new

subcollection: natural-language-classifier

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Note sul rilascio
{: #release-notes}

Sono disponibili le seguenti nuove funzioni e modifiche per il servizio.
{: shortdesc}

## Funzioni beta
{: #beta}

{{site.data.keyword.IBM_notm}} rilascia servizi, funzioni e supporto lingua per una tua valutazione che sono classificati come beta. Queste funzioni potrebbero essere instabili, cambiare frequentemente e potrebbero essere sospese con breve preavviso. Inoltre, le funzioni beta potrebbero non fornire lo stesso livello di prestazioni o di compatibilità fornito generalmente dalle funzioni e non sono progettate per essere utilizzate in un ambiente di produzione. Le funzioni beta sono supportate solo su [IBM Developer Answers ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/answers/topics/natural-language-classifier.html){: new_window}.

## Modifiche
{: #changelog}

Sono disponibili le seguenti nuove funzioni e modifiche per il servizio.

### 25 gennaio 2019
{: #25jan2019}

**L'ubicazione di Francoforte supporta ora i dati di formazione con dati più grandi**

Le istanze del servizio {{site.data.keyword.nlclassifiershort}} ospitate in Francoforte possono ora essere preparate su serie di dati più grandi. Puoi includere fino a 20.000 record nei tuoi dati di formazione.

La dimensione dei dati più grandi è ora supportata in tutte le ubicazioni {{site.data.keyword.nlclassifiershort}}. Per ulteriori dettagli sui dati di preparazione, consulta [Preparazione dei dati](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data).

### 13 novembre 2018
{: #18November2018}

**Numero massimo di classi**

I dati di formazione supportano ora un massimo di 3.000 classi, sebbene un numero inferiore di classi può portare a prestazioni migliori. Per i dettagli, consulta [Preparazione dei dati](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#training-limits) e [Procedure consigliate per i classificatori](/docs/services/natural-language-classifier?topic=natural-language-classifier-best-practices-overview#training-guidelines).

### 9 novembre 2018
{: #9November2018}

**Nuova ubicazione di Tokyo**

Puoi ora creare delle istanze del servizio {{site.data.keyword.nlclassifiershort}} ospitate nell'ubicazione di Tokyo.

### 30 ottobre 2018
{: #30october2018}

Il 30 ottobre 2018, le ubicazioni Stati Uniti Sud e Germania sono passate all'utilizzo dell'autenticazione IAM (Identity and Access Management) basata sui token. {{site.data.keyword.nlclassifiershort}} ha migrato tutte le ubicazioni nelle seguenti date:

- Stati Uniti Sud (Dallas): 30 ottobre 2018
- Germania (Francoforte): 30 ottobre 2018
- Stati Uniti Est: 12 ottobre 2018

La migrazione all'autenticazione IAM riguarda le istanze nuove o esistenti in modo diverso:

- Con le *nuove* istanze del servizio che crei nelle ubicazioni e nelle date elencate precedentemente, esegui l'autenticazione all'API utilizzando IAM. Puoi passare un token di connessione in un'intestazione di autorizzazione o una chiave API. I token supportano le richieste autenticate senza l'integrazione di credenziali di servizio in ogni chiamata. Le chiavi API utilizzano l'autenticazione di base. 

    Quando utilizzi uno degli SDK {{site.data.keyword.watson}}, puoi passare la chiave API e lasciare che l'SDK gestisca il ciclo di vita dei token.
- Con le istanze del servizio *esistenti* che hai creato prima delle date indicate, continua ad eseguire l'autenticazione fornendo nome utente e password per l'istanza del servizio. Puoi utilizzare questi servizi fino ad ottobre 2019, dopodiché dovrai effettuare la migrazione a IAM.

Ulteriori informazioni:
- Per informazioni sul processo di autenticazione da utilizzare con la tua istanza del servizio, visualizza le credenziali del servizio facendo clic sull'istanza sul {{site.data.keyword.cloud_notm}} [Dashboard ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/dashboard/apps?watson){: new_window}.
- Per ulteriori informazioni ed esempi sugli SDK, consulta [Autenticazione ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier?language=java#authentication){: new_window} nella guida di riferimento API.
- Per ulteriori informazioni sull'utilizzo dei token IAM con i servizi Watson, consulta [Autenticazione con i token IAM](/docs/services/watson?topic=watson-iam#iam).
- Per ulteriori informazioni sull'utilizzo delle chiavi API IAM con i servizi Watson, consulta [Chiavi API del servizio IAM](/docs/services/watson?topic=watson-api-key-bp#api-key-bp).
- Per ulteriori informazioni sulla migrazione delle istanze Cloud Foundry, consulta [Migrazione di istanze del servizio Cloud Foundry a un gruppo di risorse](/docs/resources?topic=resources-migrate#migrate).

### 19 settembre 2018
{: #19september2018}

**È stata introdotta la limitazione alla velocità**

- Le chiamate API sono ora limitate a 1500 richieste al minuto per istanza del servizio. Se superi il limite, viene restituito il codice di stato HTTP `429 Too Many Requests`.

### 7 agosto 2018
{: #07august2018}

**È stata sostituita la strumentazione classica**

La strumentazione classica è stata disattivata a partire dal 7 agosto 2018 e sostituita da [{{site.data.keyword.DSX}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")][watson-studio-reg]{: new_window}.

Puoi migrare i dati di formazione per i classificatori creati all'esterno di {{site.data.keyword.DSX}} fino al 30 settembre 2018. Dopo la migrazione, puoi facilmente aggiornare i dati di formazione e creare un altro classificatore all'interno di {{site.data.keyword.DSX}}.

### 2 agosto 2018
{: #02august2018}

**Migra i tuoi dati di formazione a {{site.data.keyword.DSX}}**

Puoi ora migrare i dati di formazione per i classificatori creati all'esterno di {{site.data.keyword.DSX}}. Dopo la migrazione, puoi facilmente aggiornare i dati di formazione e creare un altro classificatore all'interno di {{site.data.keyword.DSX}}.

Puoi migrare i dati fino al 30 settembre 2018.

### 6 luglio 2018
{: #06july2018}

**Nuovo strumento beta disponibile: {{site.data.keyword.DSX}}**

{{site.data.keyword.DSX}} è il nuovo ambiente integrato che include una sostituzione per la precedente strumentazione {{site.data.keyword.nlclassifiershort}} classica. Per iniziare ad utilizzare {{site.data.keyword.DSX}}, fai clic su **Launch tool** da un dashboard dell'istanza del servizio {{site.data.keyword.nlclassifiershort}}. Per i dettagli, consulta [Gestione dei classificatori con {{site.data.keyword.DSX}}](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#studio).

{{site.data.keyword.DSX}} supporta non solo {{site.data.keyword.nlclassifiershort}} ma anche {{site.data.keyword.visualrecognitionshort}} e molti altri servizi e risorse {{site.data.keyword.cloud_notm}}. {{site.data.keyword.DSX}} fornisce un ambiente collaborativo nel cloud. Con {{site.data.keyword.DSX}}, gli sviluppatori, gli esperti in materia, i data scientist e altri possono creare e preparare {{site.data.keyword.nlclassifiershort}} e altri modelli IA. Puoi inoltre utilizzare {{site.data.keyword.DSX}} per verificare i tuoi classificatori.

Puoi utilizzare {{site.data.keyword.DSX}} con tutti i tuoi classificatori e istanze {{site.data.keyword.nlclassifiershort}} esistenti. La strumentazione classica rimane disponibile fino al 7 agosto 2018.

### 8 giugno 2018
{: #08june2018}

**Scarica i tuoi dati di formazione per il nuovo strumento**

La strumentazione classica {{site.data.keyword.nlclassifiershort}} esistente sarà disattivata il 31 luglio 2018. La sostituzione pianificata per la strumentazione è **{{site.data.keyword.DSX}}**, il nuovo ambiente integrato. [{{site.data.keyword.DSX}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")][watson-studio-reg]{: new_window} supporta già {{site.data.keyword.visualrecognitionshort}} e altri servizi e risorse {{site.data.keyword.cloud_notm}}.

Ci aspettiamo che tutti i tuoi classificatori esistenti saranno disponibili in {{site.data.keyword.DSX}}. Tuttavia, se vuoi assicurarti di poter ricreare i tuoi classificatori esistenti, scarica i dati di formazione dalla strumentazione classica prima del 31 luglio 2018.

Per quelli che utilizzano l'[API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier){: new_window} direttamente, non vi è alcun cambiamento con la migrazione dello strumento.

### 16 marzo 2018
{: #16march2018}

- **Classify multiple phrases**

    È disponibile un nuovo metodo **Classify multiple phrases** che supporta l'invio di fino a 30 frasi di testo in una richiesta. Il metodo `POST /v1/classifiers/{classifier_id}/classify_collection` supporta la classificazione delle frasi nelle stesse lingue del metodo originale, con l'eccezione del giapponese, che è una funzione beta.

    Per i dettagli sulla chiamata API, consulta il metodo **Classify multiple phrases** nella [Guida di riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}.

- **Preparazione con serie di dati più grandi**

    Puoi ora includere fino a 20.000 record nei tuoi dati di formazione. La preparazione del classificatore viene ora migliorata da IBM Deep Learning as a Service. Questa offerta è un'infrastruttura di formazione della rete neurale che utilizza un cluster elastico di GPU (graphics processing unit) per gestire le serie di dati più grandi. La dimensione massima dei dati di formazione rimane di 15.000 record per gli utenti nell'ubicazione di Francoforte o gli utenti con {{site.data.keyword.Bluemix_dedicated_notm}}.

### 10 luglio 2017
{: #10july2017}

**Lingue aggiuntive:** il servizio ora supporta il coreano in aggiunta a arabo, inglese, francese, tedesco, giapponese, italiano, portoghese e spagnolo. La lingua dei dati di formazione deve corrispondere alla lingua del testo che si intende classificare.

Per i dettagli sulle lingue, consulta [Utilizzo dei tuoi propri dati](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#languages). Per i dettagli sulla chiamata API, consulta il metodo `Create classifier` nella [Guida di riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}.

### 6 aprile 2016
{: #06april2016}

**Lingue aggiuntive:** il servizio ora supporta il tedesco in aggiunta a arabo, inglese, francese, giapponese, italiano, portoghese e spagnolo. La lingua dei dati di formazione deve corrispondere alla lingua del testo che si intende classificare.

### 29 febbraio 2016
{: #29february2016}

**Lingue aggiuntive:** il servizio ora supporta il giapponese in aggiunta a arabo, inglese, francese, italiano, portoghese e spagnolo.

### 7 dicembre 2015
{: #07december2015}

**Lingue aggiuntive:** il servizio ora supporta arabo, francese e italiano in aggiunta a inglese, portoghese e spagnolo.

### 16 novembre 2015
{: #16november2015}

**Lingue aggiuntive:** il servizio ora supporta le lingue portoghese e spagnolo in aggiunta all'inglese.
