---

copyright:
  years: 2019
lastupdated: "2019-03-22"

keywords: HA,DR,high availability,disaster recovery, restoring classifiers

subcollection: natural-language-classifier

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:table: .aria-labeledby="caption"}

# High availability and disaster recovery
{: #ha-dr-top}

The {{site.data.keyword.nlclassifierfull}} service is highly available within multiple IBM Cloud locations (for example, Dallas and Washington, DC). However, recovering from potential disasters that affect an entire location requires planning and preparation.
{: shortdesc}

You are responsible for understanding your configuration, customization, and usage of the service. You are also responsible for being ready to re-create an instance of the service in a new location and to restore your data in any location. See [How do I ensure zero downtime? ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window} for more information.

## High availability
{: #ha-dr-availability}

{{site.data.keyword.nlclassifiershort}} supports high availability with no single point of failure. The service achieves high availability automatically and transparently by using the multi-zone region (MZR) feature provided by {{site.data.keyword.cloud_notm}}.

{{site.data.keyword.cloud_notm}} enables multiple zones that do not share a single point of failure within a single location. It also provides automatic load balancing across the zones within a region.

## Disaster recovery
{: #ha-dr-recovery}

Disaster recovery can become an issue if an {{site.data.keyword.cloud_notm}} location experiences a significant failure that includes the potential loss of data. Because MZR is not available across locations, you must wait for {{site.data.keyword.IBM_notm}} to bring a location back online if it becomes unavailable. If underlying data services are compromised by the failure, you must also wait for {{site.data.keyword.IBM_notm}} to restore those data services.

If a catastrophic failure occurs, {{site.data.keyword.IBM_notm}} might not be able to recover data from database backups. In this case, you need to restore your data to return your service instance to its most recent state. You can restore the data to the same or to a different location.

Your disaster recovery plan includes knowing, preserving, and being prepared to restore all data that is maintained on {{site.data.keyword.cloud_notm}}. This stored data includes the training data for your classifiers.

Re-creating classifiers from saved data takes time. You can maintain parallel service configurations in multiple locations to help eliminate the turnaround time associated with disaster recovery.
{: note}

### Disaster recovery for classifiers
{: #ha-dr-classifiers}

For classifiers, you need to store the training data and metadata.

#### Backing up training data
{: #ha-dr-backup}

You can download the training data from {{site.data.keyword.DSX_full}}:

1.  Click a {{site.data.keyword.nlclassifiershort}} service instance from the [Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/dashboard){: new_window}.
1.  Click **Launch tool** on the Manage page.
1.  For each classifier, click ![Open and close options icon](images/options.png "Open and close image icons") and select **Download training data**.

The metadata identifies the language of the data, and the classifier name. Save the training data and metadata in a safe location.

#### Restoring classifiers
{: #ha-dr-restore}

To recover from a disaster, you can use the backup information to re-create your classifier. For more information, see [Create and train a classifier](/docs/services/natural-language-classifier?topic=natural-language-classifier-natural-language-classifier#natural-language-classifier) in the Getting started tutorial.

### Client applications
{: #ha-dr-update-apps}

When you re-create a classifier, the value of the classifier ID changes. Update the ID in any apps that use the classifier.
