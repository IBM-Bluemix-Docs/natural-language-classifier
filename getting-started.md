---

copyright:
  years: 2015, 2019
lastupdated: "2019-01-09"

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

# Getting started tutorial
{: #natural-language-classifier}

{{site.data.keyword.nlclassifierfull}} can help your application understand the language of short texts and make predictions about how to handle them. A classifier learns from your example data and then can return information for texts that it is not trained on. You can create and train this classifier in less than 15 minutes.
{:shortdesc}

If you prefer to work in a graphical interface, use {{site.data.keyword.DSX}}. [Launch tool ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://dataplatform.cloud.ibm.com/registration/stepone?context=wdp){: new_window} and follow [Building a classifier ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/nlc-create.html?audience=wdp&context=analytics){: new_window} in the docs.
{: tip}

## Before you begin
{: #prerequisites}

- {: hide-dashboard} Create an instance of the service:
    1. Go to the [{{site.data.keyword.nlclassifiershort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/natural-language-classifier){: new_window} page in the catalog.
    1.  Sign up for a free {{site.data.keyword.Bluemix_notm}} account or log in.
    1.  Click **Create**.
- {: hide-dashboard} Copy the credentials to authenticate to your service instance:
    1.  On the **Manage** page, click **Show Credentials**.
    1.  Copy the `API Key` and `URL` values.
- {: curl} Make sure that you have the `curl` command.
    - Test whether `curl` is installed. Run the following command on the command line. If the output lists the `curl` version with SSL support, you are set for the tutorial.

        ```bash
        curl -V
        ```
        {: pre}

    - If necessary, install a version with SSL enabled from [curl.haxx.se ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://curl.haxx.se/){: new_window}. Add the location of the file to your PATH environment variables if you want to run `curl` from any command line location.
- {:go} Install the [Go SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/go-sdk){: new_window}.

    ```go
    go get -u github.com/watson-developer-cloud/go-sdk/...
    ```
    {: go}
    {: pre}

- {: java} Install the [Java SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/java-sdk){: new_window}
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

- {: javascript} Install the [Node SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/node-sdk){: new_window}

    ```bash
    npm install --save watson-developer-cloud
    ```
- {: python} Install the [Python SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/python-sdk){: new_window}

    ```bash
    pip install --upgrade watson-developer-cloud
    ```
- {: ruby} Install the [Ruby SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/ruby-sdk){: new_window}

    ```bash
    gem install ibm_watson
    ```

The following video walks you through this tutorial.
{: #video}

<iframe class="embed-responsive-item" id="youtubeplayer" title="Video walkthrough of Getting started tutorial" type="text/html" width="560" height="315" src="https://www.youtube.com/embed/SUj826ybCdU?rel=0" webkitallowfullscreen mozallowfullscreen allowfullscreen gesture="media" allow="encrypted-media"></iframe>

## Step 1: Create and train a classifier
{: #create-train}

The classifier learns from examples before it can return information for texts that it hasn't seen before. The example data is referred to as "training data." You upload the training data when you create a classifier.

1.  Download the two sample files:
    - The <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a> is the same as was used with the [demo ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://natural-language-classifier-demo.ng.bluemix.net/){:new_window}. The file is in a CSV format in two columns. The first column is the text input. The second column is the class for that text: temperature or condition. View the file to see the entries.
    - The <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/metadata.json" download="metadata.json">metadata.json</a> file specifies the language of the data (`en`) and includes a name to identify the classifier.
1.  Issue the following command to call the **Create classifier** method, which uploads the training data and creates an English language classifier with the name, "TutorialClassifier":
    - {: hide-dashboard} Replace `{apikey}` and `{url}` with the credentials that you copied in the prerequisites.
    - Modify the location of `training_data` and `training_metadata` to point to where you saved the two sample files.

    ```bash
    curl -i -u "apikey:{apikey}"{: apikey} \
    -F training_data=@weather_data_train.csv \
    -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" \
    "{url}/v1/classifiers"{: url}
    ```
    {: pre}
    {: curl}

    Windows users: Replace the backslash (`\`) at the end of each line with a caret (`^`). Make sure there are no trailing spaces.
    {: tip}

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

    The response includes a new classifier ID and status, as in the following example.

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

    Training begins immediately and must finish before you can query the classifier.
1.  Check the training status periodically until you see a status of `Available`. With this sample data, training takes about 6 minutes:

    Issue a call to the **Get information about a classifier** method to retrieve the status of the classifier. <span class="hide-dashboard">Replace `{apikey}` and `{url}` with the credentials that you copied in the prerequisites.</span> Replace `{classifier_id}` with your information.

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

## Step 2: Classify text

Now that the classifier is trained, you can query it.

1.  Classify some weather-related questions to review how your newly trained classifier responds. Here is an example call.
    - {: hide-dashboard} Replace `{apikey}` and `{url}` with the credentials that you copied in the prerequisites.
    - Replace `{classifier_id}` with your information.

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

    The API returns a response that includes the name of the class for which the classifier has the highest confidence. Other class-confidence pairs are listed in descending order of confidence:

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

    The confidence value represents a percentage, and higher values represent higher confidences. The response includes up to 10 classes.

    If you have fewer than 10 classes in your training data, the sum of all confidence values is 100%. In this sample training data, only two classes are defined, so only two can be returned.
1.  Review the top class for the questions to see how the classifier is predicting them.

    Here are some other sample questions to classify:

    - Is it hot outside?
    - Will it be windy?
    - Will we see some sun?
    - What is the expected high for today?
    - Will it be foggy tomorrow morning?

    One of the sample questions includes a term ("foggy") that the classifier isn't trained on. The classifier can score well with these "missing" terms without your having to do extra work to identify them. Try other questions that include words that are not in the training data, for example, "sleet" or "storm."

You're done! You created, trained, and queried a classifier in the {{site.data.keyword.nlclassifiershort}} service.

This tutorial classifies a single phrase. {{site.data.keyword.nlclassifiershort}} also supports classifying multiple phrases in a single call. For details, see the **Classify multiple phrases** in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){: new_window}.
{: tip}

## Delete the tutorial classifier

So that you can create classifiers for your own use and with your own training data, you might want to delete this classifier from the tutorial.

- {: hide-dashboard} Replace `{apikey}` and `{url}` with the credentials that you copied in the prerequisites.
- Replace `{classifier_id}` with your information.

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

The response ifs an empty JSON object.

## Next steps
You have a basic understanding of how to use {{site.data.keyword.nlclassifiershort}}. Now dive deeper:

- This tutorial uses an API key to authenticate. For production uses, review the IAM service API keys [best practices](/docs/services/watson/apikey-bp.html#api-bp).
- Learn how to [prepare your data](/docs/services/natural-language-classifier/using-your-data.html) to train a classifier.
- {: curl} Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}
- {: go} Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-classifier?language=go){: new_window}.
- {: java} Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-classifier?language=java){: new_window}.
- {: javascript} Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-classifier?language=node){: new_window}.
- {: python} Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-classifier?language=python){: new_window}.
- {: ruby} Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-classifier?language=ruby){: new_window}.
- Explore the [sample apps](/docs/services/natural-language-classifier/sample-applications.html) for example uses.
