---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-06"

keywords: language support,supported languages,best practices,guidelines

subcollection: natural-language-classifier

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}

# 分类器的最佳实践
{: #best-practices-overview}

通过遵循一些准则并采用一些设计模式，您可以为用户提供最佳体验，并帮助确保您的应用程序可处理您希望它分类的内容。

## 分类器数量
{: #classifier-limits}

{{site.data.keyword.nlclassifiershort}} 服务的每个实例可具有最多 8 个分类器，其中每个都具有唯一分类器标识。要支持超过 8 个分类器，请创建另一个 {{site.data.keyword.nlclassifiershort}} 实例。您可以从 {{site.data.keyword.watson}} 控制台[浏览服务 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/developer/watson/services){: new_window} 页面创建服务实例。

## 对多个短语进行分类
{: #best-practices-multiple}

您可以使用 **Classify a phrase** 方法来对单个文本字符串进行分类。使用 **Classify multiple phrases** 方法，您可以在单个请求中发送最多 30 个文本短语。有关详细信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}。

## 语言
{: #language-support}

虽然缺省语言为英语，但您可以在创建分类器时，指定训练数据的语言。训练数据的语言必须与您打算分类的文本的语言相匹配。有关详细信息，请参阅 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/natural-language-classifier#create-classifier){:new_window}。

分类器支持英语 (en)、阿拉伯语 (ar)、法语 (fr)、德语 (de)、意大利语 (it)、日语 (ja)、韩语 (ko)、巴西葡萄牙语 (pt) 和西班牙语 (es)。

使用 **Classify multiple phrases** 方法对日语文本进行分类是 Beta 功能。
{: note}

## 良好训练准则
{: #training-guidelines}

API 并未强制实施以下准则。但是，如果训练数据遵循这些准则，分类器的性能可能会更好：

- 将输入文本的长度限制为少于 60 个词。
- 将类的数量限制在几百个类以内。该服务的更高版本可能会支持更多数量的类。
- 确保在每个文本记录只有一个类时，每个类至少与 5 - 10 个记录相匹配。此数量的记录可提供对该类的足够训练。
- 评估是否需要多个类。需要多个类的常见原因有两个：
    - 文本含义不明确，不一定能明确识别单个类。
    - 不同专家以不同方式解释文本时，多个类可支持这些解释。

但是，如果训练数据中有许多文本包含多个类，或者某些文本有三个以上的类，那么可能需要优化这些类。例如，复查这些类是否为分层的。如果是分层的，请将叶节点包含为类。
- 包含训练数据中含有的以连字符连接的标准术语（`back-to-back` 或 ` part-time job`）。

    但是，不要连接相邻词语来创建训练数据的语言中找不到的新术语。例如，不要定义 `dish-ran-away` 或 `with_the_spoon`，而是使用相应类将相关短语定义为单独的词语（`dish ran away` 和 `with the spoon`）。

## 构造训练数据
{: #best-practices-training-data}

机器学习描述了从一组数据中学习某些属性，然后将这些属性应用于新数据的过程。{{site.data.keyword.nlclassifiershort}} 服务遵循此过程。它经过训练，可将预定义类连接到示例文本，然后将这些类应用于新输入。

所以，训练后的分类器的性能不超出训练数据。数据中的每个文本值必须表示您期望分类器预测的文本类型。此外，您期望返回的每个类也必须位于训练数据中，并且与每个文本关联的类必须正确。

例如，如果训练数据中的文本是提问，请使用在用户提问中具有代表性和典型性的提问。您可从实际用户数据中收集这些文本，也可让您的领域的专家来创建这些文本。

数据的这一代表性和准确性十分重要，因为它将推动分类器中的所有流程以及结果。此外，在训练数据中包含的记录越多，分类器能找到匹配项的机会也越多。

## 其他资源
{: #best-practices-next-steps}

请参阅 {{site.data.keyword.nlclassifiershort}} 的更多[最佳实践和设计模式 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/assets-watson/pdf/Watson-NLC-Links-Best-Practices-Design-Patterns.pdf){: new_window}。
