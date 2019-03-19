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

# 資訊安全
{: #information-security}

IBM 致力於為我們的客戶及合作夥伴提供創新的資料隱私權、安全及控管解決方案。
{: shortdesc}

**注意事項：**客戶負責確定本身遵循各種法令規章，包括「歐盟一般資料保護規範」。有關任何可能影響「客戶」業務之相關法令規章之確認與解釋，以及任何「客戶」為遵循該等法令規章所需採取之行動，「客戶」應自行負責向該法律顧問取得諮詢意見。

本文所述的產品、服務及其他功能並不適合所有客戶情況，並且可用性可能受到限制。IBM 不提供法律、會計或審核意見，亦不聲明或保證其服務或產品可確保「客戶」遵循任何法令規章。

## 歐盟一般資料保護規範 (GDPR)
{: #gdpr}

IBM 致力於為我們的客戶及合作夥伴提供創新的資料隱私權、安全及控管解決方案，以協助他們邁向 GDPR 法規遵循。

在[這裡 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/gdpr){: new_window} 進一步瞭解 IBM 自己的 GDPR 整備行程及 GDPR 功能及供應項目來支援法規遵循行程。

## 在 {{site.data.keyword.nlclassifiershort}} 中標示及刪除資料
{: #gdpr-in-service}

當您建立分類器時，{{site.data.keyword.nlclassifiershort}} 不支援訓練資料中有「個人資料」。「個人資料」不會進入訓練資料中。此外，當您分類一個詞組或分類多個詞組時，不會擷取或保留任何資料。

在分類器期限內，會儲存訓練資料。若要刪除與分類器相關聯的訓練資料，請使用**刪除分類器**方法來移除分類器。
