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

# Einführung - Lernprogramm
{: #natural-language-classifier}

{{site.data.keyword.nlclassifierfull}} kann Ihre Anwendung dabei unterstützen, die Sprache kurzer Texte zu verstehen und Vorhersagen zu ihrer Verarbeitung zu erstellen. Ein Klassifikationsmerkmal (Classifier) lernt anhand Ihrer Beispieldaten und kann anschließend Informationen zu Texten zurückgeben, anhand derer es nicht trainiert wurde. Sie können dieses Klassifikationsmerkmal in weniger als 15 Minuten erstellen und trainieren.
{:shortdesc}

Wenn Sie es vorziehen, in einer grafischen Schnittstelle zu arbeiten, verwenden Sie {{site.data.keyword.DSX}}. [Starten Sie das Tool ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://dataplatform.cloud.ibm.com/registration/stepone?context=wdp){: new_window} und befolgen Sie die Anweisungen in [Klassifikationsmerkmal erstellen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/nlc-create.html?audience=wdp&context=analytics){: new_window} in der Dokumentation.
{: tip}

## Vorbereitende Schritte
{: #prerequisites}

- {: hide-dashboard} Erstellen Sie eine Instanz des Service: 
    1.  Rufen Sie die Seite [{{site.data.keyword.nlclassifiershort}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/natural-language-classifier){: new_window} im Katalog auf. 
    1.  Registrieren Sie sich für ein kostenloses {{site.data.keyword.Bluemix_notm}}-Konto oder melden Sie sich an. 
    1.  Klicken Sie auf **Erstellen**. 
- {: hide-dashboard} Kopieren Sie die Berechtigungsnachweise für die Authentifizierung bei Ihrer Serviceinstanz: 
    1.  Auf der Seite **Verwalten** klicken Sie auf **Berechtigungsnachweise anzeigen**. 
    1.  Kopieren Sie die Werte für `API-Schlüssel` und `URL`. 
- {: curl} Stellen Sie sicher, dass der Befehl `curl` vorhanden ist. 
    - Testen Sie, ob `curl` installiert ist. Führen Sie den folgenden Befehl in der Befehlszeile aus. Wenn in der Ausgabe die `curl`-Version mit SSL-Unterstützung aufgelistet wird, können Sie das Lernprogramm ausführen. 

        ```bash
        curl -V
        ```
        {: pre}

    - Falls erforderlich, installieren Sie eine Version mit aktiviertem SSL von [curl.haxx.se ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://curl.haxx.se/){: new_window}. Fügen Sie die Position der Datei zu Ihren PATH-Umgebungsvariablen hinzu, wenn Sie `curl` von einer beliebigen Befehlszeilenposition aus ausführen möchten. 
- {:go} Installieren Sie das [Go-SDK ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/watson-developer-cloud/go-sdk){: new_window}. 

    ```go
    go get -u github.com/watson-developer-cloud/go-sdk/...
    ```
    {: go}
    {: pre}

- {: java} Installieren Sie das [Java-SDK ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/watson-developer-cloud/java-sdk){: new_window}
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

- {: javascript} Installieren Sie das [Node-SDK ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/watson-developer-cloud/node-sdk){: new_window}

    ```bash
    npm install --save watson-developer-cloud
    ```
- {: python} Installieren Sie das [Python-SDK ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/watson-developer-cloud/python-sdk){: new_window}

    ```bash
    pip install --upgrade watson-developer-cloud
    ```
- {: ruby} Installieren Sie das [Ruby-SDK ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/watson-developer-cloud/ruby-sdk){: new_window}

    ```bash
    gem install ibm_watson
    ```

Das folgende Video führt Sie durch dieses Lernprogramm.
{: #video}

<iframe class="embed-responsive-item" id="youtubeplayer" title="Video-Walkthrough des Lernprogramms zur Einführung" type="text/html" width="560" height="315" src="https://www.youtube.com/embed/SUj826ybCdU?rel=0" webkitallowfullscreen mozallowfullscreen allowfullscreen gesture="media" allow="encrypted-media"></iframe>

## Schritt 1: Klassifikationsmerkmal erstellen und trainieren
{: #create-train}

Das Klassifikationsmerkmal muss zunächst anhand von Beispielen lernen, bevor es Informationen zu Texten zurückgeben kann, die es zuvor nicht gesehen hat. Die Beispieldaten werden als 'Trainingsdaten' bezeichnet. Sie laden die Trainingsdaten beim Erstellen eines Klassifikationsmerkmals hoch.

1.  Laden Sie die beiden Beispieldateien herunter: 
    - Die Datei <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a> entspricht der Datei, die für die [Demo ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://natural-language-classifier-demo.ng.bluemix.net/){:new_window} verwendet wurde. Die Datei hat das CSV-Format und weist zwei Spalten auf. Die erste Spalte ist die Texteingabe. Die zweite Spalte gibt die Klasse für diesen Text an: 'Temperatur' (temperature) oder 'Bedingung' (condition). Zeigen Sie die Datei an, um die Einträge zu sehen.
    - Die Datei <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/metadata.json" download="metadata.json">metadata.json</a> gibt die Sprache der Daten (`en`) an und enthält einen Namen zur Identifizierung des Klassifikationsmerkmals. 
1.  Geben Sie den folgenden Befehl aus, um die Methode **Klassifikationsmerkmal erstellen** aufzurufen, die die Trainingsdaten hochlädt und ein Klassifikationsmerkmal für die englische Sprache mit dem Namen "TutorialClassifier" erstellt: 
    - {: hide-dashboard} Ersetzen Sie `{apikey}` und `{url}` durch die Berechtigungsnachweise, die Sie bei den vorbereitenden Schritten kopiert haben. 
    - Ändern Sie die Position von `training_data` und `training_metadata` in die Position, an der Sie die beiden Beispieldateien gespeichert haben. 

    ```bash
    curl -i -u "apikey:{apikey}"{: apikey} \
    -F training_data=@weather_data_train.csv \
    -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" \
    "{url}/v1/classifiers"{: url}
    ```
    {: pre}
    {: curl}

    Windows-Benutzer: Ersetzen Sie den umgekehrten Schrägstrich (``\`) am Ende jeder Zeile durch ein Winkelzeichen (``^`). Stellen Sie sicher, dass keine nachgestellten Leerzeichen vorhanden sind. {: tip}
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

    Die Antwort enthält eine neue Klassifikationsmerkmal-ID und einen neuen Status, wie im folgenden Beispiel dargestellt. 

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

    Das Training beginnt sofort und muss abgeschlossen sein, bevor Sie das Klassifikationsmerkmal abfragen können.
1.  Überprüfen Sie regelmäßig den Trainingsstatus, bis der Status `Verfügbar` angezeigt wird. Das Training mit diesen Beispieldaten dauert etwa 6 Minuten:

    Setzen Sie einen Aufruf der Methode **Informationen zu einem Klassifikationsmerkmal abrufen** ab, um den Status des Klassifikationsmerkmals abzurufen. <span class="hide-dashboard">Ersetzen Sie `{apikey}` und `{url}` durch die Berechtigungsnachweise, die Sie bei den vorbereitenden Schritten kopiert haben.</span> Ersetzen Sie `{classifier_id}` durch Ihre Informationen. 

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

## Schritt 2: Text klassifizieren
{: #getting-started-classify}

Das Klassifikationsmerkmal ist nun trainiert und Sie können es abfragen.

1.  Klassifizieren Sie einige auf das Wetter bezogenen Fragen, um zu überprüfen, wie Ihr neu trainiertes Klassifikationsmerkmal antwortet. Im Folgenden finden Sie einen Beispielaufruf.
    - {: hide-dashboard} Ersetzen Sie `{apikey}` und `{url}` durch die Berechtigungsnachweise, die Sie bei den vorbereitenden Schritten kopiert haben. 
    - Ersetzen Sie `{classifier_id}` durch Ihre Informationen. 

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

    Die API gibt eine Antwort zurück, in der der Name der Klasse enthalten ist, die das Klassifikationsmerkmal mit der höchsten Konfidenz bewertet hat. Weitere Paare aus 'Klasse' und 'Konfidenz' werden hinsichtlich der Konfidenz in absteigender Reihenfolge aufgelistet:

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

    Der Konfidenzwert wird durch einen Prozentsatz angegeben; höhere Werte stellen höhere Konfidenzwerte dar. Die Antwort enthält bis zu 10 Klassen.

    Wenn in Ihren Trainingsdaten weniger als 10 Klassen vorhanden sind, beträgt die Summe aller Konfidenzwerte 100 Prozent. In diesen als Beispiel verwendeten Trainingsdaten sind nur zwei Klassen definiert; es können also nur zwei zurückgegeben werden.
1.  Überprüfen Sie die höchste Klasse anhand der Fragen, um zu sehen, welche Vorhersage das Klassifikationsmerkmal für sie vornimmt.

    Hier einige weitere Beispielfragen, die klassifiziert werden können:

    - Is it hot outside?
    - Will it be windy?
    - Will we see some sun?
    - What is the expected high for today?
    - Will it be foggy tomorrow morning?

    In einer der Beispielfragen ist ein Begriff enthalten ('foggy' - neblig), für das das Klassifikationsmerkmal nicht trainiert ist. Das Klassifikationsmerkmal kann trotz 'fehlender' Begriffe eine gute Bewertung erzielen, ohne dass Sie sich zusätzlich mit der Ermittlung solcher Begriffe befassen müssen. Machen Sie einen Versuch mit anderen Fragen, in denen Wörter enthalten sind, die sich nicht in den Trainingsdaten befinden, beispielsweise 'sleet' (Graupelschauer) oder 'storm' (Sturm).

Fertig! Sie haben im Service '{{site.data.keyword.nlclassifiershort}}' ein Klassifikationsmerkmal erstellt, trainiert und abgefragt.

In diesem Lernprogramm wird ein einzelner Ausdruck klassifiziert. {{site.data.keyword.nlclassifiershort}} unterstützt auch die Klassifizierung mehrerer Ausdrücke in einem einzigen Aufruf. Details finden Sie in **Mehrere Ausdrücke klassifizieren** in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){: new_window}.
{: tip}

## Klassifikationsmerkmal des Lernprogramms löschen
{: #getting-started-delete}

Damit Sie Klassifikationsmerkmale mit eigenen Trainingsdaten und zu Ihrer eigenen Verwendung erstellen können, müssen Sie dieses Klassifikationsmerkmal aus dem Lernprogramm löschen.

- {: hide-dashboard} Ersetzen Sie `{apikey}` und `{url}` durch die Berechtigungsnachweise, die Sie bei den vorbereitenden Schritten kopiert haben. 
- Ersetzen Sie `{classifier_id}` durch Ihre Informationen. 

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

Die Antwort ist ein leeres JSON-Objekt. 

## Nächste Schritte
{: #getting-started-next-steps}

Sie verfügen jetzt über ein Grundverständnis der Verwendung von {{site.data.keyword.nlclassifiershort}}. Gehen Sie nun einen Schritt weiter:

- In diesem Lernprogramm wird ein API-Schlüssel für die Authentifizierung verwendet. Überprüfen Sie für Produktionsanwendungen die [bewährten Verfahren](/docs/services/watson?topic=watson-api-key-bp#api-bp) für die API-Schlüssel des IAM-Service. 
- Lernen Sie, wie Sie [Ihre Daten vorbereiten](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data), um ein  Klassifikationsmerkmal zu trainieren. 
- {: curl} Lesen Sie Informationen zur API in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}. 
- {: go} Lesen Sie Informationen zur API in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier?language=go){: new_window}.
- {: java} Lesen Sie Informationen zur API in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier?language=java){: new_window}.
- {: javascript} Lesen Sie Informationen zur API in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier?language=node){: new_window}.
- {: python} Lesen Sie Informationen zur API in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier?language=python){: new_window}.
- {: ruby} Lesen Sie Informationen zur API in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier?language=ruby){: new_window}.
- Erkunden Sie die [Beispielapps](/docs/services/natural-language-classifier?topic=natural-language-classifier-sample-applications#sample-applications) mit Verwendungsbeispielen. 
