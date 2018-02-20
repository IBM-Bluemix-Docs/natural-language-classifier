---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Best practices for classifiers
By following some guidelines and adopting some design patterns, you can provide the best experience for your users and help ensure that your application can handle what you want it to classify.

## Number of classifiers
{: #classifier-limits}

Each instance of the {{site.data.keyword.nlclassifiershort}} service can have up to 8 classifiers, each with a unique classifier ID. To support more than 8 classifiers, create another instance of {{site.data.keyword.nlclassifiershort}}. You can create a service instance from the {{site.data.keyword.watson}} console [Browse Services ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/developer/watson/services){: new_window} page.

## Languages
{: #language-support}

Although the default language is English, you can specify the language of the training data when you create the classifier. The language of the training data must match the language of the text that you intend to classify. For details, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/natural-language-classifier/api/v1/){:new_window}.

The classifier supports English (en), Arabic (ar), French (fr), German (de), Italian (it), Japanese (ja), Korean (ko), Portuguese (Brazilian) (pt), and Spanish (es).

## Guidelines for good training
{: #training-guidelines}

The following guidelines are not enforced by the API. However, the classifier tends to perform better when the training data adheres to them:

- Limit the length of input text to fewer than 60 words.
- Limit the number of classes to several hundred classes. Support for larger numbers of classes might be included in later versions of the service.
- Make sure that each class is matched with at least 5 - 10 records when each text record has only one class. This number provides enough training on that class.
- Evaluate the need for multiple classes. Two common reasons drive multiple classes:
    - When the text is vague, identifying a single class is not always clear.
    - When experts interpret the text in different ways, multiple classes support those interpretations.

    However, if many texts in your training data include multiple classes, or if some texts have more than three classes, you might need to refine the classes. For example, review whether the classes are hierarchical. If they are hierarchical, include the leaf node as the class.
- Include standard hyphenated terms when they are part of the training data (`back-to-back` or ` part-time job`).

    However, don't connect adjacent words to create new terms not found in the language of the training data. For example, instead of defining `dish-ran-away` or `with_the_spoon`, define the relevant phrases as separate words (`dish ran away` and `with the spoon`) with the appropriate class.

## Constructing training data
Machine learning describes a process of learning some properties from a set of data and then applying the properties to new data. The {{site.data.keyword.nlclassifiershort}} service follows this process. It is trained to connect predefined classes to example texts and then applies those classes to new inputs.

So, the trained classifier is only as good as the training data. Each text value in the data must represent the kinds of texts that you expect the classifier to predict. Every class that you expect to return must also be in the training data, and the classes that you associate with each text must be correct.

For example, when the texts in your training data are questions, use questions that are representative and typical of the questions that your users ask. You might collect these texts from actual user data, or you might have people who are experts in your field create the texts.

This representative and accurate nature of the data is important because it drives all the processes of and results from the classifier. In addition, the more records that you include in the training data, the more opportunity the classifier has to find a match.

## Additional resources
{: #next-steps}

See more [Best practices and design patterns ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/assets-watson/pdf/Watson-NLC-Links-Best-Practices-Design-Patterns.pdf){: new_window} for {{site.data.keyword.nlclassifiershort}}.