---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

<!-- Link definitions -->

[cloud-dashboard-watson]: https://console.{DomainName}/dashboard/apps?category=watson
[watson-studio-reg]: https://dataplatform.ibm.com/registration/stepone?context=wdp

# Managing classifiers with the tool
{: #managing-toolkit}

---

**This classic {{site.data.keyword.nlclassifiershort}} classic toolkit is deprecated and replaced by {{site.data.keyword.DSX}}.**

- You can use {{site.data.keyword.DSX}} with all your existing instances and classifiers.
- Get started: You can get to {{site.data.keyword.DSX}} from the service page for your instance. Go to the [Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")][cloud-dashboard-watson]{: new_window}, click on an instance, and then click **Launch tool**.
- You can continue to use this classic toolkit with your existing Cloud Foundry service instances until the toolkit is shut down on July 31, 2018.
- For other details, see the [Release notes](/docs/services/natural-language-classifier/release-notes.html#06july2018)

---

You can train, manage, and test your classifiers by using the {{site.data.keyword.nlclassifierfull}} tool. The tool gives you a unified view of all the classifiers that are running in the same {{site.data.keyword.cloud_notm}} service instance.
{: shortdesc}

## About {{site.data.keyword.DSX}}
{: #studio}

{{site.data.keyword.DSX_full}} is the replacement for the earlier classic toolkit. {{site.data.keyword.DSX}} provides a collaborative environment in the cloud where you can work with {{site.data.keyword.nlclassifiershort}}.

You can find a link to {{site.data.keyword.DSX}} on the {{site.data.keyword.cloud_notm}} service dashboard page for your instance of {{site.data.keyword.nlclassifiershort}}.

### Getting access to {{site.data.keyword.DSX}}

1.  Click a {{site.data.keyword.nlclassifiershort}} service instance from the [Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")][cloud-dashboard-watson]{: new_window}.
1.  Click **Launch tool** on the Manage page.

If you don't have a service instance for {{site.data.keyword.nlclassifiershort}}, run through those steps in the [Before you begin](/docs/services/natural-language-classifier/getting-started.html#prerequisites) section of the "Getting started tutorial."
{: tip}

### Updating classifiers trained outside {{site.data.keyword.DSX}}

{{site.data.keyword.DSX}} provides a feature that supports easily updating the training data and creating another classifier. This **Edit and Retrain** feature is not available for classifiers created outside of {{site.data.keyword.DSX}} because that data is not available to the tool.

To update an older classifier, [access the classic toolkit](#getting-access) through {{site.data.keyword.DSX}}, and then [download](#download) the training data. Return to {{site.data.keyword.DSX}} to create a classifier with this data. You might want to delete the older classifier from the tutorial to avoid extra charges.

## The classic toolkit
{: #getting-access}

You can find the link to the classic toolkit from {{site.data.keyword.DSX}}. This toolkit will be shut down on July 31, 2018.

1.  Go to [{{site.data.keyword.DSX}} ![External link icon](../../icons/launch-glyph.svg "External link icon")][watson-studio-reg]{: new_window}.
1.  Select "Watson Services" from the **Services** top menu. This lists all your {{site.data.keyword.nlclassifiershort}} service instances.
1.  Click the {{site.data.keyword.nlclassifiershort}} service instance that you want to use.
1.  At the top of the page, click the link to the classic tool.
1.  Bookmark the URL for easy access to the toolkit for this instance.

### Giving access to the classic toolkit to others

You can allow others to use your toolkit by adding them in {{site.data.keyword.cloud_notm}}.

1.  From the menu bar, click **Manage** &gt; **Security** &gt; **Identity and Access**, and then click **Users**.
1.  Click **Invite users**.
1.  Specify the email address of the user.
1.  Expand the **Cloud Foundry access** section.
1.  Select the organization that holds your classifier service.
1.  Select the **Auditor** organization role.
1.  Select the **Developer** space role. For details about roles, see [Cloud Foundry roles](/docs/iam/cfaccess.html#cfroles).
1.  In a separate email, send the URL of your toolkit (that you bookmarked earlier) to the users.

## Downloading training data
{: #download}

You can use the classic toolkit to download the training data used to train your classifiers. You can then use that training data to create another classifier in {{site.data.keyword.DSX}}.

1.  On the **Classifiers** page of the toolkit, find the classifier.
1.  Click the **Download data used to train this classifier** icon ![Download training data icon](images/download-training-data.png) to save the data as a backup.
1.  Rename the .csv file with a name that identifies the classifier.
