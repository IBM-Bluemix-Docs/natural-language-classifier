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

# Tutorial de introdução
{: #natural-language-classifier}

O {{site.data.keyword.nlclassifierfull}} pode ajudar o seu aplicativo a entender a linguagem de textos curtos e a fazer predições sobre como manipulá-los. Um classificador aprende com seus dados de exemplo e então pode retornar informações para os textos nos quais ele não está treinado. É possível criar e treinar esse classificador em menos de 15 minutos.
{:shortdesc}

Se você preferir trabalhar em uma interface gráfica, use o {{site.data.keyword.DSX}}. [Ative a ferramenta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://dataplatform.cloud.ibm.com/registration/stepone?context=wdp){: new_window} e siga [Construindo um classificador ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/nlc-create.html?audience=wdp&context=analytics){: new_window} nos docs.
{: tip}

## Antes de Começar
{: #prerequisites}

- {: hide-dashboard} Crie uma instância do serviço:
    1.  Acesse a página [{{site.data.keyword.nlclassifiershort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/natural-language-classifier){: new_window} no catálogo.
    1.  Inscreva-se para obter uma conta gratuita do {{site.data.keyword.Bluemix_notm}} ou efetue login.
    1.  Clique em  ** Criar **.
- {: hide-dashboard} Copie as credenciais para autenticação em sua instância de serviço:
    1.  Na página **Gerenciar**, clique em **Mostrar credenciais**.
    1.  Copie os valores `API Key` e `URL`.
- {: curl} Certifique-se de que você tenha o comando `curl`.
    - Teste se o  ` curl `  está instalado. Execute o comando a seguir na linha de comandos. Se a saída listar a versão `curl` com suporte de SSL, você estará pronto para começar o tutorial.

        ```bash
        curl -V
        ```
        {: pre}

    - Se necessário, instale uma versão com SSL ativada por meio de [curl.haxx.se ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://curl.haxx.se/){: new_window}. Inclua o local do arquivo em suas variáveis de ambiente PATH se você desejar executar `curl` em qualquer local de linha de comandos.
- {:go} Instale o [SDK do Go ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/watson-developer-cloud/go-sdk){: new_window}.

    ```go
    go get -u github.com/watson-developer-cloud/go-sdk/...
    ```
    {: go}
    {: pre}

- {: java} Instale o [SDK do Java ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/watson-developer-cloud/java-sdk){: new_window}
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
        compile 'com.ibm.watson.developer_cloud:java-sdk: {'
        ```
        {:pre}

- {: javascript} Instale o [SDK do Node ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/watson-developer-cloud/node-sdk){: new_window}

    ```bash
    npm install --save watson-developer-cloud
    ```
- {: python} Instale o [SDK do Python ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/watson-developer-cloud/python-sdk){: new_window}

    ```bash
    pip install --upgrade watson-developer-cloud
    ```
- {: ruby} Instale o [SDK do Ruby ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/watson-developer-cloud/ruby-sdk){: new_window}

    ```bash
    gem install ibm_watson
    ```

O vídeo a seguir guia você por esse tutorial.
{: #video}

<iframe class="embed-responsive-item" id="youtubeplayer" title="Video walkthrough of Getting started tutorial" type="text/html" width="560" height="315" src="https://www.youtube.com/embed/SUj826ybCdU?rel=0" webkitallowfullscreen mozallowfullscreen allowfullscreen gesture="media" allow="encrypted-media"></iframe>

## Etapa 1: Criar e treinar um classificador
{: #create-train}

O classificador aprende com exemplos antes que possa retornar informações para os textos que ainda não viu. Os dados de exemplo são referidos como "dados de treinamento". Faça
upload dos dados de treinamento ao criar um classificador.

1.  Faça download dos dois arquivos de amostra:
    - O <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a> é o mesmo que foi usado com a [demo ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://natural-language-classifier-demo.ng.bluemix.net/){:new_window}. O arquivo está em um formato CSV em duas colunas. A primeira coluna é a entrada de texto. A segunda coluna é a classe para esse texto: temperatura ou condição. Visualize o arquivo para ver as entradas.
    - O arquivo <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/metadata.json" download="metadata.json">metadata.json</a> especifica a linguagem dos dados (`en`) e inclui um nome para identificar o classificador.
1.  Emita o comando a seguir para chamar o método **Criar classificador**, que faz upload dos dados de treinamento e cria um classificador de linguagem em inglês com o nome "TutorialClassifier":
    - {: hide-dashboard} Substitua `{apikey}` e `{url}` pelas credenciais que você copiou nos pré-requisitos.
    - Modifique o local de `training_data` e `training_metadata` para apontar para o local em que você salvou os dois arquivos de amostra.

    ```bash
    curl -i -u "apikey: {"{: apikey} \
    -F training_data=@weather_data_train.csv \
    -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" \
    "{url}/v1/classifiers"{: url}
    ```
    {: pre}
    {: curl}

    Usuários do Windows: substituam a barra invertida (``\`) no final de cada linha por um circunflexo (``^`). Certifiquem-se de que não haja espaços à direita.
    {: tip}
    {: curl}

    ```go
    principal do pacote

    import (
      "encoding/json"
      "fmt"
      "os"
      "github.com/watson-developer-cloud/go-sdk/naturallanguageclassifierv1"
    )

    func main () {

      naturalLanguageClassifier, naturalLanguageClassifierErr: = naturallinguageclassifierv1.
        NewNaturalLanguageClassifierV1(&naturallanguageclassifierv1.NaturalLanguageClassifierV1Options{ URL: "{url}"{: url}, IAMApiKey: "{apikey}"{: apikey},
        })
      if naturalLanguageClassifierErr! = nil {
        pânico (naturalLanguageClassifierErr)
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
      if responseErr! = nil {
        panic(responseErr) }
      result := naturalLanguageClassifier.GetCreateClassifierResult(response)
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println (string (b)) }
    ```
    {: go}
    {: codeblock}

    ```java
    Opções de IamOptions = new IamOptions.Builder ()
      .apiKey ("{"{: apikey})
      .build ();

    NaturalLanguageClassifier naturalLanguageClassifier = new NaturalLanguageClassifier(options); naturalLanguageClassifier.setEndPoint("{url}"{: url});

    CreateClassifierOptions createOptions = new CreateClassifierOptions.Builder ()
      .metadata( "./metadata.json ")
      .trainingData (new File ("./weather_data_train.csv "))
      .trainingDataFilename ("weather_data_train.csv")
      .build();
    Classifier classifier = naturalLanguageClassifier.createClassifier(createOptions)
    .execute(); System.out.println(classifier);
    ```
    {: java}
    {: codeblock}

    ```javascript
    var NaturalLanguageClassifierV1 = require('watson-developer-cloud/natural-language-classifier/v1'); var fs = require('fs');

    var naturalLanguageClassifier = new NaturalLanguageClassifierV1 ({
      iam_apikey: '{apikey}'{: apikey}, url: '{url}'{: url}
    });

    var params = {
      metadata_filename: 'metadata.json',
      metadata: fs.createReadStream('./metadata.json'),
      training_data: fs.createReadStream('./weather_data_train.csv')
    };

    naturalLanguageClassifier.createClassifier(params,
      function(err, response) {
        if (err) {
          console.log('error:', err); } else {
          console.log(JSON.stringify(response, null, 2)); }
    });
    ```
    {: javascript}
    {: codeblock}

    ```python
    import json from watson_developer_cloud import NaturalLanguageClassifierV1

    natural_language_classifier = NaturalLanguageClassifierV1( iam_apikey='{apikey}'{: apikey}, url='{url}'{: url})

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
    require "json" require "ibm_watson/natural_language_classifier_v1" include IBMWatson

    natural_language_classifier = NaturalLanguageClassifierV1.new( iam_apikey: "{apikey}"{: apikey}, url: "{url}"{: url}
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

    A resposta inclui um novo ID de classificador e um status, como no exemplo a seguir.

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

    O treinamento começa imediatamente e deve ser concluído antes de ser possível consultar o classificador.
1.  Verifique o status de treinamento periodicamente até que veja um status de `Disponível`. Com esses dados de amostra, o treinamento leva cerca de 6 minutos:

    Emita uma chamada para o método **Obter informações sobre um classificador** para recuperar o status do classificador. <span class="hide-dashboard">Substitua `{apikey}` e `{url}` pelas credenciais que você copiou nos pré-requisitos.</span> Substitua  ` { `  por suas informações.

    ```bash
    curl -u "apikey: {"{: apikey} \
    "{1}/classifiers/ {"{: url}
    ```
    {: pre}
    {: curl}

    ```go
    principal do pacote

    import (
      "encoding/json" "fmt" "github.com/watson-developer-cloud/go-sdk/core" "github.com/watson-developer-cloud/go-sdk/naturallanguageclassifierv1"
    )

    func main () {

      naturalLanguageClassifier, naturalLanguageClassifierErr: = naturallinguageclassifierv1.
        NewNaturalLanguageClassifierV1(&naturallanguageclassifierv1.NaturalLanguageClassifierV1Options{
          URL: "{url}",
          IAMApiKey: "{apikey}",
        })
      if naturalLanguageClassifierErr! = nil {
        pânico (naturalLanguageClassifierErr)
      }

      response, responseErr := naturalLanguageClassifier.GetClassifier(
        &naturallanguageclassifierv1.GetClassifierOptions{
          ClassifierID: core.StringPtr("{classifier_id}"),
        },
      )
      if responseErr! = nil {
        panic(responseErr) }
      result := naturalLanguageClassifier.GetGetClassifierResult(response)
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println (string (b)) }
    ```
    {: go}
    {: codeblock}

    ```java
    Opções de IamOptions = new IamOptions.Builder ()
      .apiKey ("{"{: apikey})
      .build ();

    NaturalLanguageClassifier naturalLanguageClassifier = new NaturalLanguageClassifier(options); naturalLanguageClassifier.setEndPoint("{url}"{: url});

    GetClassifierOptions getOptions = new GetClassifierOptions.Builder ()
      .classifierId ("{")
      .build();
    Classifier classifier = naturalLanguageClassifier.getClassifier(getOptions);
      .execute(); System.out.println(classifier);
    ```
    {: java}
    {: codeblock}

    ```javascript
    var NaturalLanguageClassifierV1 = require('watson-developer-cloud/natural-language-classifier/v1'); var fs = require('fs');

    var naturalLanguageClassifier = new NaturalLanguageClassifierV1 ({
      iam_apikey: '{apikey}'{: apikey}, url: '{url}'{: url}
    });

    naturalLanguageClassifier.getClassifier({
      classifier_id: '{classifier_id}' },
      function(err, response) {
        if (err) {
          console.log('error:', err); } else {
          console.log(JSON.stringify(response, null, 2)); }
    });
    ```
    {: javascript}
    {: codeblock}

    ```python
    import json from watson_developer_cloud import NaturalLanguageClassifierV1

    natural_language_classifier = NaturalLanguageClassifierV1( iam_apikey='{apikey}'{: apikey}, url='{url}'{: url})

    status = natural_language_classifier.get_classifier('{classifier_id}').get_result()
    print (json.dumps(status, indent=2))
    ```
    {: python}
    {: codeblock}

    ```ruby
    require "json" require "ibm_watson/natural_language_classifier_v1" include IBMWatson

    natural_language_classifier = NaturalLanguageClassifierV1.new( iam_apikey: "{apikey}"{: apikey}, url: "{url}"{: url}
    )

    status = natural_language_classifier.get_classifier( classifier_id: "{classifier_id}" )
    puts JSON.pretty_generate (status.result)
    ```
    {: ruby}
    {: codeblock}

## Etapa 2: Classificar texto
{: #getting-started-classify}

Agora que o classificador está treinado, será possível consultá-lo.

1.  Classifique algumas perguntas relacionadas ao clima para revisar como seu classificador recém-treinado responde. Aqui está uma chamada de exemplo.
    - {: hide-dashboard} Substitua `{apikey}` e `{url}` pelas credenciais que você copiou nos pré-requisitos.
    - Substitua  ` { `  por suas informações.

    ```bash
    curl -G -u "apikey: {"{: apikey} \
    "{1}/classifiers/ { /classify"{: url} \
    --data-urlencode "text=How hot will it be today?"
    ```
    {: pre}
    {: curl}

    ```go
    principal do pacote

    import (
      "encoding/json" "fmt" "github.com/watson-developer-cloud/go-sdk/core" "github.com/watson-developer-cloud/go-sdk/naturallanguageclassifierv1"
    )

    func main () {

      naturalLanguageClassifier, naturalLanguageClassifierErr: = naturallinguageclassifierv1.
        NewNaturalLanguageClassifierV1(&naturallanguageclassifierv1.NaturalLanguageClassifierV1Options{ URL: "{url}"{: url}, IAMApiKey: "{apikey}"{: apikey},
        })
      if naturalLanguageClassifierErr! = nil {
        pânico (naturalLanguageClassifierErr)
      }

      response, responseErr := naturalLanguageClassifier.Classify(
        &naturallanguageclassifierv1.ClassifyOptions{
          ClassifierID: core.StringPtr("{classifier_id}"),
          Text:         core.StringPtr("How hot will it be today?"),
        },
      )
      if responseErr! = nil {
        panic(responseErr) }
      result := naturalLanguageClassifier.GetClassifyResult(response)
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println (string (b)) }
    ```
    {: go}
    {: codeblock}

    ```java
    Opções de IamOptions = new IamOptions.Builder ()
      .apiKey ("{"{: apikey})
      .build ();

    NaturalLanguageClassifier naturalLanguageClassifier = new NaturalLanguageClassifier(options); naturalLanguageClassifier.setEndPoint("{url}"{: url});

    ClassifyOptions ClassifyOptions = new ClassifyOptions.Builder ()
      .classifierId ("{")
      .text ("How hot it it be hoje?")
      .build();
    Classification classification = naturalLanguageClassifier.classify(classifyOptions)
      .execute (); System.out.println (classificação);
    ```
    {: java}
    {: codeblock}

    ```javascript
    var NaturalLanguageClassifierV1 = require ('watson-developer-cloud/natural-language-classifier/v1');

    var naturalLanguageClassifier = new NaturalLanguageClassifierV1 ({
      iam_apikey: '{apikey}'{: apikey}, url: '{url}'{: url}
    });

    naturalLanguageClassifier.classify({
      text: 'Quão quente estará hoje?',
      classifier_id: '{classifier_id}' },
      function(err, response) {
        if (err) {
          console.log('error:', err); } else {
          console.log(JSON.stringify(response, null, 2)); }
    });
    ```
    {: javascript}
    {: codeblock}

    ```python
    import json from watson_developer_cloud import NaturalLanguageClassifierV1

    natural_language_classifier = NaturalLanguageClassifierV1( iam_apikey='{apikey}'{: apikey}, url='{url}'{: url})

    classes = natural_language_classifier.classify('{classifier_id}', 'Quão quente estará hoje?').get_result()
    print(json.dumps(classes, indent=2))
    ```
    {: python}
    {: codeblock}

    ```ruby
    require "json" require "ibm_watson/natural_language_classifier_v1" include IBMWatson

    natural_language_classifier = NaturalLanguageClassifierV1.new( iam_apikey: "{apikey}"{: apikey}, url: "{url}"{: url}
    )

    status = natural_language_classifier.get_classifier( classifier_id: "{classifier_id}" )
    puts JSON.pretty_generate (status.result)
    ```
    {: ruby}
    {: codeblock}

    A API retorna uma resposta que inclui o nome da classe para a qual o classificador tem a confiança mais alta. Outros pares de classe de confiança são listados em ordem decrescente de confiança:

    ```json
    {
      "classifier_id": "0e6935x475-nlc-2948",
      "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1",
      "text": "Quão quente estará hoje?",
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

    O valor de confiança representa uma porcentagem e valores mais altos representam confianças maiores. A resposta inclui até 10 classes.

    Se você tiver menos de 10 classes nos dados de treinamento, a soma de todos os valores de confiança será 100%. Nestes dados de treinamento de amostra, apenas duas classes são definidas, portanto, apenas duas podem ser retornadas.
1.  Revise a classe principal das perguntas para ver como o classificador as está predizendo.

    Aqui estão algumas outras perguntas de amostra para classificar:

    - Está quente lá fora?
    - Será que vai ventar?
    - Será que veremos sol?
    - Qual é a máxima esperada para hoje?
    - Será que teremos nevoeiro amanhã de manhã?

    Uma das perguntas de amostra inclui um termo ("nevoeiro") para o qual o classificador não está treinado. O classificador pode pontuar bem esses termos "omissos" sem ter que fazer trabalho extra para identificá-los. Tente outras perguntas que incluam palavras que não estejam nos dados de treinamento, por exemplo, "granizo" ou "tempestade".

Pronto! Você criou, treinou e consultou um classificador no serviço {{site.data.keyword.nlclassifiershort}}.

Este tutorial classifica uma única frase. O {{site.data.keyword.nlclassifiershort}} também suporta a classificação de múltiplas frases em uma única chamada. Para obter detalhes, consulte **Classificar múltiplas frases** na [referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){: new_window}.
{: tip}

## Exclua o classificador do tutorial
{: #getting-started-delete}

Para que seja possível criar classificadores para seu próprio uso e com seus próprios dados de treinamento, talvez você queira excluir esse classificador do tutorial.

- {: hide-dashboard} Substitua `{apikey}` e `{url}` pelas credenciais que você copiou nos pré-requisitos.
- Substitua  ` { `  por suas informações.

```bash
curl -X DELETE -u "apikey:{apikey}"{: apikey} \
"{url } /v1/classifiers/ { /v1/classifiers/ { " {
```
{: pre}
{: curl}

```go
package main

import (
  "github.com/watson-developer-cloud/go-sdk/core" "github.com/watson-developer-cloud/go-sdk/naturallanguageclassifierv1"
)

func main() {

  naturalLanguageClassifier, naturalLanguageClassifierErr: = naturallinguageclassifierv1.
    NewNaturalLanguageClassifierV1(&naturallanguageclassifierv1.NaturalLanguageClassifierV1Options{
      URL: "{url}"{: url},
      IAMApiKey: "{apikey}"{: apikey},
    })
  if naturalLanguageClassifierErr! = nil {
    pânico (naturalLanguageClassifierErr) }

  _, responseErr := naturalLanguageClassifier.DeleteClassifier(
    &naturallanguageclassifierv1.DeleteClassifierOptions{
      ClassifierID: core.StringPtr("{classifier_id}"),
    },
  )
  if responseErr! = nil {
    Pânico (responseErr)
  }
}

```
{: go}
{: codeblock}

```java
Opções de IamOptions = new IamOptions.Builder ()
  .apiKey("{apikey}"{: apikey})
  .build ();

NaturalLanguageClassifier naturalLanguageClassifier = new NaturalLanguageClassifier(options);
naturalLanguageClassifier.setEndPoint("{url}"{: url});

DeleteClassifierOptions deleteOptions = new DeleteClassifierOptions.Builder ()
  .classifierId ("{")
  .build (); naturalLanguageClassifier.deleteClassifier (deleteOptions) .execute ();
```
{: java}
{: codeblock}

```javascript
var NaturalLanguageClassifierV1 = require('watson-developer-cloud/natural-language-classifier/v1'); var fs = require('fs');

var naturalLanguageClassifier = new NaturalLanguageClassifierV1 ({
  iam_apikey: '{apikey}'{: apikey},
  url: '{url}'{: url}
});

naturalLanguageClassifier.deleteClassifier({
  classifier_id: '{classifier_id}' },
  function(err, response) {
    if (err) {
      console.log('error:', err); } else {
      console.log(JSON.stringify(response, null, 2)); }
});
```
{: javascript}
{: codeblock}

```python
import json from watson_developer_cloud import NaturalLanguageClassifierV1

natural_language_classifier = NaturalLanguageClassifierV1(
    iam_apikey='{apikey}'{: apikey},
    url='{url}'{: url})

status = natural_language_classifier.delete_classificfier ('{2}))
```
{: python}
{: codeblock}

```ruby
require "json" require "ibm_watson/natural_language_classifier_v1" include IBMWatson

natural_language_classifier = NaturalLanguageClassifierV1.new(
  iam_apikey: "{apikey}"{: apikey},
  url: "{url}"{: url}
)

status = natural_language_classifier.delete_classifier(
  classifier_id: "{classifier_id}"
)
puts JSON.pretty_generate (status.result)
```
{: ruby}
{: codeblock}

A resposta é um objeto de JSON vazio.

## Etapas Seguintes
{: #getting-started-next-steps}

Você tem um entendimento básico de como usar o {{site.data.keyword.nlclassifiershort}}. Agora vá além:

- Este tutorial usa uma chave API para autenticação. Para usos de produção, revise as [melhores práticas](/docs/services/watson?topic=watson-api-key-bp#api-bp) das chaves de API de serviço do IAM.
- Saiba como [preparar os seus dados](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data) para treinar um classificador.
- {: curl} Leia sobre a API na [Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}
- {: go} Leia sobre a API na [referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier?language=go){: new_window}.
- {: java} Leia sobre a API na [referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier?language=java){: new_window}.
- {: javascript} Leia sobre a API na [referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier?language=node){: new_window}.
- {: python} Leia sobre a API na [referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier?language=python){: new_window}.
- {: ruby} Leia sobre a API na [referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier?language=ruby){: new_window}.
- Explore os [aplicativos de amostra](/docs/services/natural-language-classifier?topic=natural-language-classifier-sample-applications#sample-applications) para usos de exemplo.
