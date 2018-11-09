---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

<!-- Link definitions -->

[cloud-dashboard-watson]: https://console.{DomainName}/dashboard/apps?category=watson
[watson-studio-reg]: https://dataplatform.ibm.com/registration/stepone?context=wdp
[watson-studio-product-page]: https://www.ibm.com/cloud/watson-studio

# Release notes

The following new features and changes to the service are available.
{: shortdesc}

## Beta features
{: #beta}

{{site.data.keyword.IBM_notm}} releases services, features, and language support for your evaluation that are classified as beta. These features might be unstable, might change frequently, and might be discontinued with short notice. Beta features also might not provide the same level of performance or compatibility that generally available features provide and are not intended for use in a production environment. Beta features are supported only on [IBM Developer Answers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/natural-language-classifier.html){: new_window}.

## Changes
{: #changelog}

The following new features and changes to the service are available.

### 9 November 2018
{: #9November2018}

**New Tokyo location**

- You can now create {{site.data.keyword.nlclassifiershort}} service instances that are hosted in the Tokyo location.

### 30 October 2018
{: #30october2018}

On 30 October 2018, the US South and Germany locations transitioned to using token-based Identity and Access Management (IAM) authentication. {{site.data.keyword.nlclassifiershort}} migrated each location on the following dates:

- US South (Dallas): 30 October 2018
- Germany (Frankfurt): 30 October 2018
- US East: 12 October 2018

The migration to IAM authentication affects new and existing service instances differently:

- With *new* service instances that you create in the locations and dates listed earlier, you authenticate to the API by using IAM. You can pass either a bearer token in an Authorization header or an API key. Tokens support authenticated requests without embedding service credentials in every call. API keys use basic authentication.

    When you use any of the {{site.data.keyword.watson}} SDKs, you can pass the API key and let the SDK manage the lifecycle of the tokens.
- With *existing* service instances that you created before the indicated dates, you continue to authenticate by providing the username and password for the service instance. You can use these services until October 2019, when you must migrate to IAM.

More information:
- To learn which authentication process to use with your service instance, view the service credentials by clicking the instance on the {{site.data.keyword.cloud_notm}} [Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/dashboard/apps?watson){: new_window}.
- For more information and examples about the SDK, see [Authentication ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/apidocs/natural-language-classifier?language=java#authentication){: new_window} in the API reference.
- For more information about using IAM tokens with Watson services, see [Authenticating with IAM tokens](/docs/services/watson/getting-started-iam.html).
- For more information about using IAM API keys with Watson services, see [IAM service API keys](/docs/services/watson/apikey-bp.html).
- For more information about migrating Cloud Foundry instances, see [Migrating Cloud Foundry service instances to a resource group](/docs/resources/instance_migration.html).

### 19 September 2018
{: #19september2018}

**Rate limiting introduced**

- API calls are now limited to 1500 requests per minute per service instance. If you exceed the limit, the HTTP status code `429 Too Many Requests` is returned.

### 7 August 2018
{: #07august2018}

**Classic toolkit replaced**

The classic toolkit is shut down as of August 7, 2018 and is replaced by  [{{site.data.keyword.DSX}} ![External link icon](../../icons/launch-glyph.svg "External link icon")][watson-studio-reg]{: new_window}.

You can [migrate](/docs/services/natural-language-classifier/tool-overview.html#migrating) the training data for classifiers created outside of {{site.data.keyword.DSX}} until September 30, 2018. After you migrate, you can easily update the training data and create another classifier within {{site.data.keyword.DSX}}.

### 2 August 2018
{: #02august2018}

**Migrate your training data to {{site.data.keyword.DSX}}**

You can now [migrate](/docs/services/natural-language-classifier/tool-overview.html#migrating) the training data for classifiers created outside of {{site.data.keyword.DSX}}. After you migrate, you can easily update the training data and create another classifier within {{site.data.keyword.DSX}}.

You can migrate data until September 30, 2018.

### 6 July 2018
{: #06july2018}

**New beta tool available: {{site.data.keyword.DSX}}**

{{site.data.keyword.DSX}} is the new integrated environment that includes a replacement for the earlier classic {{site.data.keyword.nlclassifiershort}} toolkit. To get started with {{site.data.keyword.DSX}}, click **Launch tool** from a {{site.data.keyword.nlclassifiershort}} service instance dashboard. For details, see [Managing classifiers with {{site.data.keyword.DSX}}](/docs/services/natural-language-classifier/tool-overview.html#studio).

{{site.data.keyword.DSX}} supports not only {{site.data.keyword.nlclassifiershort}} but also {{site.data.keyword.visualrecognitionshort}} and many other {{site.data.keyword.cloud_notm}} services and resources. {{site.data.keyword.DSX}} provides a collaborative environment in the cloud. With {{site.data.keyword.DSX}}, developers, subject matter experts, data scientists, and others can build and train {{site.data.keyword.nlclassifiershort}} and other AI models. You can also use {{site.data.keyword.DSX}} to test your classifiers.

You can use {{site.data.keyword.DSX}} with all your existing {{site.data.keyword.nlclassifiershort}} instances and classifiers. The classic toolkit remains available until August 7, 2018.

### 8 June 2018
{: #08june2018}

**Download your training data for the new tool**

The existing {{site.data.keyword.nlclassifiershort}} classic toolkit is scheduled to shut down July 31, 2018. The planned replacement for the toolkit is **{{site.data.keyword.DSX}}**, the new integrated environment. [{{site.data.keyword.DSX}} ![External link icon](../../icons/launch-glyph.svg "External link icon")][watson-studio-reg]{: new_window} already supports {{site.data.keyword.visualrecognitionshort}} and other {{site.data.keyword.cloud_notm}} services and resources.

We expect that all of your existing classifiers will be available in {{site.data.keyword.DSX}}. However, if you want to make sure that you can re-create your existing classifiers, download the training data from the classic toolkit before July 31, 2018.

For those who use the [API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/apidocs/natural-language-classifier){: new_window} directly, there is no change with the tool migration.

### 16 March 2018
{: #16march2018}

- **Classify multiple phrases**

    A new **Classify multiple phrases** method is available that supports sending up to 30 text phrases in one request. The `POST /v1/classifiers/{classifier_id}/classify_collection` method supports classifying phrases in the same languages as for the original method, except for Japanese, which launches as a beta feature.

    For details about the API call, see the **Classify multiple phrases** method in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}.

- **Train with larger data sets**

    You can now include up to 20,000 records in your training data. Classifier training is now enhanced by IBM Deep Learning as a Service. This offering is a neural network training infrastructure that uses an elastic cluster of graphics processing units (GPU) to handle larger data sets. The maximum size of the training data remains at 15,000 records for users in the Frankfurt location or users with {{site.data.keyword.Bluemix_dedicated_notm}}.

### 10 July 2017
{: #10july2017}

**Additional languages:** The service now supports Korean in addition to Arabic, English, French, German, Japanese, Italian, Portuguese, and Spanish. The language of the training data must match the language of the text that you intend to classify.

For details about languages, see [Using your own data](/docs/services/natural-language-classifier/using-your-data.html#languages). For details about the API call, see the `Create classifier` method in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/apidocs/natural-language-classifier){:new_window}.

### 06 April 2016
{: #06april2016}

**Additional languages:** The service now supports German in addition to Arabic, English, French, Japanese, Italian, Portuguese, and Spanish. The language of the training data must match the language of the text that you intend to classify.

### 29 February 2016
{: #29february2016}

**Additional languages:** The service now supports Japanese in addition to Arabic, English, French, Italian, Portuguese, and Spanish.

### 7 December 2015
{: #07december2015}

**Additional languages:** The service now supports Arabic, French, and Italian in addition to English, Portuguese, and Spanish.

### 16 November 2015
{: #16november2015}

**Additional languages:** The service now supports Portuguese and  Spanish languages in addition to English.
