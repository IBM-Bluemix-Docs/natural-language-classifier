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

# Tutoriel d'initiation
{: #natural-language-classifier}

{{site.data.keyword.nlclassifierfull}} peut aider votre application à comprendre la langue de textes courts et à prévoir comment les traiter. Un discriminant effectue son apprentissage à partir de vos exemples de données, puis peut renvoyer des informations pour les textes pour lesquels il n'est pas entraîné. Vous pouvez créer et entraîner ce discriminant en moins de quinze minutes.
{:shortdesc}

Si vous préférez travailler dans une interface graphique, utilisez {{site.data.keyword.DSX}}. [Lancez l'outil ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://dataplatform.cloud.ibm.com/registration/stepone?context=wdp){: new_window} et suivez les instructions de [génération d'un discriminant ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/nlc-create.html?audience=wdp&context=analytics){: new_window} dans la documentation.
{: tip}

## Avant de commencer
{: #prerequisites}

- {: hide-dashboard} Créez une instance du service :
    1.  Accédez à la page [{{site.data.keyword.nlclassifiershort}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/natural-language-classifier){: new_window} du catalogue.
    1.  Inscrivez-vous pour un compte {{site.data.keyword.Bluemix_notm}} gratuite ou connectez-vous.
    1.  Cliquez sur **Créer**.
- {: hide-dashboard} Copiez les données d'identification pour vous authentifier auprès de votre instance de service :
    1.  Sur la page **Gérer**, cliquez sur **Afficher les données d'identification**.
    1.  Copiez les valeurs des zones `Clé d'API` et `URL`.
- {: curl} Veillez à disposez de la commande `curl`.
    - Vérifiez si `curl` est installée. Exécutez la commande suivante sur la ligne de commande. Si la sortie de la commande indique la version `curl` avec support SSL, vous êtes configuré pour ce tutoriel.

        ```bash
        curl -V
        ```
        {: pre}

    - Au besoin, installez une version avec SSL activé depuis [curl.haxx.se ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://curl.haxx.se/){: new_window}. Ajoutez l'emplacement du fichier à vos variables d'environnement PATH si vous voulez exécuter `curl` à partir de n'importe quel emplacement de ligne de commande.
- {:go} Installez le logiciel [SDK Go ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/watson-developer-cloud/go-sdk){: new_window}.

    ```go
    go get -u github.com/watson-developer-cloud/go-sdk/...
    ```
    {: go}
    {: pre}

- {: java} Installez le logiciel [SDK Java ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/watson-developer-cloud/java-sdk){: new_window}
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

- {: javascript}Installez le logiciel [SDK Node ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/watson-developer-cloud/node-sdk){: new_window}

    ```bash
    npm install --save watson-developer-cloud
    ```
- {: python}Installez le logiciel [SDK Python ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/watson-developer-cloud/python-sdk){: new_window}.

    ```bash
    pip install --upgrade watson-developer-cloud
    ```
- {: ruby}Installez le logiciel [SDK Ruby ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/watson-developer-cloud/ruby-sdk){: new_window}.

    ```bash
    gem install ibm_watson
    ```

La vidéo suivante vous présente les étapes de ce tutoriel.
{: #video}

<iframe class="embed-responsive-item" id="youtubeplayer" title="Vidéo de présentation détaillée du tutoriel d'initiation " type="text/html" width="560" height="315" src="https://www.youtube.com/embed/SUj826ybCdU?rel=0" webkitallowfullscreen mozallowfullscreen allowfullscreen gesture="media" allow="encrypted-media"></iframe>

## Etape 1 : Création et entraînement d'un discriminant 
{: #create-train}

Le discriminant effectue son apprentissage à partir d'exemples avant de pouvoir renvoyer des informations pour des textes qu'il n'a jamais vus auparavant. Les exemples de données sont appelés "données d'apprentissage". Vous les téléchargez lorsque vous créez un discriminant.

1.  Téléchargez les deux fichiers d'exemple :
    - Le fichier <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a> est celui utilisé pour la [démonstration ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://natural-language-classifier-demo.ng.bluemix.net/){:new_window}. Le fichier est au format CSV et comporte deux colonnes. La première colonne contient l'entrée de texte. La deuxième colonne contient la classe pour ce texte : temperature ou condition. Affichez le fichier pour visualiser les entrées.
    - Le fichier <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/metadata.json" download="metadata.json">metadata.json</a> spécifie la langue des données (`en`) et inclut un nom pour identifier le discriminant.
1.  Exécutez la commande suivante pour appeler la méthode **Create classifier**, qui télécharge les données d'apprentissage et crée un discriminant de la langue anglaise nommé "TutorialClassifier":
    - {: hide-dashboard} Remplacez `{apikey}` et `{url}` par les données d'identification précédemment copiées.
    - Modifiez l'emplacement de `training_data` et `training_metadata` pour désigner le répertoire dans lequel vous avez sauvegardé les fichiers d'exemple.

    ```bash
    curl -i -u "apikey:{apikey}"{: apikey} \
    -F training_data=@weather_data_train.csv \
    -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" \
    "{url}/v1/classifiers"{: url}
    ```
    {: pre}
    {: curl}

    Utilisateurs Windows : Remplacez la barre oblique inversée (``\`) à la fin de chaque ligne par un accent circonflexe (``^`). Vérifiez qu'il n'y a aucun espace de fin.
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

    La réponse inclut un nouvel ID de discriminant et un statut, comme dans l'exemple suivant.

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

    L'apprentissage commence immédiatement et doit être terminé pour que vous puissiez interroger le discriminant.
1.  Vérifiez le statut d'apprentissage régulièrement jusqu'à ce qu'il s'agisse d'`Available`. Avec ces exemples de données, l'apprentissage prend environ 6 minutes :

    Appelez la méthode **Get information about a classifier** afin d'extraire le statut du discriminant. <span class="hide-dashboard">Remplacez `{apikey}` et `{url}` par les données d'identification précédemment copiée.</span> Remplacez `{classifier_id}` par vos informations.

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

## Etape 2 : Classification du texte 
{: #getting-started-classify}

Maintenant que le discriminant est entraîné, vous pouvez l'interroger.

1.  Classifiez des questions relatives à la météo pour déterminer la façon dont le discriminant que vous venez d'entraîner répond. Voici un exemple d'appel.
    - {: hide-dashboard} Remplacez `{apikey}` et `{url}` par les données d'identification précédemment copiées.
    - Remplacez `{classifier_id}` par vos informations.

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

    L'API renvoie une réponse qui inclut le nom de la classe que le discriminant considère comme la plus fiable. D'autres paires classe-fiabilité sont répertoriées par ordre décroissant de fiabilité :

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

    Le niveau de fiabilité correspond à un pourcentage, et les valeurs les plus élevées représentent des niveaux de fiabilité élevés. La réponse peut inclure jusqu'à dix classes.

    Si vous disposez de moins de dix classes dans vos données d'apprentissage, la somme de tous les niveaux de fiabilité est de 100 %. Dans ces exemples de données d'apprentissage, deux classes seulement sont définies ; par conséquent, deux classes seulement peuvent être renvoyées.
1.  Examinez la classe supérieure pour les questions afin de déterminer dans quelle mesure le discriminant les prévoit.

    Voici d'autres exemples de question à classifier :

    - Is it hot outside? (Fait-il chaud dehors ?)
    - Will it be windy? (Y'aura-t-il du vent ?)
    - Will we see some sun? (Y'aura-t-il du soleil ?)
    - What is the expected high for today? (Quelle est la température maximale prévue pour aujourd'hui ?)
    - Will it be foggy tomorrow morning? (Y'aura-t-il du brouillard demain matin ?)

    L'un des exemples de question inclut un terme ("foggy") que le discriminant ne connaît pas. Ce dernier peut obtenir de bon résultats avec ces termes "manquants" sans que vous n'ayez à effectuer de tâches supplémentaires pour les identifier. Essayez d'autres questions incluant des mots qui ne figurent pas dans les données d'apprentissage, par exemple "sleet" (grésil) ou "storm" (orage).

Vous avez terminé ! Vous avez créé, entraîné et interrogé un discriminant dans le service {{site.data.keyword.nlclassifiershort}}.

Ce tutoriel classifie une seule phrase. {{site.data.keyword.nlclassifiershort}} prend également en charge la classification de plusieurs phrases dans un unique appel. Pour plus d'informations, voir la section **Classify multiple phrases** dans la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){: new_window}.
{: tip}

## Supprimez le discriminant du tutoriel
{: #getting-started-delete}

Pour pouvoir créer vos propres discriminants avec vos propres données d'apprentissage, il est recommandé de supprimer ce discriminant du tutoriel.

- {: hide-dashboard} Remplacez `{apikey}` et `{url}` par les données d'identification précédemment copiées.
- Remplacez `{classifier_id}` par vos informations.

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

La réponse est un objet JSON vide.

## Etapes suivantes
{: #getting-started-next-steps}

Vous avez compris les principes de base de l'utilisation de {{site.data.keyword.nlclassifiershort}}. A présent, approfondissez vos connaissances :

- Ce tutoriel utilise une clé d'interface de programmation (API) pour l'authentification. Pour une utilisation en production, revoyez les [pratiques recommandées](/docs/services/watson?topic=watson-api-key-bp#api-bp) en matière de clés d'API de service IAM.
- Apprenez à [préparer vos données](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data) pour entraîner un discriminant. 
- {: curl} Lisez les informations sur l'API dans la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}
- {: go} Lisez la documentation sur l'API dans la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/natural-language-classifier?language=go){: new_window}.
- {: java} Lisez la documentation sur l'API dans la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/natural-language-classifier?language=java){: new_window}.
- {: javascript} Lisez la documentation sur l'API dans la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/natural-language-classifier?language=node){: new_window}.
- {: python} Lisez la documentation sur l'API dans la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/natural-language-classifier?language=python){: new_window}.
- {: ruby} Lisez la documentation sur l'API dans la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/natural-language-classifier?language=ruby){: new_window}.
- Explorez les [exemples d'application](/docs/services/natural-language-classifier?topic=natural-language-classifier-sample-applications#sample-applications) pour découvrir des exemples d'utilisation.
