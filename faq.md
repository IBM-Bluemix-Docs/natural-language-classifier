---

copyright:
  years: 2021
lastupdated: "2021-02-01"

keywords: natural language classifier frequently asked questions

subcollection: natural-language-classifier

content-type: faq

---


{:shortdesc: .shortdesc}
{:faq: data-hd-content-type='faq'}
{:support: data-reuse='support'}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}


# FAQs for {{site.data.keyword.nlclassifiershort}}
{: #nlclassifier-faqs}

FAQs for {{site.data.keyword.nlclassifierfull}} might include questions about training, error conditions, or other topics. To find all FAQs for {{site.data.keyword.cloud}}, see our [FAQ library](/docs/faqs).
{: shortdesc}

## Can I retrain a classifier?
{: #faq-retrain}
{: faq}

To train a classifier again, delete the original model and create another with a new model ID. You cannot “retrain” in a way that keeps the same model ID.  If you manage your classifiers with {{site.data.keyword.DSX}}, you can “retrain” a model by using the {{site.data.keyword.nlclassifiershort}} model builder, which has the effect of deleting the original model and creating a new model with a new model ID. See [Retraining a Natural Language Classifier model](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/nlc-retrain.html).

## How do I delete training data?
{: #faq-delete}
{: faq}

Training data is stored with the classifier.  To delete training data, delete the classifier that has the data by using the [Delete classifier method](/apidocs/natural-language-classifier#deleteclassifier).


## How do I recover from an Entitlement error when adding a classifier?
{: #faq-limit}
{: faq}

If you see “Error: Entitlement error”, then your {{site.data.keyword.nlclassifiershort}} service has reached the limit of 8 classifiers for that instance. To support more than 8 classifiers, create another instance of {{site.data.keyword.nlclassifiershort}}. Refer to [Number of classifiers](/docs/natural-language-classifier?topic=natural-language-classifier-best-practices-overview#classifier-limits).
