---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-06"

keywords: GDPR,General Data Protection Regulation,deleting customer data,privacy

subcollection: natural-language-classifier

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 信息安全
{: #information-security}

IBM 致力于为客户和合作伙伴提供创新的数据隐私、安全性和监管解决方案。
{: shortdesc}

**声明：**
客户应负责确保自身遵守各种法律和法规，包括《欧盟一般数据保护条例》。客户须自行负责就可能会影响客户业务的任何相关法律法规的认定和解释以及客户为了遵守此类法律法规需要采取的任何行动，从合格的法律顾问那里获得意见。


此处描述的产品、服务和其他功能并不适用于所有客户情形，并且在可用性方面可能有限制。IBM 不会提供法律、会计或审计建议，也不会表述或保证其服务或产品将确保客户遵守任何法律或法规。

## 欧盟一般数据保护条例 (GDPR)
{: #gdpr}

IBM 致力于为客户和合作伙伴提供创新的数据隐私、安全性和监管解决方案，以帮助他们完成 GDPR 合规旅程。

在[此处 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/gdpr) 了解有关 IBM 自己的 GDPR 就绪性旅程以及支持您合规旅程的 GDPR 功能和产品的更多信息。{: new_window}.

## 标注和删除 {{site.data.keyword.nlclassifiershort}} 中的数据
{: #gdpr-in-service}

创建分类器时，{{site.data.keyword.nlclassifiershort}} 不支持训练数据中的个人数据。训练数据中不应输入个人数据。此外，对一个短语或多个短语进行分类时，不会捕获或保留任何数据。

训练数据在整个分类器生命周期内进行存储。要删除与分类器关联的训练数据，请使用 **Delete classifier** 方法除去分类器。
