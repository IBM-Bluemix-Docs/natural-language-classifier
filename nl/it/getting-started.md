---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-06"

keywords: training data,examples,Natural Language Classifier,getting started,sample code


subcollection: natural-language-classifier

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:curl: .ph data-hd-programlang='curl'}
{:go: .ph data-hd-programlang='go'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}

# Esercitazione introduttiva 
{: #natural-language-classifier}

{{site.data.keyword.nlclassifierfull}} può aiutare la tua applicazione a comprendere la lingua di brevi testi e fare delle previsioni su come gestirli. Un classificatore fornisce informazioni sui dati di esempio e può restituire le informazioni per i testi su cui non è preparato. Puoi creare e preparare questo classificatore in meno di 15 minuti.
{:shortdesc}

Se preferisci utilizzare un'interfaccia grafica, utilizza {{site.data.keyword.DSX}}. [Avvia lo strumento ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://dataplatform.cloud.ibm.com/registration/stepone?context=wdp){: new_window} e segui [Building a classifier ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/nlc-create.html?audience=wdp&context=analytics){: new_window} nella documentazione.
{: tip}

## Prima di cominciare 
{: #prerequisites}

- {: hide-dashboard} Crea un'istanza del servizio: 
    1.  Vai alla pagina [{{site.data.keyword.nlclassifiershort}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/catalog/services/natural-language-classifier){: new_window} nel catalogo.
    1.  Registrati per un account {{site.data.keyword.Bluemix_notm}} gratuito o accedi.
    1.  Fai clic su **Crea**. 
- {: hide-dashboard} Copia le credenziali per autenticarti con la tua istanza del servizio: 
    1.  Nella pagina **Gestisci**, fai clic su **Mostra credenziali**.
    1.  Copia i valori `Chiave API` e `URL`.
- {: curl} Assicurati di disporre del comando `curl`.
    - Verifica se `curl` è installato. Immetti il seguente comando nella riga di comando. Se l'output elenca la versione `curl` con il supporto SSL, sei pronto per l'esercitazione.

        ```bash
        curl -V
        ```
        {: pre}

    - Se necessario, installa una versione con SSL abilitato da [curl.haxx.se ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://curl.haxx.se/){: new_window}. Aggiungi l'ubicazione del file alle tue variabili di ambiente PATH se vuoi eseguire `curl` da qualsiasi ubicazione della riga di comando.
- {:go} Installa [Go SDK ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/watson-developer-cloud/go-sdk){: new_window}.

    ```go
    go get -u github.com/watson-developer-cloud/go-sdk/...
    ```
    {: go}
    {: pre}

- {: java} Installa [Java SDK ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/watson-developer-cloud/java-sdk){: new_window}
    - {: java} Maven

        ```java
        <dependency>
          <groupId>com.ibm.watson.developer_cloud</groupId>
          <artifactId>java-sdk</artifactId>
          <version>{version}</version>
        </dependency>
        ```
        {: codeblock}

    - {: java} Gradle

        ```bash
        compile 'com.ibm.watson.developer_cloud:java-sdk:{version}'
        ```
        {:pre}

- {: javascript}Installa [Node SDK ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/watson-developer-cloud/node-sdk){: new_window}

    ```bash
    npm install --save watson-developer-cloud
    ```
- {: python} Installa [Python SDK ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/watson-developer-cloud/python-sdk){: new_window}

    ```bash
    pip install --upgrade watson-developer-cloud
    ```
- {: ruby} Installa [Ruby SDK ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/watson-developer-cloud/ruby-sdk){: new_window}

    ```bash
    gem install ibm_watson
    ```

Il seguente video ti guida attraverso questa esercitazione.
{: #video}

<iframe class="embed-responsive-item" id="youtubeplayer" title="Video della procedura dell'esercitazione introduttiva" type="text/html" width="560" height="315" src="https://www.youtube.com/embed/SUj826ybCdU?rel=0" webkitallowfullscreen mozallowfullscreen allowfullscreen gesture="media" allow="encrypted-media"></iframe>

## Passo 1: crea e prepara un classificatore
{: #create-train}

Il classificatore apprende dagli esempi prima di poter restituire informazioni per testi che non aveva visto precedentemente. I dati
di esempio sono indicati come "dati di formazione". Carichi i dati di formazione quando crei un classificatore.

1.  Scarica i due file di esempio:
    - Il <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a> è lo stesso di quello utilizzato con la [demo ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://natural-language-classifier-demo.ng.bluemix.net/){:new_window}. Il file è in un formato CSV in due colonne. La prima colonna è l'input di testo. La seconda colonna è la classe per tale testo: temperatura o condizione. Visualizza il file per vedere le voci.
    - Il file <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/metadata.json" download="metadata.json">metadata.json</a> specifica la lingua dei dati (`en`) e include un nome per identificare il classificatore.
1.  Immetti il seguente comando per richiamare il metodo **Create classifier**, che carica i dati di formazione e crea un classificatore di lingua inglese con il nome, "TutorialClassifier":
    - {: hide-dashboard} Sostituisci `{apikey}` e `{url}` con le credenziali che hai copiato nei prerequisiti.
    - Modifica l'ubicazione di `training_data` e `training_metadata` in modo che puntino a dove hai salvato i due file di esempio.

    ```bash
    curl -i -u "apikey:{apikey}"{: apikey} \
    -F training_data=@weather_data_train.csv \
    -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" \
    "{url}/v1/classifiers"{: url}
    ```
    {: pre}
    {: curl}

    Utenti Windows: sostituire la barra rovesciata (``\`) alla fine di ogni riga con un accento circonflesso (``^`). Assicurarsi che non ci siano spazi finali.
    {: tip}
    {: curl}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "os"
      "github.com/watson-developer-cloud/go-sdk/naturallanguageclassifierv1"
    )

    func main() {

      naturalLanguageClassifier, naturalLanguageClassifierErr := naturallanguageclassifierv1.
        NewNaturalLanguageClassifierV1(&naturallanguageclassifierv1.NaturalLanguageClassifierV1Options{
          URL: "{url}"{: url},
          IAMApiKey: "{apikey}"{: apikey},
        })
      if naturalLanguageClassifierErr != nil {
        panic(naturalLanguageClassifierErr)
      }

      metadata, metadataErr := os.Open("./metadata.json")
      if metadataErr != nil {
        panic(metadataErr)
      }
      defer metadata.Close()
      trainingData, trainingDataErr := os.Open("./weather_data_train.csv")
      if trainingDataErr != nil {
        panic(trainingDataErr)
      }
      defer trainingData.Close()
      response, responseErr := naturalLanguageClassifier.CreateClassifier(
        &naturallanguageclassifierv1.CreateClassifierOptions{
          TrainingData: trainingData,
          Metadata:     metadata,
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      result := naturalLanguageClassifier.GetCreateClassifierResult(response)
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: go}
    {: codeblock}

    ```java
    IamOptions options = new IamOptions.Builder()
      .apiKey("{apikey}"{: apikey})
      .build();

    NaturalLanguageClassifier naturalLanguageClassifier = new NaturalLanguageClassifier(options);
    naturalLanguageClassifier.setEndPoint("{url}"{: url});

    CreateClassifierOptions createOptions = new CreateClassifierOptions.Builder()
      .metadata("./metadata.json")
      .trainingData(new File("./weather_data_train.csv"))
      .trainingDataFilename("weather_data_train.csv")
      .build();
    Classifier classifier = naturalLanguageClassifier.createClassifier(createOptions)
    .execute();
    System.out.println(classifier);
    ```
    {: java}
    {: codeblock}

    ```javascript
    var NaturalLanguageClassifierV1 = require('watson-developer-cloud/natural-language-classifier/v1');
    var fs = require('fs');

    var naturalLanguageClassifier = new NaturalLanguageClassifierV1({
      iam_apikey: '{apikey}'{: apikey},
      url: '{url}'{: url}
    });

    var params = {
      metadata_filename: 'metadata.json',
      metadata: fs.createReadStream('./metadata.json'),
      training_data: fs.createReadStream('./weather_data_train.csv')
    };

    naturalLanguageClassifier.createClassifier(params,
      function(err, response) {
        if (err) {
          console.log('error:', err);
        } else {
          console.log(JSON.stringify(response, null, 2));
        }
    });
    ```
    {: javascript}
    {: codeblock}

    ```python
    import json
    from watson_developer_cloud import NaturalLanguageClassifierV1

    natural_language_classifier = NaturalLanguageClassifierV1(
        iam_apikey='{apikey}'{: apikey},
        url='{url}'{: url})

    with open('./weather_data_train.csv', 'rb') as training_data:
        with open('./metadata.json', 'rb') as metadata:
          classifier = natural_language_classifier.create_classifier(
            training_data=training_data,
            metadata=metadata
          ).get_result()
    print(json.dumps(classifier, indent=2))
    ```
    {: python}
    {: codeblock}

    ```ruby
    require "json"
    require "ibm_watson/natural_language_classifier_v1"
    include IBMWatson

    natural_language_classifier = NaturalLanguageClassifierV1.new(
      iam_apikey: "{apikey}"{: apikey},
      url: "{url}"{: url}
    )

    File.open("./training_data") do |training_data|
      File.open("./metadata") do |metadata|
        classifier = natural_language_classifier.create_classifier(
          training_data: training_data,
          metadata: metadata
        )
        puts JSON.pretty_generate(classifier.result)
      end
    end
    ```
    {: ruby}
    {: codeblock}

    La risposta include un nuovo stato e ID del classificatore, come nel seguente esempio. 

    ```json
    {
      "name": "TutorialClassifier",
      "language": "en",
      "status": "Training",
      "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/0e6935x475-nlc-2948",
      "classifier_id": "0e6935x475-nlc-2948",
      "created": "2018-12-10T17:42:31.823Z",
      "status_description": "The classifier instance is in its training phase, not yet ready to accept classify requests"
    }
    ```

    La preparazione inizia immediatamente e deve finire prima di poter eseguire la query del classificatore.
1.  Controlla lo stato di preparazione periodicamente finché visualizzi lo stato `Available`. Con questi dati di esempio, la preparazione dura circa 6 minuti:

    Immetti una chiamata al metodo **Get information about a classifier** per richiamare lo stato del classificatore. <span class="hide-dashboard">Sostituisci `{apikey}` e `{url}` con le credenziali che hai copiato nei prerequisiti.</span> Sostituisci `{classifier_id}` con le tue informazioni.

    ```bash
    curl -u "apikey:{apikey}"{: apikey} \
    "{url}/v1/classifiers/{classifier_id}"{: url}
    ```
    {: pre}
    {: curl}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "github.com/watson-developer-cloud/go-sdk/core"
      "github.com/watson-developer-cloud/go-sdk/naturallanguageclassifierv1"
    )

    func main() {

      naturalLanguageClassifier, naturalLanguageClassifierErr := naturallanguageclassifierv1.
        NewNaturalLanguageClassifierV1(&naturallanguageclassifierv1.NaturalLanguageClassifierV1Options{
          URL: "{url}",
          IAMApiKey: "{apikey}",
        })
      if naturalLanguageClassifierErr != nil {
        panic(naturalLanguageClassifierErr)
      }

      response, responseErr := naturalLanguageClassifier.GetClassifier(
        &naturallanguageclassifierv1.GetClassifierOptions{
          ClassifierID: core.StringPtr("{classifier_id}"),
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      result := naturalLanguageClassifier.GetGetClassifierResult(response)
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: go}
    {: codeblock}

    ```java
    IamOptions options = new IamOptions.Builder()
      .apiKey("{apikey}"{: apikey})
      .build();

    NaturalLanguageClassifier naturalLanguageClassifier = new NaturalLanguageClassifier(options);
    naturalLanguageClassifier.setEndPoint("{url}"{: url});

    GetClassifierOptions getOptions = new GetClassifierOptions.Builder()
      .classifierId("{classifier_id}")
      .build();
    Classifier classifier = naturalLanguageClassifier.getClassifier(getOptions);
      .execute();
    System.out.println(classifier);
    ```
    {: java}
    {: codeblock}

    ```javascript
    var NaturalLanguageClassifierV1 = require('watson-developer-cloud/natural-language-classifier/v1');
    var fs = require('fs');

    var naturalLanguageClassifier = new NaturalLanguageClassifierV1({
      iam_apikey: '{apikey}'{: apikey},
      url: '{url}'{: url}
    });

    naturalLanguageClassifier.getClassifier({
      classifier_id: '{classifier_id}' },
      function(err, response) {
        if (err) {
          console.log('error:', err);
        } else {
          console.log(JSON.stringify(response, null, 2));
        }
    });
    ```
    {: javascript}
    {: codeblock}

    ```python
    import json
    from watson_developer_cloud import NaturalLanguageClassifierV1

    natural_language_classifier = NaturalLanguageClassifierV1(
        iam_apikey='{apikey}'{: apikey},
        url='{url}'{: url})

    status = natural_language_classifier.get_classifier('{classifier_id}').get_result()
    print (json.dumps(status, indent=2))
    ```
    {: python}
    {: codeblock}

    ```ruby
    require "json"
    require "ibm_watson/natural_language_classifier_v1"
    include IBMWatson

    natural_language_classifier = NaturalLanguageClassifierV1.new(
      iam_apikey: "{apikey}"{: apikey},
      url: "{url}"{: url}
    )

    status = natural_language_classifier.get_classifier(
      classifier_id: "{classifier_id}"
    )
    puts JSON.pretty_generate(status.result)
    ```
    {: ruby}
    {: codeblock}

## Passo 2: classifica il testo
{: #getting-started-classify}

Ora che il classificatore è stato preparato, puoi eseguirne la query.

1.  Classifica alcune domande correlate al meteo per controllare come risponde il tuo classificatore preparato più recentemente. Questa è una chiamata di esempio.
    - {: hide-dashboard} Sostituisci `{apikey}` e `{url}` con le credenziali che hai copiato nei prerequisiti.
    - Sostituisci `{classifier_id}` con le tue informazioni.

    ```bash
    curl -G -u "apikey:{apikey}"{: apikey} \
    "{url}/v1/classifiers/{classifier_id}/classify"{: url} \
    --data-urlencode "text=How hot will it be today?"
    ```
    {: pre}
    {: curl}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "github.com/watson-developer-cloud/go-sdk/core"
      "github.com/watson-developer-cloud/go-sdk/naturallanguageclassifierv1"
    )

    func main() {

      naturalLanguageClassifier, naturalLanguageClassifierErr := naturallanguageclassifierv1.
        NewNaturalLanguageClassifierV1(&naturallanguageclassifierv1.NaturalLanguageClassifierV1Options{
          URL: "{url}"{: url},
          IAMApiKey: "{apikey}"{: apikey},
        })
      if naturalLanguageClassifierErr != nil {
        panic(naturalLanguageClassifierErr)
      }

      response, responseErr := naturalLanguageClassifier.Classify(
        &naturallanguageclassifierv1.ClassifyOptions{
          ClassifierID: core.StringPtr("{classifier_id}"),
          Text:         core.StringPtr("How hot will it be today?"),
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      result := naturalLanguageClassifier.GetClassifyResult(response)
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: go}
    {: codeblock}

    ```java
    IamOptions options = new IamOptions.Builder()
      .apiKey("{apikey}"{: apikey})
      .build();

    NaturalLanguageClassifier naturalLanguageClassifier = new NaturalLanguageClassifier(options);
    naturalLanguageClassifier.setEndPoint("{url}"{: url});

    ClassifyOptions classifyOptions = new ClassifyOptions.Builder()
      .classifierId("{classifier_id}")
      .text("How hot will it be today?")
      .build();
    Classification classification = naturalLanguageClassifier.classify(classifyOptions)
      .execute();
    System.out.println(classification);
    ```
    {: java}
    {: codeblock}

    ```javascript
    var NaturalLanguageClassifierV1 = require('watson-developer-cloud/natural-language-classifier/v1');

    var naturalLanguageClassifier = new NaturalLanguageClassifierV1({
      iam_apikey: '{apikey}'{: apikey},
      url: '{url}'{: url}
    });

    naturalLanguageClassifier.classify({
      text: 'How hot will it be today?',
      classifier_id: '{classifier_id}' },
      function(err, response) {
        if (err) {
          console.log('error:', err);
        } else {
          console.log(JSON.stringify(response, null, 2));
        }
    });
    ```
    {: javascript}
    {: codeblock}

    ```python
    import json
    from watson_developer_cloud import NaturalLanguageClassifierV1

    natural_language_classifier = NaturalLanguageClassifierV1(
        iam_apikey='{apikey}'{: apikey},
        url='{url}'{: url})

    classes = natural_language_classifier.classify('{classifier_id}', 'How hot will it be today?').get_result()
    print(json.dumps(classes, indent=2))
    ```
    {: python}
    {: codeblock}

    ```ruby
    require "json"
    require "ibm_watson/natural_language_classifier_v1"
    include IBMWatson

    natural_language_classifier = NaturalLanguageClassifierV1.new(
      iam_apikey: "{apikey}"{: apikey},
      url: "{url}"{: url}
    )

    status = natural_language_classifier.get_classifier(
      classifier_id: "{classifier_id}"
    )
    puts JSON.pretty_generate(status.result)
    ```
    {: ruby}
    {: codeblock}

    L'API restituisce una risposta che include il nome della classe con cui il classificatore ha la confidenza più elevata. Altre coppie di confidenza-classe sono elencate in ordine di confidenza:

    ```json
    {
      "classifier_id": "0e6935x475-nlc-2948",
      "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1",
      "text": "How hot will it be today?",
	  "top_class": "temperature",
	  "classes": [
	    {
          "class_name": "temperature",
          "confidence": 0.9930577105371443
        },
        {
          "class_name": "conditions",
          "confidence": 0.00694228946285564
        }
      ]
    }
    ```

    Il valore della confidenza rappresenta una percentuale e il valore più alto rappresenta la confidenza più alta. La risposta include fino a 10 classi.

    Se hai meno di 10 classi nei tuoi dati di formazione, il totale di tutti i valori di confidenza è 100%. In questi dati di formazione di esempio, sono definite solo due classi, per cui ne possono essere restituite solo due.
1.  Verifica la classe più il alto per le domande per visualizzare come il classificatore le sta prevedendo.

    Queste sono alcune domande di esempio da classificare:

    - Fa caldo fuori?
    - Sarà ventoso?
    - Si avrà il sole?
    - Quale è la temperatura prevista più elevata per oggi?
    - Sarà nebbioso domani mattina?

    Una delle domande di esempio include una termine ("nebbioso") per cui il classificatore non è preparato. Il classificatore può riuscire ad ottenere questi termini "mancanti" senza alcuna tua ulteriore azione per identificarli. Prova altre domande che includo parole non presenti nei dati di formazione, ad esempio "nevischio" o "tempesta".

L'operazione è terminata! Hai creato, preparato ed eseguito query di un classificatore nel servizio {{site.data.keyword.nlclassifiershort}}.

Questa esercitazione classifica una singola frase. {{site.data.keyword.nlclassifiershort}} supporta anche la classificazione di più frasi in una sola chiamata. Per i dettagli, consulta **Classify multiple phrases** nella [Guida di riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){: new_window}.
{: tip}

## Elimina il classificatore dell'esercitazione
{: #getting-started-delete}

Per poter creare i classificatori per il tuo proprio utilizzo e con i tuoi dati di formazione, potresti voler eliminare questo classificatore dall'esercitazione.

- {: hide-dashboard} Sostituisci `{apikey}` e `{url}` con le credenziali che hai copiato nei prerequisiti.
- Sostituisci `{classifier_id}` con le tue informazioni.

```bash
curl -X DELETE -u "apikey:{apikey}"{: apikey} \
"{url}/v1/classifiers/{classifier_id}"{: url}
```
{: pre}
{: curl}

```go
package main

import (
  "github.com/watson-developer-cloud/go-sdk/core"
  "github.com/watson-developer-cloud/go-sdk/naturallanguageclassifierv1"
)

func main() {

  naturalLanguageClassifier, naturalLanguageClassifierErr := naturallanguageclassifierv1.
    NewNaturalLanguageClassifierV1(&naturallanguageclassifierv1.NaturalLanguageClassifierV1Options{
      URL: "{url}"{: url},
      IAMApiKey: "{apikey}"{: apikey},
    })
  if naturalLanguageClassifierErr != nil {
    panic(naturalLanguageClassifierErr)
  }

  _, responseErr := naturalLanguageClassifier.DeleteClassifier(
    &naturallanguageclassifierv1.DeleteClassifierOptions{
      ClassifierID: core.StringPtr("{classifier_id}"),
    },
  )
  if responseErr != nil {
    panic(responseErr)
  }
}

```
{: go}
{: codeblock}

```java
IamOptions options = new IamOptions.Builder()
  .apiKey("{apikey}"{: apikey})
  .build();

NaturalLanguageClassifier naturalLanguageClassifier = new NaturalLanguageClassifier(options);
naturalLanguageClassifier.setEndPoint("{url}"{: url});

DeleteClassifierOptions deleteOptions = new DeleteClassifierOptions.Builder()
  .classifierId("{classifier_id}")
  .build();
naturalLanguageClassifier.deleteClassifier(deleteOptions).execute();
```
{: java}
{: codeblock}

```javascript
var NaturalLanguageClassifierV1 = require('watson-developer-cloud/natural-language-classifier/v1');
var fs = require('fs');

var naturalLanguageClassifier = new NaturalLanguageClassifierV1({
  iam_apikey: '{apikey}'{: apikey},
  url: '{url}'{: url}
});

naturalLanguageClassifier.deleteClassifier({
  classifier_id: '{classifier_id}' },
  function(err, response) {
    if (err) {
      console.log('error:', err);
    } else {
      console.log(JSON.stringify(response, null, 2));
    }
});
```
{: javascript}
{: codeblock}

```python
import json
from watson_developer_cloud import NaturalLanguageClassifierV1

natural_language_classifier = NaturalLanguageClassifierV1(
    iam_apikey='{apikey}'{: apikey},
    url='{url}'{: url})

status = natural_language_classifier.delete_classifier('{classifier_id}').get_result()
print (json.dumps(status, indent=2))
```
{: python}
{: codeblock}

```ruby
require "json"
require "ibm_watson/natural_language_classifier_v1"
include IBMWatson

natural_language_classifier = NaturalLanguageClassifierV1.new(
  iam_apikey: "{apikey}"{: apikey},
  url: "{url}"{: url}
)

status = natural_language_classifier.delete_classifier(
  classifier_id: "{classifier_id}"
)
puts JSON.pretty_generate(status.result)
```
{: ruby}
{: codeblock}

La risposta è un oggetto JSON vuoto.

## Passi successivi
{: #getting-started-next-steps}

Hai una conoscenza di base su come utilizzare {{site.data.keyword.nlclassifiershort}}. Ora approfondisci:

- Questa esercitazione utilizza una chiave API per l'autenticazione. Per utilizzi di produzione, consulta le [procedure consigliate](/docs/services/watson?topic=watson-api-key-bp#api-bp) delle chiavi API del servizio IAM.
- Impara come [preparare i tuoi dati](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data) per preparare un classificatore.
- {: curl}Troverai ulteriori informazioni sull'API nel [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}
- {: go} Leggi le informazioni sull'API in [API reference ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier?language=go){: new_window}.
- {: java} Leggi le informazioni sull'API in [API reference ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier?language=java){: new_window}.
- {: javascript} Leggi le informazioni sull'API in [API reference ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier?language=node){: new_window}.
- {: python} Leggi le informazioni sull'API in [API reference ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier?language=python){: new_window}.
- {: ruby} Leggi le informazioni sull'API in [API reference ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/natural-language-classifier?language=ruby){: new_window}.
- Esplora le [applicazioni di esempio](/docs/services/natural-language-classifier?topic=natural-language-classifier-sample-applications#sample-applications) per degli esempi di utilizzo.
