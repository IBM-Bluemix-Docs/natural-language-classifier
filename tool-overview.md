---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

<!-- Link definitions -->

[cloud-dashboard-watson]: https://console.{DomainName}/dashboard/apps?category=watson
[watson-studio-reg]: https://dataplatform.ibm.com/registration/stepone?context=wdp

# Managing classifiers with {{site.data.keyword.DSX}}
{: #managing-toolkit}

---

**The {{site.data.keyword.nlclassifiershort}} classic toolkit is deprecated and replaced by {{site.data.keyword.DSX}}.**

- You can use {{site.data.keyword.DSX}} with all your classifiers. You can also [import](#migrating) the training data for classifiers created outside of {{site.data.keyword.DSX}}.
- Get started: You can get to {{site.data.keyword.DSX}} from the service page for your instance. Go to the [Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")][cloud-dashboard-watson]{: new_window}, click on an instance, and then click **Launch tool**.
- You can continue to use this classic toolkit with your existing Cloud Foundry service instances until the toolkit is shut down on August 7, 2018. You can migrate data until September 30, 2018.
- For other details, see the [Release notes](/docs/services/natural-language-classifier/release-notes.html#06july2018)

---

You can train, manage, and test your classifiers by using {{site.data.keyword.DSX}}. {{site.data.keyword.DSX}} supports not only {{site.data.keyword.nlclassifierfull}} but also {{site.data.keyword.visualrecognitionshort}} and many other {{site.data.keyword.cloud_notm}} services and resources.
{: shortdesc}

## About {{site.data.keyword.DSX}}
{: #studio}

{{site.data.keyword.DSX_full}} is the replacement for the earlier classic toolkit. {{site.data.keyword.DSX}} provides a collaborative environment in the cloud where you can work with {{site.data.keyword.nlclassifiershort}}.

You can find a link to {{site.data.keyword.DSX}} on the {{site.data.keyword.cloud_notm}} service dashboard page for your instance of {{site.data.keyword.nlclassifiershort}}.

### Getting access to {{site.data.keyword.DSX}}
{: #access-studio}

1.  Click a {{site.data.keyword.nlclassifiershort}} service instance from the [Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")][cloud-dashboard-watson]{: new_window}.
1.  Click **Launch tool** on the Manage page.

If you don't have a service instance for {{site.data.keyword.nlclassifiershort}}, go to  [{{site.data.keyword.DSX}} ![External link icon](../../icons/launch-glyph.svg "External link icon")][watson-studio-reg]{: new_window} and follow the steps in the docs.
{: tip}

### Updating classifiers trained outside {{site.data.keyword.DSX}}
{: #migrating}

{{site.data.keyword.DSX}} supports easily updating the training data and creating another classifier. This **Edit and Retrain** feature is not available for classifiers created outside of {{site.data.keyword.DSX}} until you import the training data.

#### Migrating the training data
To update an older classifier, you associate the classifier with a project in {{site.data.keyword.DSX}} and import the training data.

1.  Go to [{{site.data.keyword.DSX}} ![External link icon](../../icons/launch-glyph.svg "External link icon")][watson-studio-reg]{: new_window}.
1.  Select "Watson Services" from the **Services** top menu. This lists all your {{site.data.keyword.nlclassifiershort}} service instances.
1.  Click the {{site.data.keyword.nlclassifiershort}} service instance that contains the classifier that you want to migrate.
1.  A banner is displayed if the service contains classifiers to import. Click **Get Started**.
1.  Associate the classifier with a new project. Name the project, select the service instance if you have more than one, and click **Create**.
1.  Import the training data. In the "Import data from classic tool" window, enter a new name for the classifier (called "model" in {{site.data.keyword.DSX}}}) and click **Import**. Your training data is imported to use in {{site.data.keyword.DSX}}.

After the training data is imported, you can train the new classifier (model).

#### Deleting the older classifier
You might want to delete the older classifier to avoid extra charges.

1.  Go to [{{site.data.keyword.DSX}} ![External link icon](../../icons/launch-glyph.svg "External link icon")][watson-studio-reg]{: new_window}.
1.  Select "Watson Services" from the **Services** top menu. This lists all your {{site.data.keyword.nlclassifiershort}} service instances.
1.  Click **Launch tool** for the service that contains the older classifier that you migrated.
1.  Click the Options menu for the classifier and select **Delete**.

## The classic toolkit
{: #getting-access}

You can find the link to the classic toolkit from {{site.data.keyword.DSX}}. Access to this toolkit will be shut down on August 7, 2018

#### Getting to the classic toolkit

1.  Go to [{{site.data.keyword.DSX}} ![External link icon](../../icons/launch-glyph.svg "External link icon")][watson-studio-reg]{: new_window}.
1.  Select "Watson Services" from the **Services** top menu. This lists all your {{site.data.keyword.nlclassifiershort}} service instances.
1.  Click the {{site.data.keyword.nlclassifiershort}} service instance that you want to use.
1.  At the top of the page, click the link to the classic tool.
1.  Bookmark the URL for easy access to the toolkit for this instance.

#### Downloading training data
{: #download}

You can use the classic toolkit to download the training data used to train your classifiers. If you want to use that training data to create another classifier in {{site.data.keyword.DSX}}, consider [migrating](#migrating) the data instead.

1.  On the **Classifiers** page of the toolkit, find the classifier.
1.  Click the **Download data used to train this classifier** icon ![Download training data icon](images/download-training-data.png) to save the data as a backup.
1.  Rename the .csv file with a name that identifies the classifier.