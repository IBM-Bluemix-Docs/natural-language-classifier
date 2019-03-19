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

# 시작하기 튜토리얼
{: #natural-language-classifier}

{{site.data.keyword.nlclassifierfull}}는 애플리케이션이 단문 텍스트의 언어를 이해하고 해당 텍스트의 처리 방법을 예측할 수 있도록 도와줍니다. 분류자는 예제 데이터를 통해 훈련한 후에 아직 훈련되지 않은 텍스트에 대한 정보를 리턴할 수 있습니다. 사용자는 이 분류자를 15분 내에 작성하고 훈련할 수 있습니다. {:shortdesc}

그래픽 인터페이스에서 작업하려는 경우 {{site.data.keyword.DSX}}를 사용하십시오. [도구를 실행![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://dataplatform.cloud.ibm.com/registration/stepone?context=wdp){: new_window}하고 문서에 설명된 [분류자 빌드![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/nlc-create.html?audience=wdp&context=analytics){: new_window}를 수행하십시오.
{: tip}

## 시작하기 전에
{: #prerequisites}

- {: hide-dashboard}서비스 인스턴스 작성: 
    1.  카탈로그에서 [{{site.data.keyword.nlclassifiershort}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/catalog/services/natural-language-classifier){: new_window} 페이지로 이동하십시오. 
    1.  무료 {{site.data.keyword.Bluemix_notm}} 계정을 등록하거나 로그인하십시오. 
    1.  **작성**을 클릭하십시오. 
- {: hide-dashboard} 인증할 인증 정보를 서비스 인스턴스로 복사하십시오. 
    1.  **관리** 페이지에서 **인증 정보 표시**를 클릭하십시오. 
    1.  `API Key` 및 `URL` 값을 복사하십시오. 
- {: curl} `curl` 명령이 있는지 확인하십시오. 
    - `curl`이 설치되었는지 테스트하십시오. 명령행에서 다음 명령을 실행하십시오. SSL 지원을 제공하는 `curl` 버전이 출력에 나열될 경우 튜토리얼용으로 설정된 것입니다. 

        ```bash
        curl -V
        ```
        {: pre}

    - 필요한 경우 SSL 지원 버전을 [curl.haxx.se![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://curl.haxx.se/){: new_window}에서 설치하십시오. 원하는 명령행 위치에서 `curl`을 실행하려는 경우 파일 위치를 PATH 환경 변수에 추가하십시오. 
- {:go} [Go SDK![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/watson-developer-cloud/go-sdk){: new_window}를 설치하십시오. 

    ```go
    go get -u github.com/watson-developer-cloud/go-sdk/...
    ```
    {: go}
    {: pre}

- {: java} [Java SDK![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/watson-developer-cloud/java-sdk){: new_window}를 설치하십시오. 
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

- {: javascript} [Node SDK![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/watson-developer-cloud/node-sdk){: new_window}를 설치하십시오. 

    ```bash
    npm install --save watson-developer-cloud
    ```
- {: python} [Python SDK![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/watson-developer-cloud/python-sdk){: new_window}를 설치하십시오. 

    ```bash
    pip install --upgrade watson-developer-cloud
    ```
- {: ruby} [Ruby SDK![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/watson-developer-cloud/ruby-sdk){: new_window}를 설치하십시오. 

    ```bash
    gem install ibm_watson
    ```

다음 동영상은 이 튜토리얼에 대해 소개합니다.
{: #video}

<iframe class="embed-responsive-item" id="youtubeplayer" title="시작하기 튜토리얼의 안내 동영상" type="text/html" width="560" height="315" src="https://www.youtube.com/embed/SUj826ybCdU?rel=0" webkitallowfullscreen mozallowfullscreen allowfullscreen gesture="media" allow="encrypted-media"></iframe>

## 1단계: 분류자 작성 및 훈련
{: #create-train}

분류자가 이전에 본 적이 없는 텍스트에 대한 정보를 리턴할 수 있으려면 우선 예제를 학습합니다. 예제 데이터는 "훈련 데이터"라고 합니다. 분류자를 작성할 때 훈련 데이터를 업로드합니다.

1.  다음 두 개의 샘플 파일을 다운로드하십시오. 
    - <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a>는 [데모![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://natural-language-classifier-demo.ng.bluemix.net/){:new_window}에 사용된 것과 동일합니다. 이 파일은 CSV 형식으로 두 개의 열로 되어 있습니다. 첫 번째 열은 텍스트 입력입니다. 두 번째 열은 해당 텍스트의 클래스(온도 또는 상태)입니다. 파일을 보고 항목을 확인하십시오.
    - <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/metadata.json" download="metadata.json">metadata.json</a> 파일은 데이터 언어(`en`)를 지정하며 분류자 식별 이름을 포함하고 있습니다. 
1.  다음 명령을 실행하여 **분류자 작성** 메소드를 호출하십시오. 이 메소드는 훈련 데이터를 업로드하고 "TutorialClassifier"라는 이름으로 영어 분류자를 작성합니다. 
    - {: hide-dashboard} `{apikey}` 및 `{url}`을 전제조건에서 복사한 인증 정보로 바꾸십시오. 
    - 두 샘플 파일의 저장 위치를 가리키도록 `training_data` 및 `training_metadata`의 위치를 수정하십시오. 

    ```bash
    curl -i -u "apikey:{apikey}"{: apikey} \
    -F training_data=@weather_data_train.csv \
    -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" \
    "{url}/v1/classifiers"{: url}
    ```
    {: pre}
    {: curl}

    Windows 사용자: 각 행의 끝에 있는 백슬래시(`\`)를 캐럿(`^`)으로 바꾸십시오. 끝에 공백이 없는지 확인하십시오.
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

    다음 예에서와 같이, 응답에는 새 분류자 ID와 상태가 포함되어 있습니다. 

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

훈련이 바로 시작되며 이는 분류자의 조회가 가능하기 전에 완료되어야 합니다.
1.  `Available` 상태가 나타날 때까지 훈련 상태를 주기적으로 확인하십시오. 이 샘플 데이터로 훈련하는 데는 약 6분 정도 걸립니다.

    **분류자에 대한 정보 가져오기** 메소드에 대한 호출을 실행하여 분류자의 상태를 검색하십시오. <span class="hide-dashboard">`{apikey}` 및 `{url}`을 전제조건에서 복사한 인증 정보로 바꾸십시오.</span> `{classifier_id}`는 자신의 정보로 바꾸십시오. 

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

## 2단계: 텍스트 분류
{: #getting-started-classify}

이제 분류자를 훈련했으니 조회가 가능합니다.

1.  새로 훈련된 분류자가 어떻게 응답하는지 확인하려면 몇몇 날씨 관련 질문을 분류하십시오. 예제 호출은 다음과 같습니다.
    - {: hide-dashboard} `{apikey}` 및 `{url}`을 전제조건에서 복사한 인증 정보로 바꾸십시오. 
    - `{classifier_id}`는 자신의 정보로 바꾸십시오. 

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

    API는 분류자가 최상위 신뢰도를 갖는 클래스의 이름이 포함된 응답을 리턴합니다. 기타 클래스-신뢰도 쌍은 내림차순의 신뢰도 순서로 나열됩니다.

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

    신뢰도 값은 백분율로 표시되며, 값이 클수록 더 높은 신뢰도를 표시합니다. 응답에는 최대 10개의 클래스가 포함되어 있습니다.

훈련 데이터에 10개 미만의 클래스가 있는 경우, 모든 신뢰도 값의 합은 100% 입니다. 이 샘플 훈련 데이터에서는 두 개의 클래스만 정의되어 있으므로 두 개만 리턴될 수 있습니다.
1.  분류자의 예측 방식을 알아보려면 질문에 대해 최상위 클래스를 검토하십시오.

    분류할 일부 기타 샘플 질문은 다음과 같습니다.

    - 밖이 덥습니까?
    - 바람이 많이 불겠습니까?
    - 햇빛이 좀 보이겠습니까?
    - 오늘의 최고 예상 기온은 몇 도입니까?
    - 내일 아침에 안개가 끼겠습니까?

    샘플 질문 중 하나에는 분류자가 아직 훈련하지 않은 용어("안개가 끼다")가 포함되어 있습니다. 분류자는 식별을 위한 추가 작업을 수행할 필요 없이 이러한 "누락" 용어로 점수를 잘 매길 수 있습니다. 훈련 데이터에 없는 단어가 포함된 기타 질문을 시도해 보십시오(예: "진눈깨비" 또는 "폭우").

이제 모두 마쳤습니다! {{site.data.keyword.nlclassifiershort}} 서비스에서 분류자를 작성하고 훈련했으며 이를 조회했습니다.

이 튜토리얼은 단일 문구를 분류합니다. {{site.data.keyword.nlclassifiershort}}는 또한 한 번의 호출로 여러 개의 문구를 분류하는 기능도 지원합니다. 자세한 내용은 [API 참조서![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){: new_window}에서 **여러 문구 분류**를 참조하십시오.
{: tip}

## 튜토리얼 분류자 삭제
{: #getting-started-delete}

직접 사용을 위해 자체 훈련 데이터로 분류자를 작성할 수 있도록 튜토리얼에서 이 분류자를 삭제하고자 할 수 있습니다.

- {: hide-dashboard} `{apikey}` 및 `{url}`을 전제조건에서 복사한 인증 정보로 바꾸십시오. 
- `{classifier_id}`는 자신의 정보로 바꾸십시오. 

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

응답은 비어 있는 JSON 오브젝트입니다. 

## 다음 단계
{: #getting-started-next-steps}

이제 {{site.data.keyword.nlclassifiershort}}의 기본적인 사용법을 살펴보았습니다. 이제 심층 학습을 수행합니다. 

- 이 튜토리얼은 API 키를 사용하여 인증합니다. 프로덕션 용도에 대해서는 IAM 서비스 API 키 [우수 사례](/docs/services/watson?topic=watson-api-key-bp#api-bp)를 검토하십시오. 
- 분류자 훈련을 위해 [데이터를 준비](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data)하는 방법을 알아보십시오. 
- {: curl}[API 참조서![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}에서 API 관련 자료를 읽어보십시오. 
- {: go}[API 참조서![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier?language=go){: new_window}에서 API 관련 자료를 읽어보십시오.
- {: java}[API 참조서![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier?language=java){: new_window}에서 API 관련 자료를 읽어보십시오.
- {: javascript}[API 참조서![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier?language=node){: new_window}에서 API 관련 자료를 읽어보십시오.
- {: python}[API 참조서![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier?language=python){: new_window}에서 API 관련 자료를 읽어보십시오.
- {: ruby}[API 참조서![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier?language=ruby){: new_window}에서 API 관련 자료를 읽어보십시오.
- 예제 사용은 [샘플 앱](/docs/services/natural-language-classifier?topic=natural-language-classifier-sample-applications#sample-applications)을 탐색하십시오. 
