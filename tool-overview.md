---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-08"

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

**The {{site.data.keyword.nlclassifiershort}} classic toolkit is shut down as of August 7, 2018 and is replaced by  [{{site.data.keyword.DSX}} ![External link icon](../../icons/launch-glyph.svg "External link icon")][watson-studio-reg]{: new_window}.**

- You can use {{site.data.keyword.DSX}} with all your classifiers.
- You can [import](#migrating) the training data for classifiers created outside of {{site.data.keyword.DSX}} until September 30, 2018.
- For other details, see the [Release notes](/docs/services/natural-language-classifier/release-notes.html#06july2018).
- Get started: You can get to {{site.data.keyword.DSX}} from the service page for your instance. Go to the [Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")][cloud-dashboard-watson]{: new_window}, click on an instance, and then click **Launch tool**.

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
