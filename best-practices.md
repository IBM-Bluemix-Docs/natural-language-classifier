---

copyright:
  years: 2015, 2020
lastupdated: "2020-04-22"

keywords: language support,supported languages,best practices,guidelines,supported languages,language support

subcollection: natural-language-classifier

---

{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}
{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}

# Best practices for classifiers
{: #best-practices-overview}

By following some guidelines and adopting some design patterns, you can provide the best experience for your users and help ensure that your application can handle what you want it to classify.

## Number of classifiers
{: #classifier-limits}

Each instance of the {{site.data.keyword.nlclassifiershort}} service can have up to 8 classifiers, each with a unique classifier ID. To support more than 8 classifiers, create another instance of {{site.data.keyword.nlclassifiershort}}. You can create a service instance from the {{site.data.keyword.watson}} console [Browse Services](https://{DomainName}/developer/watson){: external} page.

## Classify Multiple Phrases
{: #best-practices-multiple}

You use the **Classify a phrase** method to classify a single text string. With the **Classify multiple phrases** method, you can send up to 30 text phrases in a single request. For details, see the [API reference](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){: external}.

## Languages
{: #language-support}

Although the default language is English, you can specify the language of the training data when you create the classifier. The language of the training data must match the language of the text that you intend to classify. For details, see the [API reference](https://{DomainName}/apidocs/natural-language-classifier#create-classifier){: external}.

The classifier supports English (en), Arabic (ar), French (fr), German (de), Italian (it), Japanese (ja), Korean (ko), Portuguese (Brazilian) (pt), and Spanish (es).

Classifying Japanese texts with the **Classify multiple phrases** method is a beta feature.
{: note}

## Guidelines for good training
{: #training-guidelines}
{: help}
{: support}

The following guidelines are not enforced by the API. However, the classifier tends to perform better when the training data adheres to them:

- Limit the length of input text to fewer than 60 words.
- Limit the number of classes to several hundred classes. Support for larger numbers of classes might be included in later versions of the service.
- Make sure that each class is matched with at least 5 - 10 records when each text record has only one class. This number provides enough training on that class.
- Evaluate the need for multiple classes. Two common reasons drive multiple classes:
    - When the text is vague, identifying a single class is not always clear.
    - When experts interpret the text in different ways, multiple classes support those interpretations.

    However, if many texts in your training data include multiple classes, or if some texts have more than three classes, you might need to refine the classes. For example, review whether the classes are hierarchical. If they are hierarchical, include the leaf node as the class.
- Include standard hyphenated terms when they are part of the training data (`back-to-back` or `part-time job`).

    However, don't connect adjacent words to create new terms not found in the language of the training data. For example, instead of defining `dish-ran-away` or `with_the_spoon`, define the relevant phrases as separate words (`dish ran away` and `with the spoon`) with the appropriate class.

## Constructing training data
{: #best-practices-training-data}

Machine learning describes a process of learning some properties from a set of data and then applying the properties to new data. The {{site.data.keyword.nlclassifiershort}} service follows this process. It is trained to connect predefined classes to example texts and then applies those classes to new inputs.

So, the trained classifier is only as good as the training data. Each text value in the data must represent the kinds of texts that you expect the classifier to predict. Every class that you expect to return must also be in the training data, and the classes that you associate with each text must be correct.

For example, when the texts in your training data are questions, use questions that are representative and typical of the questions that your users ask. You might collect these texts from actual user data, or you might have people who are experts in your field create the texts.

This representative and accurate nature of the data is important because it drives all the processes of and results from the classifier. In addition, the more records that you include in the training data, the more opportunity the classifier has to find a match.
