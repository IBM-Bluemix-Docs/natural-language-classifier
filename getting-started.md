---

copyright:
  years: 2015, 2020
lastupdated: "2020-01-30"

keywords: examples,natural language classifier,classifier,classes,texts,nlc,NaturalLanguageClassifier

subcollection: natural-language-classifier

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:curl: .ph data-hd-programlang='curl'}
{:go: .ph data-hd-programlang='go'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:unity: .ph data-hd-programlang='unity'}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}

# Getting started with {{site.data.keyword.nlclassifiershort}}
{: #natural-language-classifier}

{{site.data.keyword.nlclassifierfull}} can help your application understand the language of short texts and make predictions about how to handle them. A classifier learns from your example data and then can return information for texts that it is not trained on. You can create and train this classifier in less than 15 minutes.
{:shortdesc}

To work in a graphical interface, use <span class="hide-dashboard">[{{site.data.keyword.DSX}}](https://dataplatform.cloud.ibm.com/registration/stepone?context=wdp){: external}</span><span class="hide-in-docs">[{{site.data.keyword.DSX}}](tooling-url){: external}</span>, and follow [Building a classifier](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/nlc-create.html?audience=wdp&context=analytics){: external} in the docs.
{: tooling-url}
{: tip}

## Before you begin
{: #prerequisites}

- {: hide-dashboard} Create an instance of the service:
    1.  Go to the [{{site.data.keyword.nlclassifiershort}}](https://{DomainName}/catalog/natural-language-classifier){: external} page in the catalog.
    1.  Sign up for a free {{site.data.keyword.Bluemix_notm}} account or log in.
    1.  Click **Create**.
- {: hide-dashboard} Copy the credentials to authenticate to your service instance:
    1.  On the **Manage** page, click **Show Credentials**.
    1.  Copy the `API Key` and `URL` values.
- {: curl} Make sure that you have the `curl` command.
    - Test whether `curl` is installed. Run the following command on the command line. If the output lists the `curl` version with SSL support, you are set for the tutorial.

        ```sh
        curl -V
        ```
        {: pre}

    - If necessary, install a version with SSL enabled from [curl.haxx.se](https://curl.haxx.se/){: external}. Add the location of the file to your PATH environment variables if you want to run `curl` from any command-line location.
- {: dotnet-standard} Install the [.NET SDK](https://github.com/watson-developer-cloud/dotnet-standard-sdk){: external}.
    - {: dotnet-standard} Package Manager

        ```sh
        Install-Package IBM.Watson.NaturalLanguageClassifier.v1 -Version 4.2.1
        ```
        {: codeblock}

    - {: dotnet-standard} .NET CLI

        ```sh
        dotnet add package IBM.Watson.NaturalLanguageClassifier.v1 -version 4.2.1
        ```
        {: pre}

    - {: dotnet-standard} PackageReference

        ```xml
        <PackageReference Include="IBM.Watson.NaturalLanguageClassifier.v1" Version="4.2.1" />
        ```
        {: codeblock}
- {:go} Install the [Go SDK](https://github.com/watson-developer-cloud/go-sdk){: external}.

    ```go
    go get -u github.com/watson-developer-cloud/go-sdk@v1
    ```
    {: go}
    {: pre}

- {: java} Install the [Java SDK](https://github.com/watson-developer-cloud/java-sdk){: external}
    - {: java} Maven

        ```xml
        <dependency>
          <groupId>com.ibm.watson</groupId>
          <artifactId>ibm-watson</artifactId>
          <version>[8,9)</version>
        </dependency>
        ```
        {: codeblock}

    - {: java} Gradle

        ```sh
        compile 'com.ibm.watson:ibm-watson:8.+'
        ```
        {:pre}
- {: javascript} Install the [Node SDK](https://github.com/watson-developer-cloud/node-sdk){: external}

    ```sh
        npm install ibm-watson@^5
    ```
    {:pre}
- {: python} Install the [Python SDK](https://github.com/watson-developer-cloud/python-sdk){: external}

    ```sh
    pip install --upgrade "ibm-watson>=4.0.1"
    ```
    {:pre}
- {: ruby} Install the [Ruby SDK](https://github.com/watson-developer-cloud/ruby-sdk){: external}

    ```sh
    gem install ibm_watson
    ```
    {:pre}
- {: unity} Download the [Unity SDK](https://github.com/watson-developer-cloud/unity-sdk){: external} and the [Unity SDK Core](https://github.com/IBM/unity-sdk-core){: external}.

    The IBM Watson Unity SDK has the following requirements.

    - The SDK requires Unity version 2018.2 or later to support TLS 1.2. Set the project settings for both the **Scripting Runtime Version** and the **Api Compatibility Level** to `.NET 4.x Equivalent`.
    - The SDK does not support the WebGL projects. Change your build settings to any platform except `WebGL`.

The following video walks you through this tutorial.
{: #video}

<iframe class="embed-responsive-item" id="tutorial-youtubeplayer" title="Video walkthrough of Getting started tutorial" type="text/html" width="560" height="315" src="https://www.youtube.com/embed/SUj826ybCdU?rel=0" webkitallowfullscreen mozallowfullscreen allowfullscreen gesture="media" allow="encrypted-media"></iframe>

## Step 1: Create and train a classifier
{: #create-train}

The classifier learns from examples before it can return information for texts that it hasn't seen before. The example data is referred to as "training data." You upload the training data when you create a classifier.

1.  Download the two sample files:
    - The <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a> is the same as was used with the [demo](https://ibm.biz/Bdzqug){: external}. The file is in a CSV format in two columns. The first column is the text input. The second column is the class for that text: temperature or condition. View the file to see the entries.
    - The <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/metadata.json" download="metadata.json">metadata.json</a> file specifies the language of the data (`en`) and includes a name to identify the classifier.
1.  Issue the following call to the **Create classifier** method, which uploads the training data and creates an English language classifier with the name, "TutorialClassifier":
    - {: hide-dashboard} Replace `{apikey}` and `{url}` with the credentials that you copied in the prerequisites.
    - Modify the location of `training_data`{: curl} `trainingData`{: dotnet-standard} `TrainingData`{: go} `trainingData`{: java} `trainingData`{: javascript} `training_data`{: python} `training_data`{: ruby} `trainingData`{: unity} and `training_metadata`{:curl} `trainingMetadata`{: dotnet-standard} `TrainingMetadata`{: go} `trainingMetadata`{: java} `trainingMetadata`{: javascript} `training_metadata`{: python} `training_metadata`{: ruby} `trainingMetadata`{: unity} to point to where you saved the two sample files.

    ```sh
    curl -i -u "apikey:{apikey}"{: apikey} \
    -F training_data=@weather_data_train.csv \
    -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" \
    "{url}/v1/classifiers"{: url}
    ```
    {: pre}
    {: curl}

    Windows users: Replace the backslash (`\`) at the end of each line with a caret (`^`). Make sure that there are no trailing spaces.
    {: tip}
    {: curl}

    ```cs
    IamAuthenticator authenticator = new IamAuthenticator(
        apikey: "{apikey}"{: apikey}
        );

    NaturalLanguageClassifierService naturalLanguageClassifier = new NaturalLanguageClassifierService(authenticator);
    naturalLanguageClassifier.SetServiceUrl("{url}"{: url});

    DetailedResponse<Classifier> result = null;
    using (FileStream trainingDataFile = File.OpenRead("./weather_data_train"), metadataFile = File.OpenRead("./metadata.json"))
    {
        using (MemoryStream trainingData = new MemoryStream(), metadata = new MemoryStream())
        {
            trainingDataFile.CopyTo(trainingData);
            metadataFile.CopyTo(metadata);
            result = service.CreateClassifier(
                trainingMetadata: metadata,
                trainingData: trainingData
                );
        }
    }

    Console.WriteLine(result.Response);
    ```
    {: dotnet-standard}
    {: codeblock}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "os"
      "github.com/IBM/go-sdk-core/core"
      "github.com/watson-developer-cloud/go-sdk/naturallanguageclassifierv1"
    )

    func main() {
      authenticator := &core.IamAuthenticator{
        ApiKey: "{apikey}"{: apikey},
      }

      options := &naturallanguageclassifierv1.NaturalLanguageClassifierV1Options{
        Authenticator: authenticator,
      }

      naturalLanguageClassifier, naturalLanguageClassifierErr := naturallanguageclassifierv1.NewNaturalLanguageClassifierV1(options)

      if naturalLanguageClassifierErr != nil {
        panic(naturalLanguageClassifierErr)
      }

      naturalLanguageClassifier.SetServiceURL("{url}"{: url})

      metadata, metadataErr := os.Open("./metadata.json")
      if metadataErr != nil {
        panic(metadataErr)
      }
      defer metadata.Close()
      trainingData, trainingDataErr := os.Open("./train.csv")
      if trainingDataErr != nil {
        panic(trainingDataErr)
      }
      defer trainingData.Close()
      result, response, responseErr := naturalLanguageClassifier.CreateClassifier(
        &naturallanguageclassifierv1.CreateClassifierOptions{
          TrainingData: trainingData,
          TrainingMetadata: metadata,
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: go}
    {: codeblock}

    ```java
    import java.io.File;
    import java.io.FileNotFoundException;

    import com.ibm.cloud.sdk.core.service.security.IamOptions;
    import com.ibm.watson.natural_language_classifier.v1.NaturalLanguageClassifier;
    import com.ibm.watson.natural_language_classifier.v1.model.Classifier;
    import com.ibm.watson.natural_language_classifier.v1.model.CreateClassifierOptions;

    public class CreateClassifier {

      public static void main(String[] args) throws FileNotFoundException {

        IamAuthenticator authenticator = new IamAuthenticator("{apikey}"{: apikey});
        NaturalLanguageClassifier naturalLanguageClassifier = new NaturalLanguageClassifier(authenticator);
        naturalLanguageClassifier.setServiceUrl("{url}"{: url});

        CreateClassifierOptions createOptions = new CreateClassifierOptions.Builder()
          .trainingMetadata("./metadata.json")
          .trainingData(new File("./weather_data_train.csv"))
          .build();
        Classifier classifier = naturalLanguageClassifier.createClassifier(createOptions)
          .execute().getResult();
          System.out.println(classifier);
      }

    }
    ```
    {: java}
    {: codeblock}

    ```javascript
    const fs = require('fs');
    const NaturalLanguageClassifierV1 = require('ibm-watson/natural-language-classifier/v1');
    const { IamAuthenticator } = require('ibm-watson/auth');

    const naturalLanguageClassifier = new NaturalLanguageClassifierV1({
      authenticator: new IamAuthenticator({
        apikey: '{apikey}'{: apikey},
      }),
      url: '{url}'{: url},
    });

    const createClassifierParams = {
      trainingMetadata: JSON.stringify({
        name: 'TutorialClassifier',
        language: 'en',
      }),
      trainingData: fs.createReadStream('./weather_data_train.csv'),
    };

    naturalLanguageClassifier.createClassifier(createClassifierParams)
      .then(response => {
        const classifier = response.result;
        console.log(JSON.stringify(classifier, null, 2));
      })
      .catch(err => {
        console.log('error:', err);
      });
    ```
    {: javascript}
    {: codeblock}

    ```python
    import json
    from ibm_watson import NaturalLanguageClassifierV1
    from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

    authenticator = IAMAuthenticator('{apikey}'{: apikey})
    natural_language_classifier = NaturalLanguageClassifierV1(
        authenticator=authenticator
    )

    natural_language_classifier.set_service_url('{url}'{: url})

    with open('./weather_data_train.csv', 'rb') as training_data:
        classifier = natural_language_classifier.create_classifier(
        training_data=training_data,
        training_metadata='{"name": "TutorialClassifier","language": "en"}'
      ).get_result()
    print(json.dumps(classifier, indent=2))
    ```
    {: python}
    {: codeblock}

    ```ruby
    require "json"
    require "ibm_watson/authenticators"
    require "ibm_watson/natural_language_classifier_v1"
    include IBMWatson

    authenticator = Authenticators::IamAuthenticator.new(
      apikey: "{apikey}"{: apikey}
    )
    natural_language_classifier = NaturalLanguageClassifierV1.new(
      authenticator: authenticator
    )
    natural_language_classifier.service_url = "{url}"{: url}

    File.open("./weather_data_train.csv") do |training_data|
      classifier = natural_language_classifier.create_classifier(
          training_data: training_data,
          training_metadata: {name: "TutorialClassifier", language: "en"}
        )
      puts JSON.pretty_generate(classifier.result)
    end
    ```
    {: ruby}
    {: codeblock}

    ```cs
    var authenticator = new IamAuthenticator(
        apikey: "{apikey}"{: apikey}
    );

    while (!authenticator.CanAuthenticate())
        yield return null;

    var naturalLanguageClassifier = new NaturalLanguageClassifierService(authenticator);
    naturalLanguageClassifier.SetServiceUrl("{url}"{: url});

    ClassifiedImages createClassifierResponse = null;
    using (FileStream trainingDataFile = File.OpenRead("./weather_data_train.csv"))
    {
        using (FileStream metadataFile = File.OpenRead("./metadata.json"))
        {
            using (MemoryStream trainingData = new MemoryStream())
            {
                using (MemoryStream metadata = new MemoryStream())
                {
                    trainingDataFile.CopyTo(trainingData);
                    metadataFile.CopyTo(metadata);
                    service.CreateClassifier(
                        callback: (DetailedResponse<Classifier> response, IBMError error) =>
                        {
                            Log.Debug("NaturalLanguageClassifierServiceV1", "CreateClassifier result: {0}", response.Response);
                            createClassifierResponse = response.Result;
                            createdClassifierId = createClassifierResponse.ClassifierId;
                        },
                        trainingMetadata: metadata,
                        trainingData: trainingData
                    );

                    while (createClassifierResponse == null)
                        yield return null;
                }
            }
        }
    }
    ```
    {: unity}
    {: codeblock}

    The response includes a new classifier ID and status, as in the following example.

    ```json
    {
      "name": "TutorialClassifier",
      "language": "en",
      "status": "Training",
      "url" : "https://api.us-south.natural-language-classifier.watson.cloud.ibm.com/instances/df09aa83-9660-4137-9b5c-6169be1373a6/v1/classifiers/0e6935x475-nlc-2948",
      "classifier_id": "0e6935x475-nlc-2948",
      "created": "2020-01-20T16:32:17.403Z",
      "status_description": "The classifier instance is in its training phase, not yet ready to accept classify requests"
    }
    ```

    Training begins immediately and must finish before you can query the classifier.
1.  Check the training status periodically until you see a status of `Available`. With this sample data, training takes about 6 minutes:

    Issue a call to the **Get information about a classifier** method to retrieve the status of the classifier. <span class="hide-dashboard">Replace `{apikey}` and `{url}` with the credentials that you copied in the prerequisites.</span> Replace `{classifier_id}` with your information.

    ```sh
    curl -u "apikey:{apikey}"{: apikey} \
    "{url}/v1/classifiers/{classifier_id}"{: url}
    ```
    {: pre}
    {: curl}

    ```cs
    IamAuthenticator authenticator = new IamAuthenticator(
        apikey: "{apikey}"{: apikey}
        );

    NaturalLanguageClassifierService naturalLanguageClassifier = new NaturalLanguageClassifierService(authenticator);
    naturalLanguageClassifier.SetServiceUrl("{url}"{: url});

    var result = service.Classify(
        classifierId: "{classifier_id}",
        text: "How hot will it be today?"
        );

    Console.WriteLine(result.Response);
    ```
    {: dotnet-standard}
    {: codeblock}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "github.com/IBM/go-sdk-core/core"
      "github.com/watson-developer-cloud/go-sdk/naturallanguageclassifierv1"
    )

    func main() {
      authenticator := &core.IamAuthenticator{
        ApiKey: "{apikey}"{: apikey},
      }

      options := &naturallanguageclassifierv1.NaturalLanguageClassifierV1Options{
        Authenticator: authenticator,
      }

      naturalLanguageClassifier, naturalLanguageClassifierErr := naturallanguageclassifierv1.NewNaturalLanguageClassifierV1(options)

      if naturalLanguageClassifierErr != nil {
        panic(naturalLanguageClassifierErr)
      }

      naturalLanguageClassifier.SetServiceURL("{url}"{: url})

      result, response, responseErr := naturalLanguageClassifier.GetClassifier(
        &naturallanguageclassifierv1.GetClassifierOptions{
          ClassifierID: core.StringPtr("{classifier_id}"),
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: go}
    {: codeblock}

    ```java
    import com.ibm.cloud.sdk.core.service.security.IamOptions;
    import com.ibm.watson.natural_language_classifier.v1.NaturalLanguageClassifier;
    import com.ibm.watson.natural_language_classifier.v1.model.Classifier;
    import com.ibm.watson.natural_language_classifier.v1.model.GetClassifierOptions;

    public class GetClassifier {

      public static void main(String[] args) {

        IamAuthenticator authenticator = new IamAuthenticator("{apikey}"{: apikey});
        NaturalLanguageClassifier naturalLanguageClassifier = new NaturalLanguageClassifier(authenticator);
        naturalLanguageClassifier.setServiceUrl("{url}"{: url});

        GetClassifierOptions getOptions = new GetClassifierOptions.Builder()
          .classifierId("{classifier_id")
          .build();
        Classifier classifier = naturalLanguageClassifier.getClassifier(getOptions);
          .execute().getResult();
        System.out.println(classifier);
      }

    }
    ```
    {: java}
    {: codeblock}

    ```javascript
    const NaturalLanguageClassifierV1 = require('ibm-watson/natural-language-classifier/v1');
    const { IamAuthenticator } = require('ibm-watson/auth');

    const naturalLanguageClassifier = new NaturalLanguageClassifierV1({
      authenticator: new IamAuthenticator({
        apikey: '{apikey}'{: apikey},
      }),
      url: '{url}'{: url},
    });

    const getClassifierParams = {
      classifierId: '{classifier_id}',
    };

    naturalLanguageClassifier.getClassifier(getClassifierParams)
      .then(response => {
        const classifier = response.result;
        console.log(JSON.stringify(classifier, null, 2));
      })
      .catch(err => {
        console.log('error:', err);
      });
    ```
    {: javascript}
    {: codeblock}

    ```python
    import json
    from ibm_watson import NaturalLanguageClassifierV1
    from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

    authenticator = IAMAuthenticator('{apikey}'{: apikey})
    natural_language_classifier = NaturalLanguageClassifierV1(
        authenticator=authenticator
    )

    natural_language_classifier.set_service_url('{url}'{: url})

    status = natural_language_classifier.get_classifier('classifier_id').get_result()
    print (json.dumps(status, indent=2))
    ```
    {: python}
    {: codeblock}

    ```ruby
    require "json"
    require "ibm_watson/authenticators"
    require "ibm_watson/natural_language_classifier_v1"
    include IBMWatson

    authenticator = Authenticators::IamAuthenticator.new(
      apikey: "{apikey}"{: apikey}
    )
    natural_language_classifier = NaturalLanguageClassifierV1.new(
      authenticator: authenticator
    )
    natural_language_classifier.service_url = "{url}"{: url}

    status = natural_language_classifier.get_classifier(
      classifier_id: "{classifier_id}"
    )
    puts JSON.pretty_generate(status.result)
    ```
    {: ruby}
    {: codeblock}

    ```cs
    var authenticator = new IamAuthenticator(
        apikey: "{apikey}"{: apikey}
    );

    while (!authenticator.CanAuthenticate())
        yield return null;

    var naturalLanguageClassifier = new NaturalLanguageClassifierService(authenticator);
    naturalLanguageClassifier.SetServiceUrl("{url}"{: url});

    Classifier getClassifierResponse = null;
    service.GetClassifier(
        callback: (DetailedResponse<Classifier> response, IBMError error) =>
        {
            Log.Debug("NaturalLanguageClassifierServiceV1", "GetClassifier result: {0}", response.Response);
            getClassifierResponse = response.Result;
        },
        classifierId: "{classifier_id}"
    );

    while (getClassifierResponse == null)
        yield return null;
    ```
    {: unity}
    {: codeblock}

## Step 2: Classify text
{: #getting-started-classify}

Now that the classifier is trained, you can query it.

1.  Classify some weather-related questions to review how your newly trained classifier responds. Here is an example call.
    - {: hide-dashboard} Replace `{apikey}` and `{url}` with the credentials that you copied in the prerequisites.
    - Replace `{classifier_id}` with your information.

    ```sh
    curl -G -u "apikey:{apikey}"{: apikey} \
    "{url}/v1/classifiers/{classifier_id}/classify"{: url} \
    --data-urlencode "text=How hot will it be today?"
    ```
    {: pre}
    {: curl}

    ```cs
    IamAuthenticator authenticator = new IamAuthenticator(
        apikey: "{apikey}"{: apikey}
        );

    NaturalLanguageClassifierService naturalLanguageClassifier = new NaturalLanguageClassifierService(authenticator);
    naturalLanguageClassifier.SetServiceUrl("{url}"{: url});

    var result = service.Classify(
        classifierId: "{classifier_id}",
        text: "How hot will it be today?"
        );

    Console.WriteLine(result.Response);
    ```
    {: dotnet-standard}
    {: codeblock}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "github.com/IBM/go-sdk-core/core"
      "github.com/watson-developer-cloud/go-sdk/naturallanguageclassifierv1"
    )

    func main() {
      authenticator := &core.IamAuthenticator{
        ApiKey: "{apikey}"{: apikey},
      }

      options := &naturallanguageclassifierv1.NaturalLanguageClassifierV1Options{
        Authenticator: authenticator,
      }

      naturalLanguageClassifier, naturalLanguageClassifierErr := naturallanguageclassifierv1.NewNaturalLanguageClassifierV1(options)

      if naturalLanguageClassifierErr != nil {
        panic(naturalLanguageClassifierErr)
      }

      naturalLanguageClassifier.SetServiceURL("{url}"{: url})

      result, response, responseErr := naturalLanguageClassifier.Classify(
        &naturallanguageclassifierv1.ClassifyOptions{
          ClassifierID: core.StringPtr("{classifier_id}"),
          Text: core.StringPtr("How hot will it be today?"),
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: go}
    {: codeblock}

    ```java
    import com.ibm.cloud.sdk.core.service.security.IamOptions;
    import com.ibm.watson.natural_language_classifier.v1.NaturalLanguageClassifier;
    import com.ibm.watson.natural_language_classifier.v1.model.Classification;
    import com.ibm.watson.natural_language_classifier.v1.model.ClassifyOptions;

    public class Classify {

      public static void main(String[] args) {

        IamAuthenticator authenticator = new IamAuthenticator("{apikey}"{: apikey});
        NaturalLanguageClassifier naturalLanguageClassifier = new NaturalLanguageClassifier(authenticator);
        naturalLanguageClassifier.setServiceUrl("{url}"{: url});

        ClassifyOptions classifyOptions = new ClassifyOptions.Builder()
          .classifierId("{classifier_id}")
          .text("How hot will it be today?")
          .build();
        Classification classification = naturalLanguageClassifier.classify(classifyOptions)
          .execute().getResult();
        System.out.println(classification);
      }

    }
    ```
    {: java}
    {: codeblock}

    ```javascript
    const NaturalLanguageClassifierV1 = require('ibm-watson/natural-language-classifier/v1');
    const { IamAuthenticator } = require('ibm-watson/auth');

    const naturalLanguageClassifier = new NaturalLanguageClassifierV1({
      authenticator: new IamAuthenticator({
        apikey: '{apikey}'{: apikey},
      }),
      url: '{url}'{: url},
    });

    const classifyParams = {
      text: 'How hot will it be today?',
      classifierId: '{classifier_id}',
    };

    naturalLanguageClassifier.classify(classifyParams)
      .then(response => {
        const classification = response.result;
        console.log(JSON.stringify(classification, null, 2));
      })
      .catch(err => {
        console.log('error:', err);
      });
    ```
    {: javascript}
    {: codeblock}

    ```python
    import json
    from ibm_watson import NaturalLanguageClassifierV1
    from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

    authenticator = IAMAuthenticator('{apikey}'{: apikey})
    natural_language_classifier = NaturalLanguageClassifierV1(
        authenticator=authenticator
    )

    natural_language_classifier.set_service_url('{url}'{: url})

    classes = natural_language_classifier.classify(
        '{classifier_id}',
        'How hot will it be today?').get_result()
    print(json.dumps(classes, indent=2))
    ```
    {: python}
    {: codeblock}

    ```ruby
    require "json"
    require "ibm_watson/authenticators"
    require "ibm_watson/natural_language_classifier_v1"
    include IBMWatson

    authenticator = Authenticators::IamAuthenticator.new(
      apikey: "{apikey}"{: apikey}
    )
    natural_language_classifier = NaturalLanguageClassifierV1.new(
      authenticator: authenticator
    )
    natural_language_classifier.service_url = "{url}"{: url}

    classes = natural_language_classifier.classify(
      classifier_id: "{classifier_id}",
      text: "How hot will it be today?"
    )
    puts JSON.pretty_generate(classes.result)
    ```
    {: ruby}
    {: codeblock}

    ```cs
    var authenticator = new IamAuthenticator(
        apikey: "{apikey}"{: apikey}
    );

    while (!authenticator.CanAuthenticate())
        yield return null;

    var naturalLanguageClassifier = new NaturalLanguageClassifierService(authenticator);
    naturalLanguageClassifier.SetServiceUrl("{url}"{: url});

    Classification classifyResponse = null;
    service.Classify(
        callback: (DetailedResponse<Classification> response, IBMError error) =>
        {
            Log.Debug("NaturalLanguageClassifierServiceV1", "Classify result: {0}", response.Response);
            classifyResponse = response.Result;
        },
        classifierId: "{classifier_id}",
        text: "How hot will it be today?"
    );

    while (classifyResponse == null)
        yield return null;
    ```
    {: unity}
    {: codeblock}

    The API returns a response that includes the name of the class for which the classifier has the highest confidence. Other class-confidence pairs are listed in descending order of confidence:

    ```json
    {
      "classifier_id": "0e6935x475-nlc-2948",
      "url" : "https://api.us-south.natural-language-classifier.watson.cloud.ibm.com/instances/df09aa83-9660-4137-9b5c-6169be1373a6/v1/classifiers/0e6935x475-nlc-2948",
      "text": "How hot will it be today?",
      "top_class": "temperature",
      "classes": [
        {
          "class_name": "temperature",
          "confidence": 0.9929008461208898
        },
        {
          "class_name": "conditions",
          "confidence": 0.0070991538791101575
        }
      ]
    }
    ```

    The confidence value represents a percentage, and higher values represent higher confidences. The response includes up to 10 classes.

    If you have fewer than 10 classes in your training data, the sum of all confidence values is 100%. In this sample training data only two classes are defined, so only two can be returned.
1.  Review the top class for the questions to see how the classifier is predicting them.

    Here are some other sample questions to classify:

    - Is it hot outside?
    - Will it be windy?
    - Will we see some sun?
    - What is the expected high for today?
    - Will it be foggy tomorrow morning?

    One of the sample questions includes a term ("foggy") that the classifier isn't trained on. The classifier can score well with these "missing" terms without your having to do extra work to identify them. Try other questions that include words that are not in the training data, for example, "sleet" or "storm."

You're done! You created, trained, and queried a classifier in the {{site.data.keyword.nlclassifiershort}} service.

This tutorial classifies a single phrase. {{site.data.keyword.nlclassifiershort}} also supports classifying multiple phrases in a single call. For more information, see the **Classify multiple phrases** method in the [API reference](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){: external}.
{: curl}
{: tip}

This tutorial classifies a single phrase. {{site.data.keyword.nlclassifiershort}} also supports classifying multiple phrases in a single call. For more information, see the **Classify multiple phrases** method in the [API reference](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){: external}.
{: dotnet-standard}
{: tip}

This tutorial classifies a single phrase. {{site.data.keyword.nlclassifiershort}} also supports classifying multiple phrases in a single call. For more information, see the **Classify multiple phrases** method in the [API reference](https://{DomainName}/apidocs/natural-language-classifier?code=go#classify-multiple-phrases){: external}.
{: go}
{: tip}

This tutorial classifies a single phrase. {{site.data.keyword.nlclassifiershort}} also supports classifying multiple phrases in a single call. For more information, see the **Classify multiple phrases** method in the [API reference](https://{DomainName}/apidocs/natural-language-classifier?code=java#classify-multiple-phrases){: external}.
{: java}
{: tip}

This tutorial classifies a single phrase. {{site.data.keyword.nlclassifiershort}} also supports classifying multiple phrases in a single call. For more information, see the **Classify multiple phrases** method in the [API reference](https://{DomainName}/apidocs/natural-language-classifier?code=node#classify-multiple-phrases){: external}.
{: javascript}
{: tip}

This tutorial classifies a single phrase. {{site.data.keyword.nlclassifiershort}} also supports classifying multiple phrases in a single call. For more information, see the **Classify multiple phrases** method in the [API reference](https://{DomainName}/apidocs/natural-language-classifier?code=python#classify-multiple-phrases){: external}.
{: python}
{: tip}

This tutorial classifies a single phrase. {{site.data.keyword.nlclassifiershort}} also supports classifying multiple phrases in a single call. For more information, see the **Classify multiple phrases** method in the [API reference](https://{DomainName}/apidocs/natural-language-classifier?code=ruby#classify-multiple-phrases){: external}.
{: ruby}
{: tip}

This tutorial classifies a single phrase. {{site.data.keyword.nlclassifiershort}} also supports classifying multiple phrases in a single call. For more information, see the **Classify multiple phrases** method in the [API reference](https://{DomainName}/apidocs/natural-language-classifier?code=unity#classify-multiple-phrases){: external}.
{: unity}
{: tip}

## Delete the tutorial classifier
{: #getting-started-delete}

So that you can create classifiers for your own use and with your own training data, you might want to delete this classifier from the tutorial.

- {: hide-dashboard} Replace `{apikey}` and `{url}` with the credentials that you copied in the prerequisites.
- Replace `{classifier_id}` with your information.

```sh
curl -X DELETE -u "apikey:{apikey}"{: apikey} \
"{url}/v1/classifiers/{classifier_id}"{: url}
```
{: pre}
{: curl}

```cs
IamAuthenticator authenticator = new IamAuthenticator(
    apikey: "{apikey}"{: apikey}
    );

NaturalLanguageClassifierService naturalLanguageClassifier = new NaturalLanguageClassifierService(authenticator);
naturalLanguageClassifier.SetServiceUrl("{url}"{: url});

var result = service.DeleteClassifier(
    classifierId: "{classifier_id}"
    );

Console.WriteLine(result.Response);
```
{: dotnet-standard}
{: codeblock}

```go
package main

import (
  "github.com/IBM/go-sdk-core/core"
  "github.com/watson-developer-cloud/go-sdk/naturallanguageclassifierv1"
)


func main() {
  authenticator := &core.IamAuthenticator{
    ApiKey: "{apikey}"{: apikey},
  }

  options := &naturallanguageclassifierv1.NaturalLanguageClassifierV1Options{
    Authenticator: authenticator,
  }

  naturalLanguageClassifier, naturalLanguageClassifierErr := naturallanguageclassifierv1.NewNaturalLanguageClassifierV1(options)

  if naturalLanguageClassifierErr != nil {
    panic(naturalLanguageClassifierErr)
  }

  naturalLanguageClassifier.SetServiceURL("{url}")

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
import com.ibm.cloud.sdk.core.service.security.IamOptions;
import com.ibm.watson.natural_language_classifier.v1.NaturalLanguageClassifier;
import com.ibm.watson.natural_language_classifier.v1.model.DeleteClassifierOptions;

public class DeleteClassifier {

  public static void main(String[] args) {

    IamAuthenticator authenticator = new IamAuthenticator("{apikey}"{: apikey});
    NaturalLanguageClassifier naturalLanguageClassifier = new NaturalLanguageClassifier(authenticator);
    naturalLanguageClassifier.setServiceUrl("{url}"{: url});

    DeleteClassifierOptions deleteOptions = new DeleteClassifierOptions.Builder()
      .classifierId("{classifier_id}")
      .build();
    naturalLanguageClassifier.deleteClassifier(deleteOptions).execute();
  }

}
```
{: java}
{: codeblock}

```javascript
const NaturalLanguageClassifierV1 = require('ibm-watson/natural-language-classifier/v1');
const { IamAuthenticator } = require('ibm-watson/auth');

const naturalLanguageClassifier = new NaturalLanguageClassifierV1({
  authenticator: new IamAuthenticator({
    apikey: '{apikey}'{: apikey},
  }),
  url: '{url}'{: url}
});

const deleteClassifierParams = {
  classifierId: '{classifier_id}',
};

naturalLanguageClassifier.deleteClassifier(deleteClassifierParams)
  .then(result => {
    console.log(JSON.stringify(result, null, 2));
  })
  .catch(err => {
    console.log('error:', err);
  });
```
{: javascript}
{: codeblock}

```python
from ibm_watson import NaturalLanguageClassifierV1
from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

authenticator = IAMAuthenticator('{apikey}'{: apikey})
natural_language_classifier = NaturalLanguageClassifierV1(
    authenticator=authenticator
)

natural_language_classifier.set_service_url('{url}'{: url})

natural_language_classifier.delete_classifier('{classifier_id}')
```
{: python}
{: codeblock}

```ruby
require "ibm_watson/authenticators"
require "ibm_watson/natural_language_classifier_v1"
include IBMWatson

authenticator = Authenticators::IamAuthenticator.new(
  apikey: "{apikey}"{: apikey}
)
natural_language_classifier = NaturalLanguageClassifierV1.new(
  authenticator: authenticator
)
natural_language_classifier.service_url = "{url}"{: url}

natural_language_classifier.delete_classifier(
  classifier_id: "{classifier_id}"
)
```
{: ruby}
{: codeblock}

```cs
var authenticator = new IamAuthenticator(
    apikey: "{apikey}"{: apikey}
);

while (!authenticator.CanAuthenticate())
    yield return null;

var naturalLanguageClassifier = new NaturalLanguageClassifierService(authenticator);
naturalLanguageClassifier.SetServiceUrl("{url}"{: url});

object deleteClassifierResponse = null;
service.DeleteClassifier(
    callback: (DetailedResponse<object> response, IBMError error) =>
    {
        Log.Debug("NaturalLanguageClassifierServiceV1", "DeleteClassifier result: {0}", response.Response);
        deleteClassifierResponse = response.Result;
    },
    classifierId: "{classifier_id}"
);

while (deleteClassifierResponse == null)
    yield return null;
```
{: unity}
{: codeblock}

## Next steps
{: #getting-started-next-steps}

You have a basic understanding of how to use {{site.data.keyword.nlclassifiershort}}. Now dive deeper:

- This tutorial uses an API key to authenticate. For production uses, review the IAM service API keys [best practices](/docs/watson?topic=watson-iam#gs-iam-api-bp).
- Learn how to [prepare your data](/docs/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data) to train a classifier.
- {: curl} Read about the API in the [API reference](https://{DomainName}/apidocs/natural-language-classifier){: external}
- {: dotnet-standard} Read about the API in the [API reference](https://{DomainName}//apidocs/natural-language-classifier?code=dotnet-standard){: external}.
- {: go} Read about the API in the [API reference](https://{DomainName}/apidocs/natural-language-classifier?code=go){: external}.
- {: java} Read about the API in the [API reference](https://{DomainName}/apidocs/natural-language-classifier?code=java){: external}.
- {: javascript} Read about the API in the [API reference](https://{DomainName}/apidocs/natural-language-classifier?code=node){: external}.
- {: python} Read about the API in the [API reference](https://{DomainName}/apidocs/natural-language-classifier?code=python){: external}.
- {: ruby} Read about the API in the [API reference](https://{DomainName}/apidocs/natural-language-classifier?code=ruby){: external}.
- {: unity} Read about the API in the [API reference](https://{DomainName}/apidocs/natural-language-classifier?code=unity){: external}.
- Explore the [sample apps](/docs/natural-language-classifier?topic=natural-language-classifier-sample-applications#sample-applications) for example uses.
