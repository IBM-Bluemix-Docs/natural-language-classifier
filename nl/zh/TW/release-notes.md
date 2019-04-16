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

# 版本注意事項
{: #release-notes}

下列是服務可用的新增特性及變更。
{: shortdesc}

## 測試版特性
{: #beta}

{{site.data.keyword.IBM_notm}} 發行您評估的服務、特性及語言支援，而且這些項目都分類為測試版。這些特性可能不穩定、經常變更，且可能接到簡短通知就中斷服務。測試版特性也可能未提供正式發行特性所提供但不要用於正式作業環境的相同層次的效能或相容性。只有 [IBM Developer Answers ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/answers/topics/natural-language-classifier.html){: new_window} 才支援測試版特性。

## 變更
{: #changelog}

下列是服務可用的新增特性及變更。

### 2019 年 1 月 25 日
{: #25jan2019}

**法蘭克福位置現在支援使用較大資料的訓練**

位於法蘭克福的 {{site.data.keyword.nlclassifiershort}} 服務實例現在可以使用較大的資料集進行訓練。您可以在訓練資料中包括最多 20,000 筆記錄。

所有 {{site.data.keyword.nlclassifiershort}} 位置現在都支援較大的資料大小。如需訓練資料的詳細資料，請參閱[資料準備](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data)。

### 2018 年 11 月 13 日
{: #18November2018}

**類別數目上限**

訓練資料現在可以支援最多 3,000 個類別，但類別越少，效能越好。如需詳細資料，請參閱[資料準備](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#training-limits)及[分類器最佳作法](/docs/services/natural-language-classifier?topic=natural-language-classifier-best-practices-overview#training-guidelines)。

### 2018 年 11 月 9 日
{: #9November2018}

**新的東京位置**

您現在可以建立位於 Tokyo 位置的 {{site.data.keyword.nlclassifiershort}} 服務實例。

### 2018 年 10 月 30 日
{: #30october2018}

在 2018 年 10 月 30 日，美國南部及德國位置已轉移成使用記號型 Identity and Access Management (IAM) 鑑別。{{site.data.keyword.nlclassifiershort}} 已在下列日期移轉每個位置：

- 美國南部（達拉斯）：2018 年 10 月 30 日
- 德國（法蘭克福）：2018 年 10 月 30 日
- 美國東部：2018 年 10 月 12 日

移轉至 IAM 鑑別會以不同的方式影響新的及現有的服務實例：

- 使用您在先前所列位置及日期中建立的*新* 服務實例，即可使用 IAM 來鑑別 API。您可以在 Authorization 標頭中傳遞 Bearer 記號，或傳遞 API 金鑰。記號支援已鑑別要求，而不需要在每個呼叫中內嵌服務認證。API 金鑰使用基本鑑別。

    當您使用任何 {{site.data.keyword.watson}} SDK 時，可以傳遞 API 金鑰，並讓 SDK 管理記號的生命週期。
- 使用您在所指出日期之前建立的*現有* 服務實例，即可提供服務實例的使用者名稱及密碼來繼續鑑別。當您必須移轉至 IAM 時，在 2019 年 10 月之前仍然可以使用這些服務。

相關資訊：
- 若要瞭解與服務實例搭配使用的鑑別處理程序，請按一下 {{site.data.keyword.cloud_notm}} [儀表板 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/dashboard/apps?watson){: new_window} 上的實例來檢視服務認證。
- 如需 SDK 的相關資訊及範例，請參閱 API 參考資料中的[鑑別 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier?language=java#authentication){: new_window}。
- 如需搭配使用 IAM 記號與 Watson 服務的相關資訊，請參閱[使用 IAM 記號鑑別](/docs/services/watson?topic=watson-iam#iam)。
- 如需搭配使用 IAM API 金鑰與 Watson 服務的相關資訊，請參閱 [IAM 服務 API 金鑰](/docs/services/watson?topic=watson-api-key-bp#api-key-bp)。
- 如需移轉 Cloud Foundry 實例的相關資訊，請參閱[將 Cloud Foundry 服務實例移轉至資源群組](/docs/resources?topic=resources-migrate#migrate)。

### 2018 年 9 月 19 日
{: #19september2018}

**已建立速率限制**

- API 呼叫現在限制為每個服務實例每分鐘有 1500 個要求。如果您超出限制，則會傳回 HTTP 狀態碼 `429 Too Many Requests`。

### 2018 年 8 月 7 日
{: #07august2018}

**已取代典型工具箱**

典型工具箱已從 2018 年 8 月 7 日淘汰，並取代為 [{{site.data.keyword.DSX}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")][watson-studio-reg]{: new_window}。

您可以移轉 2018 年 9 月 30 日之前在 {{site.data.keyword.DSX}} 外部建立的分類器的訓練資料。在您移轉之後，可以輕鬆地更新訓練資料，並在 {{site.data.keyword.DSX}} 內建立另一個分類器。

### 2018 年 8 月 2 日
{: #02august2018}

**將訓練資料移轉至 {{site.data.keyword.DSX}}**

您現在可以移轉在 {{site.data.keyword.DSX}} 外部建立的分類器的訓練資料。在您移轉之後，可以輕鬆地更新訓練資料，並在 {{site.data.keyword.DSX}} 內建立另一個分類器。

您可以移轉 2018 年 9 月 30 日之前的資料。

### 2018 年 7 月 6 日
{: #06july2018}

**提供新的測試版工具：{{site.data.keyword.DSX}}**

{{site.data.keyword.DSX}} 是新的整合環境，內含較早典型 {{site.data.keyword.nlclassifiershort}} 工具箱的取代項目。若要開始使用 {{site.data.keyword.DSX}}，請從 {{site.data.keyword.nlclassifiershort}} 服務實例儀表板中按一下**啟動工具**。如需詳細資料，請參閱[使用 {{site.data.keyword.DSX}} 管理分類器](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#studio)。

{{site.data.keyword.DSX}} 不僅支援 {{site.data.keyword.nlclassifiershort}}，還支援 {{site.data.keyword.visualrecognitionshort}} 以及許多其他 {{site.data.keyword.cloud_notm}} 服務和資源。{{site.data.keyword.DSX}} 提供雲端中的協同環境。使用 {{site.data.keyword.DSX}}，開發人員、主題專家、資料科學家及其他人員即可建置與訓練 {{site.data.keyword.nlclassifiershort}} 和其他 AI 模型。您也可以使用 {{site.data.keyword.DSX}} 來測試分類器。

您可以搭配使用 {{site.data.keyword.DSX}} 與所有現有 {{site.data.keyword.nlclassifiershort}} 實例及分類器。典型工具箱在 2018 年 8 月 7 日 之前仍然可供使用。

### 2018 年 6 月 8 日
{: #08june2018}

**下載新工具的訓練資料**

排定在 2018 年 7 月 31 日淘汰現有的 {{site.data.keyword.nlclassifiershort}} 典型工具箱。規劃取代此工具箱的項目為新的整合環境：**{{site.data.keyword.DSX}}**。[{{site.data.keyword.DSX}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")][watson-studio-reg]{: new_window} 已支援 {{site.data.keyword.visualrecognitionshort}} 及其他 {{site.data.keyword.cloud_notm}} 服務和資源。

我們預期將在 {{site.data.keyword.DSX}} 中提供您的所有現有分類器。不過，如果您要確定可以重建現有分類器，則請從 2018 年 7 月 31 日之前的典型工具箱下載訓練資料。

對於直接使用 [API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier){: new_window} 的人員而言，工具移轉並沒有任何變更。

### 2018 年 3 月 16 日
{: #16march2018}

- **分類多個詞組**

    提供新的**分類多個詞組**方法，以支援在一個要求中傳送最多 30 個文字詞組。`POST /v1/classifiers/{classifier_id}/classify_collection` 方法支援分類與原始方法相同語言（但日文除外）的詞組，而原始方法會啟動為測試版特性。

    如需 API 呼叫的詳細資料，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window} 中的**分類多個詞組**方法。

- **使用較大的資料集訓練**

    您現在可以在訓練資料中包括最多 20,000 筆記錄。分類器訓練現在透過「IBM 深度學習即服務」予以加強。本供應項目是一種類神經網路訓練基礎架構，可使用圖形處理裝置 (GPU) 的彈性叢集來處理較大的資料集。對於法蘭克福位置的使用者或 {{site.data.keyword.Bluemix_dedicated_notm}} 使用者，訓練資料的大小上限仍然維持 15,000 筆記錄。

### 2017 年 7 月 10 日
{: #10july2017}

**其他語言：**除了阿拉伯文、英文、法文、德文、日文、義大利文、葡萄牙文及西班牙文之外，服務現在還支援韓文。訓練資料語言必須符合您要分類之文字的語言。

如需語言的詳細資料，請參閱[使用自己的資料](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#languages)。如需 API 呼叫的詳細資料，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier){:new_window} 中的`建立分類器`方法。

### 2016 年 4 月 6 日
{: #06april2016}

**其他語言：**除了阿拉伯文、英文、法文、日文、義大利文、葡萄牙文及西班牙文之外，服務現在還支援德文。訓練資料語言必須符合您要分類之文字的語言。

### 2016 年 2 月 29 日
{: #29february2016}

**其他語言：**除了阿拉伯文、英文、法文、義大利文、葡萄牙文及西班牙文之外，服務現在還支援日文。

### 2015 年 12 月 7 日
{: #07december2015}

**其他語言：**除了英文、葡萄牙文及西班牙文之外，服務現在還支援阿拉伯文、法文及義大利文。

### 2015 年 11 月 16 日
{: #16november2015}

**其他語言：**除了英文之外，服務現在還支援葡萄牙文及西班牙文。
