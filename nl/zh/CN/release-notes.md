---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-16"

keywords: new features,updates to Natural Language Classifier,what's new

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

# 发行说明
{: #release-notes}

为服务提供了以下新功能和更改。
{: shortdesc}

## Beta 功能
{: #beta}

{{site.data.keyword.IBM_notm}} 发布分类为 Beta 的服务、功能和语言支持供您评估。这些功能可能不太稳定，可能经常会更改，还可能会临时通知中断使用。此外，Beta 功能可能无法提供与一般可用功能所提供级别相同的性能或兼容性，并且 Beta 功能不适用于生产环境。Beta 功能仅在 [IBM Developer Answers ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/answers/topics/natural-language-classifier.html){: new_window} 上受支持。

## 更改
{: #changelog}

为服务提供了以下新功能和更改。

### 2019 年 1 月 25 日
{: #25jan2019}

**法兰克福位置现在支持使用更大的数据进行训练**

法兰克福托管的 {{site.data.keyword.nlclassifiershort}} 服务实例现在可以在更大的数据集上进行训练。您的训练数据中可以包含最多 20,000 条记录。

所有 {{site.data.keyword.nlclassifiershort}} 位置现在都支持更大的数据大小。有关训练数据的更多详细信息，请参阅[数据准备](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data)。

### 2018 年 11 月 13 日
{: #18November2018}

**最大类数量**

训练数据现在可支持最多 3,000 个类，不过类越少，性能可能越佳。有关详细信息，请参阅[数据准备](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#training-limits)和[分类器的最佳实践](/docs/services/natural-language-classifier?topic=natural-language-classifier-best-practices-overview#training-guidelines)。

### 2018 年 11 月 9 日
{: #9November2018}

**新的东京位置**

您现在可以创建托管于东京位置的 {{site.data.keyword.nlclassifiershort}} 服务实例。

### 2018 年 10 月 30 日
{: #30october2018}

在 2018 年 10 月 30 日，美国南部和德国位置转换为使用基于令牌的身份和访问权管理 (IAM) 认证。{{site.data.keyword.nlclassifiershort}} 于以下日期对每个位置进行了迁移：

- 美国南部（达拉斯）：2018 年 10 月 30 日
- 德国（法兰克福）：2018 年 10 月 30 日
- 美国东部：2018 年 10 月 12 日

迁移到 IAM 认证对新的和现有服务实例的影响有所不同：

- 使用您在先前列出的位置和日期创建的*新*服务实例，您使用 IAM 向 API 认证。您可以传递授权头中的不记名令牌或 API 密钥。令牌支持认证请求，且无需在每个调用中嵌入服务凭证。API 密钥使用基本认证。

    使用任何 {{site.data.keyword.watson}} SDK 时，您可以传递 API 密钥，并让 SDK 管理令牌的生命周期。
- 使用所指示日期之前创建的*现有*服务实例，您将继续通过提供服务实例的用户名和密码进行认证。在 2019 年 10 月之前，您可以继续使用这些服务，但之后必须迁移到 IAM。

更多信息：
- 要了解将何种认证流程用于您的服务实例，请单击 {{site.data.keyword.cloud_notm}} [仪表板 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/dashboard/apps?watson){: new_window} 上的实例来查看服务凭证。
- 有关 SDK 的更多信息和示例，请参阅 API 参考中的[认证 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/natural-language-classifier?language=java#authentication){: new_window}。
- 有关搭配使用 IAM 令牌与 Watson 服务的更多信息，请参阅[使用 IAM 令牌进行认证](/docs/services/watson?topic=watson-iam#iam)。
- 有关搭配使用 IAM API 密钥与 Watson 服务的更多信息，请参阅 [IAM 服务 API 密钥](/docs/services/watson?topic=watson-api-key-bp#api-key-bp)。
- 有关迁移 Cloud Foundry 实例的更多信息，请参阅[将 Cloud Foundry 服务实例迁移到资源组](/docs/resources?topic=resources-migrate#migrate)。

### 2018 年 9 月 19 日
{: #19september2018}

**引入了速率限制**

- API 调用现在限制为每个服务实例每分钟 1500 个请求。如果超过该限制，将返回 HTTP 状态码 `429 Too Many Requests`。

### 2018 年 8 月 7 日
{: #07august2018}

**替换了经典工具箱**

经典工具箱于 2018 年 8 月 7 日关闭，并由 [{{site.data.keyword.DSX}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")][watson-studio-reg]{: new_window} 替换。

在 2018 年 9 月 30 日之前，您可以迁移在 {{site.data.keyword.DSX}} 外部创建的分类器的训练数据。迁移后，您可以轻松更新训练数据并在 {{site.data.keyword.DSX}} 内创建其他分类器。

### 2018 年 8 月 2 日
{: #02august2018}

**将训练数据迁移到 {{site.data.keyword.DSX}}**

您现在可以迁移在 {{site.data.keyword.DSX}} 外部创建的分类器的训练数据。迁移后，您可以轻松更新训练数据并在 {{site.data.keyword.DSX}} 内创建其他分类器。

您只能在 2018 年 9 月 30 日之前迁移数据。

### 2018 年 7 月 6 日
{: #06july2018}

**提供了新的 Beta 工具：{{site.data.keyword.DSX}}**

{{site.data.keyword.DSX}} 是一个新集成环境，其中包含先前经典 {{site.data.keyword.nlclassifiershort}} 工具箱的替换项。要开始使用 {{site.data.keyword.DSX}}，请从 {{site.data.keyword.nlclassifiershort}} 服务实例仪表板单击**启动工具**。有关详细信息，请参阅[使用 {{site.data.keyword.DSX}} 管理分类器](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#studio)。

{{site.data.keyword.DSX}} 不仅支持 {{site.data.keyword.nlclassifiershort}}，还支持 {{site.data.keyword.visualrecognitionshort}} 和许多其他 {{site.data.keyword.cloud_notm}} 服务及资源。{{site.data.keyword.DSX}} 在云中提供协作环境。使用 {{site.data.keyword.DSX}}，开发者、主题专家、数据研究员和其他人可构建并训练 {{site.data.keyword.nlclassifiershort}} 及其他 AI 模型。您还可以使用 {{site.data.keyword.DSX}} 测试您的分类器。

您可以将 {{site.data.keyword.DSX}} 用于您的所有现有 {{site.data.keyword.nlclassifiershort}} 实例和分类器。经典工具箱保持可用到 2018 年 8 月 7 日为止。

### 2018 年 6 月 8 日
{: #08june2018}

**下载新工具的训练数据**

现有 {{site.data.keyword.nlclassifiershort}} 经典工具箱安排为 2018 年 7 月 31 日关闭。工具箱的计划替换项为 **{{site.data.keyword.DSX}}**，即新的集成环境。[{{site.data.keyword.DSX}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")][watson-studio-reg]{: new_window} 已支持 {{site.data.keyword.visualrecognitionshort}} 和其他 {{site.data.keyword.cloud_notm}} 服务及资源。

预期您的所有现有分类器将在 {{site.data.keyword.DSX}} 中可用。但是，如果想要确保可重新创建现有分类器，请于 2018 年 7 月 31 日之前从经典工具箱下载训练数据。

对于直接使用 [API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/natural-language-classifier){: new_window} 的用户，工具迁移无更改。

### 2018 年 3 月 16 日
{: #16march2018}

- **对多个短语进行分类**

    提供了新的 **Classify multiple phrases** 方法，可支持在一个请求中发送最多 30 个文本短语。`POST /v1/classifiers/{classifier_id}/classify_collection` 方法支持对原始方法所用相同语言的短语进行分类，但日语除外，因为日语启动为 Beta 功能。

    有关 API 调用的详细信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window} 中的 **Classify multiple phrases** 方法。

- **使用更大的数据集训练**

    现在，您的训练数据中可以包含最多 20,000 条记录。IBM Deep Learning as a Service 现在对分类器训练进行了增强。此产品是一种神经网络训练基础架构，使用灵活的图形处理单元 (GPU) 集群来处理更大的数据集。对于法兰克福位置的用户或使用 {{site.data.keyword.Bluemix_dedicated_notm}} 的用户，最大训练数据大小仍为 15,000 条记录。

### 2017 年 7 月 10 日
{: #10july2017}

**新增语言：**现在，服务除了支持阿拉伯语、英语、法语、德语、日语、意大利语、葡萄牙语和西班牙语外，还支持韩语。训练数据的语言必须与您打算分类的文本的语言相匹配。

有关语言的详细信息，请参阅[使用自己的数据](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#languages)。有关 API 调用的详细信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/natural-language-classifier){:new_window} 中的 `Create classifier` 方法。

### 2016 年 4 月 6 日
{: #06april2016}

**新增语言：**现在，服务除了支持阿拉伯语、英语、法语、日语、意大利语、葡萄牙语和西班牙语外，还支持德语。训练数据的语言必须与您打算分类的文本的语言相匹配。

### 2016 年 2 月 29 日
{: #29february2016}

**新增语言：**现在，服务除了支持阿拉伯语、英语、法语、意大利语、葡萄牙语和西班牙语外，还支持日语。

### 2015 年 12 月 7 日
{: #07december2015}

**新增语言：**现在，服务除了支持英语、葡萄牙语和西班牙语外，还支持阿拉伯语、法语和意大利语。

### 2015 年 11 月 16 日
{: #16november2015}

**新增语言：**现在，服务除了支持英语外，还支持葡萄牙语和西班牙语。
