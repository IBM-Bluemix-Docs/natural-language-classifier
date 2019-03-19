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

# 入門指導教學
{: #natural-language-classifier}

{{site.data.keyword.nlclassifierfull}} 可協助您的應用程式瞭解簡短文字的語言，並預測如何處理它們。分類器會先瞭解您的範例資料，接著可以傳回未對其進行訓練之文字的資訊。
您可以在不超過 15 分鐘的時間內建立及訓練此分類器。
{:shortdesc}

如果您偏好使用圖形介面，則請使用 {{site.data.keyword.DSX}}。[啟動工具 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://dataplatform.cloud.ibm.com/registration/stepone?context=wdp){: new_window}，並遵循文件中的[建置分類器 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/nlc-create.html?audience=wdp&context=analytics){: new_window}。
{: tip}

## 開始之前
{: #prerequisites}

- {: hide-dashboard}建立服務的實例：
    1.  移至型錄中的 [{{site.data.keyword.nlclassifiershort}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/catalog/services/natural-language-classifier){: new_window} 頁面。
    1.  註冊免費的 {{site.data.keyword.Bluemix_notm}} 帳戶或登入。
    1.  按一下**建立**。
- {: hide-dashboard}複製用來鑑別服務實例的認證：
    1.  在**管理**頁面上，按一下**顯示認證**。
    1.  複製 `API 金鑰`及 `URL` 值。
- {: curl}請確定您有 `curl` 指令。
    - 測試是否安裝 `curl`。請在指令行上執行下列指令。如果輸出列出具有 SSL 支援的 `curl` 版本，則您已設定好指導教學。

        ```bash
        curl -V
        ```
        {: pre}

    - 必要的話，請從 [curl.haxx.se ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://curl.haxx.se/){: new_window} 安裝已啟用 SSL 的版本。如果您要從任何指令行位置執行 `curl`，則請將檔案的位置新增至 PATH 環境變數。
- {:go}安裝 [Go SDK ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/watson-developer-cloud/go-sdk){: new_window}。

    ```go
    go get -u github.com/watson-developer-cloud/go-sdk/...
    ```
    {: go}
    {: pre}

- {: java}安裝 [Java SDK ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/watson-developer-cloud/java-sdk){: new_window}
    - {: java}Maven

        ```java
        <dependency>
          <groupId>com.ibm.watson.developer_cloud</groupId>
          <artifactId>java-sdk</artifactId>
          <version>{version}</version>
        </dependency>
        ```
        {: codeblock}

    - {: java}Gradle

        ```bash
        compile 'com.ibm.watson.developer_cloud:java-sdk:{version}'
        ```
        {:pre}

- {: javascript}安裝 [Node SDK ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/watson-developer-cloud/node-sdk){: new_window}

    ```bash
    npm install --save watson-developer-cloud
    ```
- {: python}安裝 [Python SDK ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/watson-developer-cloud/python-sdk){: new_window}

    ```bash
    pip install --upgrade watson-developer-cloud
    ```
- {: ruby}安裝 [Ruby SDK ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/watson-developer-cloud/ruby-sdk){: new_window}

    ```bash
    gem install ibm_watson
    ```

下列視訊將逐步引導您完成本指導教學。
{: #video}

<iframe class="embed-responsive-item" id="youtubeplayer" title="入門指導教學的視訊逐步演練" type="text/html" width="560" height="315" src="https://www.youtube.com/embed/SUj826ybCdU?rel=0" webkitallowfullscreen mozallowfullscreen allowfullscreen gesture="media" allow="encrypted-media"></iframe>

## 步驟 1：建立及訓練分類器
{: #create-train}

分類器要先瞭解範例，才能傳回以前未看過之文字的資訊。範例資料稱為「訓練資料」。當您建立分類器時，即可上傳訓練資料。

1.  下載兩個範例檔案：
    - <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a> 也用於與[展示 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://natural-language-classifier-demo.ng.bluemix.net/){:new_window} 搭配使用。此檔案的格式為 CSV 且內含兩個直欄。第一個直欄是文字輸入。第二個直欄是該文字的類別：溫度或狀況。請檢視檔案來查看項目。

    - <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/metadata.json" download="metadata.json">metadata.json</a> 檔案指定資料的語言 (`en`)，並包括用來識別分類器的名稱。
1.  發出下列指令來呼叫**建立分類器**方法，以上傳訓練資料，以及建立名稱為 "TutorialClassifier" 的英文語言分類器：
    - {: hide-dashboard}將 `{apikey}` 及 `{url}` 取代為您已在必要條件中複製的認證。
    - 修改 `training_data` 及 `training_metadata` 的位置，以指向您儲存兩個範例檔案的位置。

    ```bash
    curl -i -u "apikey:{apikey}"{: apikey} \
    -F training_data=@weather_data_train.csv \
    -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" \
    "{url}/v1/classifiers"{: url}
    ```
    {: pre}
    {: curl}

    Windows 使用者：將每行結尾的反斜線 (`\`) 取代為脫字符號 (`^`)。請確定沒有尾端空格。
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

    回應包括新的分類器 ID 及狀態，如下列範例所示。

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

訓練會立即開始，而且必須先完成，您才能查詢分類器。
1.  除非您看到`可用`狀態，否則請定期檢查訓練狀態。使用這個範例資料，訓練大約需要 6 分鐘：

    發出**取得分類器的相關資訊**方法的呼叫，以擷取分類器的狀態。<span class="hide-dashboard">將 `{apikey}` 及 `{url}` 取代為您已在必要條件中複製的認證。</span>將 `{classifier_id}` 取代為您的資訊。

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

## 步驟 2：分類文字
{: #getting-started-classify}

現在，已訓練過分類器，您可以對其進行查詢。

1.  分類一些天氣相關問題，以檢閱新訓練分類器的回應方式。以下是範例呼叫。
    - {: hide-dashboard}將 `{apikey}` 及 `{url}` 取代為您已在必要條件中複製的認證。
    - 將 `{classifier_id}` 取代為您的資訊。

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

    API 會傳回一個回應，其中包括分類器具有最高信任之類別的名稱。其他類別/信任配對則會依遞減信任順序列出：

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

    信任值以百分比呈現，值越高，代表越受信任。回應最多包括 10 個類別。

如果您訓練資料中的類別少於 10 個，則所有信任值的總和為 100%。 在此範例訓練資料中，只定義兩個類別，因此只會傳回兩個類別。
1.  檢閱問題的頂端類別，以查看分類器如何預測它們。

    以下是要分類的一些其他範例問題：

    - Is it hot outside?（外面是否很熱？）
    - Will it be windy?（會刮風嗎？）
    - Will we see some sun?（會看到一些陽光嗎？）
    - What is the expected high for today?（今天的預期最高溫度為何？）
    - Will it be foggy tomorrow morning?（明早是否起霧？）

    其中一個範例問題包括分類器未受過訓練的術語 ("foggy")。分類器可以對這些「遺漏」術語進行良好評分，而您不需要執行額外工作即可識別它們。請嘗試其他問題，而這些問題包括不在訓練資料中的單字（例如，"sleet" 或 "storm"）。

已完成！您已在 {{site.data.keyword.nlclassifiershort}} 服務中建立、訓練及查詢分類器。

本指導教學會分類單一詞組。{{site.data.keyword.nlclassifiershort}} 也支援透過單一呼叫來分類多個詞組。如需詳細資料，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){: new_window} 中的**分類多個詞組**。
{: tip}

## 刪除指導教學分類器
{: #getting-started-delete}

因此，您可以使用專屬訓練資料來建立專用分類器，而且可能會想要從指導教學刪除此分類器。

- {: hide-dashboard}將 `{apikey}` 及 `{url}` 取代為您已在必要條件中複製的認證。
- 將 `{classifier_id}` 取代為您的資訊。

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

回應是空的 JSON 物件。

## 後續步驟
{: #getting-started-next-steps}

您對如何使用 {{site.data.keyword.nlclassifiershort}} 有基本瞭解。現在，請更深入地探討：

- 本指導教學使用 API 金鑰來進行鑑別。針對正式作業使用，請檢閱 IAM 服務 API 金鑰[最佳作法](/docs/services/watson?topic=watson-api-key-bp#api-bp)。
- 瞭解如何[準備資料](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data)來訓練分類器。
- {: curl}在 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier){:new_window} 中閱讀 API
- {: go}在 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier?language=go){: new_window} 中閱讀 API。
- {: java}在 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier?language=java){: new_window} 中閱讀 API。
- {: javascript}在 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier?language=node){: new_window} 中閱讀 API。
- {: python}在 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier?language=python){: new_window} 中閱讀 API。
- {: ruby}在 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier?language=ruby){: new_window} 中閱讀 API。
- 探索[範例應用程式](/docs/services/natural-language-classifier?topic=natural-language-classifier-sample-applications#sample-applications)以瞭解範例使用。
