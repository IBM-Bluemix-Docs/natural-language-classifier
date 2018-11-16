---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:curl: #curl .ph data-hd-programlang='curl'}
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

{{site.data.keyword.nlclassifierfull}} can help your application understand the language of short texts and make predictions about how to handle them. A classifier learns from your example data and then can return information for texts that it is not trained on.
{:shortdesc}

You can create and train a classifier in less than 15 minutes.

## Before you begin
{: #prerequisites}
{: hide-dashboard}

- Create an instance of the service:
    1.  Go to the [{{site.data.keyword.nlclassifiershort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/natural-language-classifier){: new_window} page in the {{site.data.keyword.cloud_notm}} Catalog.
    1.  Sign up for a free {{site.data.keyword.cloud_notm}} account or log in.
    1.  Click **Create**.
- Copy the credentials to authenticate to your service instance:
    1.  Click **Show** to view your credentials.
    1.  Copy the `API Key` and `Url` values.
{: hide-dashboard}}

The following video walks you through this tutorial.
{: #video}

<iframe class="embed-responsive-item" id="youtubeplayer" title="Video walkthrough of Getting started tutorial" type="text/html" width="560" height="315" src="https://www.youtube.com/embed/SUj826ybCdU?rel=0" webkitallowfullscreen mozallowfullscreen allowfullscreen gesture="media" allow="encrypted-media"></iframe>

## Step 1: Create and train a classifier
{: #create-train}

The classifier learns from examples before it can return information for texts that it hasn't seen before. The example data is referred to as "training data." You upload the training data when you create a classifier.

1.  Download the sample <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a>. This is the same training data that is used in the [demo ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://natural-language-classifier-demo.ng.bluemix.net/){:new_window}.

    The file is in a CSV format in two columns. The first column is the text input. The second column is the class for that text: temperature or condition. View the file to see the entries.
1.  Issue the following command to call the `POST /v1/classifiers/` method, which uploads the training data and creates the classifier:
    - {: hide-dashboard}Replace `{apikey_value}` and `{url}` with the credentials that you copied in the prerequisites.
    - Modify the location of the training data to point to where you saved the `weather_data_train.csv` file.

    ```bash
    curl -i --user "apikey:{apikey_value}"{: apikey} \
    -F training_data=@{path_to_file}/weather_data_train.csv \
    -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" \
    "{url}/v1/classifiers"{: url}
    ```
    {: pre}

    The response includes a new classifier ID and status. For example:

    ```json
    {
      "name": "TutorialClassifier",
      "language": "en",
      "status": "Training",
      "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/10D41B-nlc-1",
      "classifier_id": "10D41B-nlc-1",
      "created": "2017-05-28T18:01:57.393Z",
      "status_description": "The classifier instance is in its training phase, not yet ready to accept classify requests"
    }
    ```

    Training begins immediately and must finish before you can query the classifier.
1.  Check the training status periodically until you see a status of `Available`. With this sample data, training takes about 6 minutes:
    - Issue a call to the `GET /v1/classifiers/{classifier_id}` method to retrieve the status of the classifier. In the following example, replace `{apikey_value}`, `{url}`, and `{classifier_id}` with your information:

        ```bash
        curl --user "apikey:{apikey_value}"{: apikey} \
        "{url}/v1/classifiers/{classifier_id}"{: url}
        ```
        {: pre}

## Step 2: Classify text

Now that the classifier is trained, you can query it.

1.  Classify some weather-related questions to review how your newly trained classifier responds. Here is an example call.<span class="hide-dashboard">Replace `{apikey_value}`, `{url}`, and `{classifier_id}` with your information.</span>

    ```bash
    curl -G --user "apikey:{apikey_value}"{: apikey} \
    "{url}/v1/classifiers/{classifier_id}/classify"{: url} \
    --data-urlencode "text=How hot will it be today?"
    ```
    {: pre}

    The API returns a response that includes the name of the class for which the classifier has the highest confidence. Other class-confidence pairs are listed in descending order of confidence:

    ```json
    {
      "classifier_id": "10D41B-nlc-1",
      "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1",
      "text": "How hot will it be today?",
      "top_class": "temperature",
      "classes": [
        {
          "class_name": "temperature",
          "confidence": 0.9998201258549781
        },
        {
          "class_name": "conditions",
          "confidence": 0.00017987414502176904
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

This tutorial classifies a single phrase. {{site.data.keyword.nlclassifiershort}} also supports classifying multiple phrases in a single call. For details, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){: new_window}.
{: tip}

## Delete the tutorial classifier

So that you can create classifiers for your own use and with your own training data, you might want to delete this classifier from the tutorial. To delete the classifier, call the `DELETE /classifiers/{classifier_id}` method.

Replace `{apikey_value}`, `{url}`, and `{classifier_id}` with your information in the following command.
{: hide-dashboard}

```bash
curl -X DELETE --user "apikey:{apikey_value}" \
"{url}/v1/classifiers/{classifier_id}"{: url}
```
{: pre}

The response to the command is an empty JSON object.

## Next steps
You have a basic understanding of how to use {{site.data.keyword.nlclassifiershort}}. Now dive deeper:

- This tutorial uses an API key to authenticate. For production uses, review the IAM service API keys [best practices](/docs/services/watson/apikey-bp.html#api-bp).
- Learn how to [prepare your data](/docs/services/natural-language-classifier/using-your-data.html) to train a classifier
- Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}
- Explore the [Sample apps](/docs/services/natural-language-classifier/sample-applications.html) for example uses
