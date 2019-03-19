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

# 分類器最佳作法
{: #best-practices-overview}

藉由遵循部分準則以及採用部分設計型樣，您可以提供您使用者的最佳經驗，並協助確定應用程式可以處理您想要它分類的項目。

## 分類器數目
{: #classifier-limits}

{{site.data.keyword.nlclassifiershort}} 服務的每個實例都可以有最多 8 個分類器，而且每個都有唯一的分類器 ID。若要支援超過 8 個分類器，請建立另一個 {{site.data.keyword.nlclassifiershort}} 實例。您可以從 {{site.data.keyword.watson}} 主控台[瀏覽服務 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/developer/watson/services){: new_window} 頁面建立服務實例。

## 分類多個詞組
{: #best-practices-multiple}

您可以使用**分類一個詞組**方法來分類單一字串。使用**分類多個詞組**方法，即可在單一要求中傳送最多 30 個文字詞組。如需詳細資料，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}。

## 語言
{: #language-support}

雖然預設語言是英文，但是您可以在建立分類器時指定訓練資料語言。訓練資料語言必須符合您要分類之文字的語言。如需詳細資料，請參閱 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/natural-language-classifier#create-classifier){:new_window}。

分類器支援英文 (en)、阿拉伯文 (ar)、法文 (fr)、德文 (de)、義大利文 (it)、日文 (ja)、韓文 (ko)、葡萄牙文（巴西）(pt) 及西班牙文 (es)。

使用**分類多個詞組**方法來分類日文文字是測試版特性。
{: note}

## 良好訓練的準則
{: #training-guidelines}

下列準則不是透過 API 強制執行。不過，訓練資料遵循它們時，分類器的執行效能會較佳：

- 將輸入文字長度限制成少於 60 個單字。
- 將類別數目限制為數百個類別。服務的更新版本可能會支援較大數量的類別。
- 每一個文字記錄只有一個類別時，請確定每一個類別都符合至少 5 - 10 筆記錄。這個數目可提供該類別的足夠訓練。
- 評估多個類別的需求。兩個常見的原因會驅動多個類別：
    - 文字模糊不清時，不一定可以清楚地識別單一類別。
    - 專家以不同的方式來解譯文字時，有多個類別支援這些解釋。

不過，如果訓練資料中的許多文字都包括多個類別，或者部分文字有三個以上的類別，您可能需要修正類別。例如，檢閱類別是否為階層式。如果它們是階層式，請將葉節點包括為類別。
- 如果標準加連號的術語是訓練資料的一部分，請包括標準加連號的術語（`back-to-back` 或 `part-time job`）。

    不過，請不要連接相鄰單字，來建立訓練資料語言中找不到的新術語。例如，將相關詞組定義為具有適當類別的個別單字（`dish ran away` 及 `with the spoon`），而不要定義 `dish-ran-away` 或 `with_the_spoon`。

## 建構訓練資料
{: #best-practices-training-data}

機器學習可說明學習來自一組資料的部分內容後將內容套用至新資料的程序。{{site.data.keyword.nlclassifiershort}} 服務遵循此程序。它經過訓練，以將預先定義的類別連接至範例文字，然後將那些類別套用至新輸入。

因此，受過訓練的分類器就只是訓練資料。資料中的每一個文字值都必須代表您預期分類器預測的文字類型。您預期傳回的每個類別也必須位在訓練資料中，而與每一個文字相關聯的類別都必須正確。

例如，訓練資料中的文字發生問題時，請使用具代表性且一般是使用者所問問題的問題。您可以從實際使用者資料收集這些文字，也可以讓您領域中的專家建立文字。

資料的這個代表性且精確的本質十分重要，因為它會驅動分類器的所有程序以及分類器的結果。此外，您包括在訓練資料中的記錄筆數越多，分類器必須符合相符項目的機會就越大。

## 其他資源
{: #best-practices-next-steps}

請進一步參閱 {{site.data.keyword.nlclassifiershort}} 的[最佳作法及設計型樣 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/assets-watson/pdf/Watson-NLC-Links-Best-Practices-Design-Patterns.pdf){: new_window}。
