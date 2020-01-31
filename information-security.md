---

copyright:
  years: 2015, 2020
lastupdated: "2020-01-30"

keywords: GDPR,General Data Protection Regulation,deleting customer data,privacy

subcollection: natural-language-classifier

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Information security
{: #information-security}

IBM is committed to providing our clients and partners with innovative data privacy, security and governance solutions.
{: shortdesc}

**Notice:**
Clients are responsible for ensuring their own compliance with various laws and regulations, including the European Union General Data Protection Regulation. Clients are solely responsible for obtaining advice of competent legal counsel as to the identification and interpretation of any relevant laws and regulations that may affect the clients’ business and any actions the clients may need to take to comply with such laws and regulations.

The products, services, and other capabilities described herein are not suitable for all client situations and may have restricted availability. IBM does not provide legal, accounting or auditing advice or represent or warrant that its services or products will ensure that clients are in compliance with any law or regulation.

## European Union General Data Protection Regulation (GDPR)
{: #gdpr}

IBM is committed to providing our clients and partners with innovative data privacy, security and governance solutions to assist them on their journey to GDPR compliance.

Learn more about IBM's own GDPR readiness journey and our GDPR capabilities and offerings to support your compliance journey [here](http://www.ibm.com/gdpr){: external}.

## Labeling and deleting data in {{site.data.keyword.nlclassifiershort}}
{: #gdpr-in-service}

{{site.data.keyword.nlclassifiershort}} does not support Personal Data in the training data when you create a classifier. No Personal Data is to be entered into the training data. In addition, no data is captured or retained when you classify a phrase or classify multiple phrases.

Training data is stored for the life of the classifier. To delete training data that is associated with a classifier, use the **Delete classifier** method to remove the classifier.
