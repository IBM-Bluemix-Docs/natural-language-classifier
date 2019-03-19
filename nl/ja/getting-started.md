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

# 入門チュートリアル
{: #natural-language-classifier}

{{site.data.keyword.nlclassifierfull}} は、アプリケーションがショート・テキストの言語を理解し、それらのテキストの処理方法を予測するのに役立ちます。 分類子は、サンプル・データから学習した後、トレーニングされていないテキストに関する情報を返すことができるようになります。 この分類子の作成とトレーニングには 15 分もかかりません。
{:shortdesc}

グラフィカル・インターフェースを使用したい場合は、{{site.data.keyword.DSX}} を使用してください。[ツールを起動して ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://dataplatform.cloud.ibm.com/registration/stepone?context=wdp){: new_window}、資料の[分類子の作成 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/nlc-create.html?audience=wdp&context=analytics){: new_window} の手順を実行してください。
{: tip}

## 始めに
{: #prerequisites}

- {: hide-dashboard} サービスのインスタンスを作成します。
    1.  カタログの [{{site.data.keyword.nlclassifiershort}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/catalog/services/natural-language-classifier){: new_window} ページに移動します。
    1.  無料の {{site.data.keyword.Bluemix_notm}} アカウントに登録するか、ログインします。
    1.  **「作成」**をクリックします。
- {: hide-dashboard} 資格情報をコピーし、以下のようにしてサービス・インスタンスに認証します。
    1.  **「管理」**ページで、**「資格情報の表示」**をクリックします。
    1.  `API 鍵`と `URL` の値をコピーします。
- {: curl}`curl` コマンドを使用できることを確認します。
    - `curl` がインストールされているかどうかをテストします。コマンド・ラインで以下のコマンドを実行してください。SSL サポート付きの `curl` バージョンが出力に表示されたら、チュートリアルを実行するための準備は完了です。

        ```bash
        curl -V
        ```
        {: pre}

    - 必要に応じて、SSL 対応バージョンを [curl.haxx.se ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://curl.haxx.se/){: new_window} からインストールします。コマンド・ラインの任意の場所から `curl` を実行できるようにするには、PATH 環境変数にこのファイルの場所を追加してください。
- {:go} [Go SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/watson-developer-cloud/go-sdk){: new_window} をインストールします。

    ```go
    go get -u github.com/watson-developer-cloud/go-sdk/...
    ```
    {: go}
    {: pre}

- {: java} [Java SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/watson-developer-cloud/java-sdk){: new_window} をインストールします。
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

- {: javascript} [Node SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/watson-developer-cloud/node-sdk){: new_window} をインストールします。

    ```bash
    npm install --save watson-developer-cloud
    ```
- {: python} [Python SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/watson-developer-cloud/python-sdk){: new_window} をインストールします。

    ```bash
    pip install --upgrade watson-developer-cloud
    ```
- {: ruby} [Ruby SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/watson-developer-cloud/ruby-sdk){: new_window} をインストールします。

    ```bash
    gem install ibm_watson
    ```

このチュートリアルを説明したビデオが以下にあります。
{: #video}

<iframe class="embed-responsive-item" id="youtubeplayer" title="入門チュートリアルのビデオ・ウォークスルー" type="text/html" width="560" height="315" src="https://www.youtube.com/embed/SUj826ybCdU?rel=0" webkitallowfullscreen mozallowfullscreen allowfullscreen gesture="media" allow="encrypted-media"></iframe>

## ステップ 1: 分類子の作成およびトレーニング
{: #create-train}

分類子は、以前見たことのないテキストに関する情報を返す前にサンプルから学習します。 それらのサンプル・データは、「トレーニング・データ」と呼ばれます。 分類器を作成する際は、トレーニング・データをアップロードします。

1.  2 つのサンプル・ファイルをダウンロードします。
    - <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a> は、[デモ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://natural-language-classifier-demo.ng.bluemix.net/){:new_window} で使用されているものと同じファイルです。このファイルは、2 つの列から成る CSV フォーマットのファイルです。 最初の列はテキスト入力です。 2 番目の列は、そのテキストのクラス (temperature または condition) です。 このファイルを表示して、項目を確認します。
    - <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/metadata.json" download="metadata.json">metadata.json</a> ファイルには、データの言語 (`en`) と分類子を識別する名前が指定されています。
1.  以下のコマンドを実行して**分類子を作成する**メソッドを呼び出します。このコマンドによって、トレーニング・データがアップロードされ、「TutorialClassifier」という名前の英語の分類子が作成されます。
    - {: hide-dashboard}`{apikey}` と `{url}` は、前提条件の作業時にコピーした資格情報に置き換えてください。
    - `training_data` と `training_metadata` の場所は、2 つのサンプル・ファイルの保存場所を指すように変更してください。

    ```bash
    curl -i -u "apikey:{apikey}"{: apikey} \
    -F training_data=@weather_data_train.csv \
    -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" \
    "{url}/v1/classifiers"{: url}
    ```
    {: pre}
    {: curl}

    Windows ユーザー: 各行末の円記号 (`\`) をキャレット (`^`) に置き換えてください。末尾にスペースが入らないように注意してください。
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

    以下の例からわかるように、応答には新しい分類子の ID と状況が含まれています。

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

    トレーニングが即時に開始されます。分類子を照会するには、その前にトレーニングが終了している必要があります。
1.  `Available` の状況が表示されるまで、トレーニング状況を定期的に確認してください。 このサンプル・データでは、トレーニングは約 6 分かかります。

    **分類子情報を取得する**メソッドの呼び出しを実行して、分類子の状況を取得します。<span class="hide-dashboard">`{apikey}` と `{url}` は、前提条件の作業時にコピーした資格情報に置き換えてください。</span>`{classifier_id}` は実際の情報に置き換えてください。

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

## ステップ 2: テキストの分類
{: #getting-started-classify}

分類子のトレーニングが終了したため、分類子を照会できます。

1.  いくつかの天気関連の質問を分類して、新たにトレーニングされた分類子がどのように応答するかを確認します。 以下に、呼び出しの例を示します。
    - {: hide-dashboard}`{apikey}` と `{url}` は、前提条件の作業時にコピーした資格情報に置き換えてください。
    - `{classifier_id}` は実際の情報に置き換えてください。

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

    API は、分類子が最も高い信頼度を持つクラスの名前を含む応答を返します。 その他のクラスと信頼度のペアは、信頼度の降順でリストされます。

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

    信頼度の値はパーセンテージを表し、値が高いほど信頼度が高いことを意味します。 応答には、最大 10 個のクラスが含まれます。

    トレーニング・データに含まれているクラスが 10 個より少ない場合、信頼度のすべての値の合計は 100% です。このサンプルのトレーニング・データでは、2 つのクラスのみが定義されているため、2 つのみを返すことができます。
1.  分類子が質問をどのように予測しているかを確認するには、質問の最上位クラスを参照します。

    以下に、分類する質問のその他のいくつかの例を示します。

    - Is it hot outside?
    - Will it be windy?
    - Will we see some sun?
    - What is the expected high for today?
    - Will it be foggy tomorrow morning?

    質問の例の 1 つには、分類子がトレーニングされていない用語 (「foggy」) が含まれています。 これらの「欠落」している用語を識別するために追加の作業をユーザーが行わなくても、分類子はこれらの用語で適切にスコアリングすることができます。 トレーニング・データにない用語 (例えば、「sleet」や「storm」) を含むその他の質問を試してみます。

これで完了です。 {{site.data.keyword.nlclassifiershort}} サービスで、分類子の作成、トレーニング、および照会を行いました。

このチュートリアルでは、1 つの句を分類します。{{site.data.keyword.nlclassifiershort}} では、1 つの呼び出しで複数の句を分類することも可能です。詳細については、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){: new_window} の**複数の句の分類**を参照してください。
{: tip}

## チュートリアル分類子の削除
{: #getting-started-delete}

独自のトレーニング・データで自分用に分類子を作成できるように、チュートリアルからこの分類子を削除することをお勧めします。

- {: hide-dashboard}`{apikey}` と `{url}` は、前提条件の作業時にコピーした資格情報に置き換えてください。
- `{classifier_id}` は実際の情報に置き換えてください。

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

応答は空の JSON オブジェクトです。

## 次のステップ
{: #getting-started-next-steps}

{{site.data.keyword.nlclassifiershort}} の使用方法の基本を理解しました。 さらに知識を深めてください。

- このチュートリアルでは、API 鍵を使用して認証します。 実動用については、IAM サービスの API 鍵の[ベスト・プラクティス](/docs/services/watson?topic=watson-api-key-bp#api-bp)を参照してください。
- 分類子をトレーニングするための[データの準備](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data)方法を確認してください。
- {: curl} [API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/natural-language-classifier){:new_window} で、API に関する説明を読みます。
- {: go} [API リファレンス ![「外部リンク」アイコン](../../icons/launch-glyph.svg "「外部リンク」アイコン")](https://{DomainName}/apidocs/natural-language-classifier?language=go){: new_window} で API について確認します。
- {: java} [API リファレンス ![「外部リンク」アイコン](../../icons/launch-glyph.svg "「外部リンク」アイコン")](https://{DomainName}/apidocs/natural-language-classifier?language=java){: new_window} で API について確認します。
- {: javascript} [API リファレンス ![「外部リンク」アイコン](../../icons/launch-glyph.svg "「外部リンク」アイコン")](https://{DomainName}/apidocs/natural-language-classifier?language=node){: new_window} で API について確認します。
- {: python} [API リファレンス ![「外部リンク」アイコン](../../icons/launch-glyph.svg "「外部リンク」アイコン")](https://{DomainName}/apidocs/natural-language-classifier?language=python){: new_window} で API について確認します。
- {: ruby} [API リファレンス ![「外部リンク」アイコン](../../icons/launch-glyph.svg "「外部リンク」アイコン")](https://{DomainName}/apidocs/natural-language-classifier?language=ruby){: new_window} で API について確認します。
- [サンプル・アプリ](/docs/services/natural-language-classifier?topic=natural-language-classifier-sample-applications#sample-applications)で使用例を探索してください。
