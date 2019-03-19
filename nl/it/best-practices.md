---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-06"

keywords: language support,supported languages,best practices,guidelines

subcollection: natural-language-classifier

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}

# Procedure consigliate per i classificatori
{: #best-practices-overview}

Seguendo alcune linee guida e utilizzando alcuni modelli di progettazione, puoi fornire un'esperienza ottimale ai tuoi utenti e assicurarti che la tua applicazione possa gestire quello che desideri classificare.

## Numero di classificatori
{: #classifier-limits}

Ogni istanza del servizio {{site.data.keyword.nlclassifiershort}} può avere fino a 8 classificatori, ognuno con un ID classificatore univoco. Per supportare più di 8 classificatori, crea un'altra istanza di {{site.data.keyword.nlclassifiershort}}. Puoi creare un'istanza del servizio dalla pagina {{site.data.keyword.watson}} console [Browse Services ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/developer/watson/services){: new_window}.

## Classify Multiple Phrases
{: #best-practices-multiple}

Utilizza il metodo **Classify a phrase** per classificare una sola stringa di testo. Con il metodo **Classify multiple phrases**, puoi inviare fino a 30 frasi di testo in una sola richiesta. Per i dettagli, consulta [API reference ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}.

## Lingue
{: #language-support}

Sebbene la lingua predefinita sia l'inglese, puoi specificare la lingua dei dati di formazione quando crei il classificatore. La lingua dei dati di formazione deve corrispondere alla lingua del testo che si intende classificare. Per i dettagli, consulta [API reference ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier#create-classifier){:new_window}.

Il classificatore supporta inglese (en), arabo (ar), francese (fr), tedesco (de), italiano (it), giapponese (ja), coreano (ko), portoghese (brasiliano) (pt) e spagnolo (es).

La classificazione del testo in giapponese con il metodo **Classify multiple phrases** è una funzione beta.
{: note}

## Linee guida per una corretta preparazione
{: #training-guidelines}

Le seguenti linee guida non sono applicate dall'API. Tuttavia, il classificatore tende a funzionare meglio quando i dati di formazione le applicano:

- Limita la lunghezza del testo di input a meno di 60 parole.
- Limita il numero di classi a diverse centinaia. Il supporto per un numero maggiore di classi potrebbe venire incluso in versioni successive del servizio.
- Assicurati che ogni classe corrisponda ad almeno 5 - 10 record quando ogni record di testo ha una sola classe. Questo numero fornisce abbastanza preparazione a tale classe.
- Valuta il bisogno di più classi. Due motivi comuni portano più classi:
    - Quando il testo è vago, l'identificazione di una sola classe non è sempre è chiara.
    - Quando gli esperti interpretano il testo in modi differenti, più classi supportano tali interpretazioni.

    Tuttavia, se molti testi nei tuoi dati di formazione includono più classi o se alcuni testi hanno più di tre classi, potresti dover affinare le classi. Ad esempio, controlla se le classi cono gerarchiche. Se sono gerarchiche, includi il nodo foglia come classe.
- Includi i termini uniti da trattino standard quando fanno parte dei dati di formazione (`back-to-back` o ` part-time job`).

    Tuttavia, non collegare parole adiacenti per creare nuovi termini non presenti nella lingua dei dati di formazione. Ad esempio, invece di definire `dish-ran-away` o `with_the_spoon`, definisci le frasi rilevanti come parole separate (`dish ran away` e `with the spoon`) con la classe appropriata.

## Messa a punto dei dati di formazione
{: #best-practices-training-data}

L'apprendimento automatico descrive un processo di apprendimento di alcune proprietà da una serie di dati e le applica ai nuovi dati. Il servizio {{site.data.keyword.nlclassifiershort}} segue questo processo. È preparato per collegare le classi predefinite ai testi di esempio e quindi ad applicare queste classi ai nuovi input.

Per cui, il classificatore preparato è buono soltanto quanto i dati di formazione. Ogni valore di testo nei dati deve rappresentare i tipi di testo che ti aspetti il classificatore preveda. Ogni classe che prevedi sia restituita deve inoltre essere presente nei dati di formazione e le classi associate ad ogni testo devono essere corrette.

Ad esempio, quando i testi nei tuoi dati di formazione sono domande, utilizza le domande rappresentative e tipiche dei tuoi utenti. Potresti raccogliere questi testi dai dati utente attuali o disporre di persone che sono esperte nel tuo campo per creare tali testi.

Questa natura accurata e rappresentativa dei dati è importante perché ti guida attraverso tutti i processi e i risultati del classificatore. In aggiunta, più record includi nei dati di formazione, maggiore è l'opportunità del classificatore di trovare una corrispondenza.

## Risorse aggiuntive
{: #best-practices-next-steps}

Consulta ulteriori [Best practices and design patterns ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/assets-watson/pdf/Watson-NLC-Links-Best-Practices-Design-Patterns.pdf){: new_window} per {{site.data.keyword.nlclassifiershort}}.
