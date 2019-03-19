---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-06"

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

<!-- Link definitions -->

[cloud-dashboard-watson]: https://{DomainName}/dashboard/apps?category=watson
[watson-studio-reg]: https://dataplatform.cloud.ibm.com/registration/stepone?context=wdp
[watson-studio-product-page]: https://www.ibm.com/cloud/watson-studio

# リリース・ノート
{: #release-notes}

以下の新機能とサービスに対する変更が使用可能です。
{: shortdesc}

## ベータ版フィーチャー
{: #beta}

{{site.data.keyword.IBM_notm}} は、お客様に評価してもらうために、ベータ版として分類したサービス、機能、言語サポートをリリースしています。これらの機能は、不安定であったり、頻繁に変更されたり、突然中止されたりする可能性があります。また、ベータ版の機能は、一般提供版の機能と同レベルのパフォーマンスや互換性を提供するものではなく、実稼働環境で使用するためのものでもありません。ベータ版の機能は、[IBM Developer Answers ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/answers/topics/natural-language-classifier.html){: new_window} でのみサポートされます。

## 変更内容
{: #changelog}

使用可能な新機能とサービスに対する変更は、次のとおりです。

### 2019 年 1 月 25 日
{: #25jan2019}

**フランクフルトのロケーションで大量のデータによるトレーニングが可能に**

フランクフルトでホストされている {{site.data.keyword.nlclassifiershort}} サービス・インスタンスが、大量のデータ・セットでトレーニングできるようになりました。最大 20,000 件のレコードをトレーニング・データに含めることができます。

大きなデータ・サイズがすべての {{site.data.keyword.nlclassifiershort}} ロケーションでサポートされるようになりました。トレーニング・データの詳細については、[データの準備](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data)を参照してください。

### 2018 年 11 月 13 日
{: #18November2018}

**クラスの最大数**

トレーニング・データで最大 3,000 個のクラスをサポートできるようになりました。ただし、クラスの数が少ないほうがパフォーマンスは高くなります。詳細については、[データの準備](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#training-limits)と[分類子のベスト・プラクティス](/docs/services/natural-language-classifier?topic=natural-language-classifier-best-practices-overview#training-guidelines)を参照してください。

### 2018 年 11 月 9 日
{: #9November2018}

**新しい東京ロケーション**

東京ロケーションでホストされる {{site.data.keyword.nlclassifiershort}} サービス・インスタンスを作成できるようになりました。

### 2018 年 10 月 30 日
{: #30october2018}

2018 年 10 月 30 日に、米国南部とドイツのロケーションがトークン・ベースの ID およびアクセス管理 (IAM) 認証を使用するように移行しました。各ロケーションで {{site.data.keyword.nlclassifiershort}} の移行が行われた日付を次に示します。

- 米国南部 (ダラス): 2018 年 10 月 30 日
- ドイツ (フランクフルト): 2018 年 10 月 30 日
- 米国東部: 2018 年 10 月 12 日

IAM 認証への移行による影響は、新規のサービス・インスタンスと既存のサービス・インスタンスとで異なります。

- 該当ロケーションで上記の日付より後に作成した*新規の*サービス・インスタンスは、IAM を使用して API への認証を行います。許可ヘッダーでベアラー・トークンを渡すか、API 鍵を使用します。トークンを使用する場合は、毎回呼び出しにサービス資格情報を埋め込まなくても、認証済みの要求を実行できます。API 鍵の場合は、基本認証を使用します。

{{site.data.keyword.watson}} SDK を使用する場合は、API 鍵を渡して SDK にトークンのライフサイクルを管理させることができます。
- 上記日付の前に作成した*既存の*サービス・インスタンスについては、引き続きサービス・インスタンスのユーザー名とパスワードを指定して認証を行います。このようなサービスは 2019 年 10 月まで使用できますが、その後は IAM への移行が必要です。

詳細情報:
- サービス・インスタンスで使用する認証プロセスを確認するには、{{site.data.keyword.cloud_notm}} [ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/dashboard/apps?watson){: new_window} で対象のインスタンスをクリックして、サービスの資格情報を表示します。
- SDK の詳細やサンプルについては、API リファレンスの[認証 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/natural-language-classifier?language=java#authentication){: new_window} を参照してください。
- Watson サービスで IAM トークンを使用する方法の詳細については、[IAM トークンによる認証](/docs/services/watson?topic=watson-iam#iam)を参照してください。
- Watson サービスで IAM API 鍵を使用する方法の詳細については、[IAM サービスの API 鍵](/docs/services/watson?topic=watson-api-key-bp#api-key-bp)を参照してください。
- Cloud Foundry インスタンスを移行する方法の詳細については、[リソース・グループへの Cloud Foundry サービス・インスタンスのマイグレーション](/docs/resources?topic=resources-migrate#migrate)を参照してください。

### 2018 年 9 月 19 日
{: #19september2018}

**速度制限の導入**

- API 呼び出しが 1 サービス・インスタンスあたり 1 分間で 1500 個の要求に制限されるようになりました。この制限を超えると、HTTP 状況コード `429 Too Many Requests` が返されます。

### 2018 年 8 月 7 日
{: #07august2018}

**クラシック・ツールキットの置き換え**

クラシック・ツールキットは 2018 年 8 月 7 日に終了し、[{{site.data.keyword.DSX}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")][watson-studio-reg]{: new_window} に置き換えられます。

2018 年 9 月 30 日までは、{{site.data.keyword.DSX}} の外部で作成した分類子のトレーニング・データを[移行](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#migrating)できます。移行すれば、{{site.data.keyword.DSX}} で簡単にトレーニング・データを更新して別の分類子を作成できます。

### 2018 年 8 月 2 日
{: #02august2018}

**トレーニング・データの {{site.data.keyword.DSX}}** への移行

{{site.data.keyword.DSX}} の外部で作成した分類子のトレーニング・データを[移行](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#migrating)できるようになりました。移行すれば、{{site.data.keyword.DSX}} で簡単にトレーニング・データを更新して別の分類子を作成できます。

2018 年 9 月 30 日までにデータを移行してください。

### 2018 年 7 月 6 日
{: #06july2018}

**新しいベータ版ツールの提供開始: {{site.data.keyword.DSX}}**

{{site.data.keyword.DSX}} は、これまでのクラシック {{site.data.keyword.nlclassifiershort}} ツールキットの後継機能が含まれている新しい統合環境です。{{site.data.keyword.DSX}} の使用を開始するには、{{site.data.keyword.nlclassifiershort}} サービス・インスタンスのダッシュボードの**「ツールの起動」**をクリックします。詳細については、[{{site.data.keyword.DSX}}による分類子の管理](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#studio)を参照してください。

{{site.data.keyword.DSX}} では、{{site.data.keyword.nlclassifiershort}} だけでなく、{{site.data.keyword.visualrecognitionshort}} や他の多くの {{site.data.keyword.cloud_notm}} のサービスとリソースもサポートされています。{{site.data.keyword.DSX}} を使用すると、クラウドにコラボレーション環境を作れます。開発者、対象分野の専門家、データ・サイエンティストなどが、 {{site.data.keyword.DSX}} で {{site.data.keyword.nlclassifiershort}} や他の AI モデルを作成してトレーニングできます。{{site.data.keyword.DSX}} を使用して分類子をテストすることも可能です。

{{site.data.keyword.DSX}} では、{{site.data.keyword.nlclassifiershort}} の既存のインスタンスや分類子をすべて使用できます。クラシック・ツールキットは、2018 年 8 月 7 日まで使用可能です。

### 2018 年 6 月 8 日
{: #08june2018}

**新しいツール用にトレーニング・データをダウンロード**

既存の {{site.data.keyword.nlclassifiershort}} クラシック・ツールキットは 2018 年 7 月 31 に終了する予定です。このツールキットの後継機能として計画されているのは、**{{site.data.keyword.DSX}}** という新しい統合環境です。[{{site.data.keyword.DSX}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")][watson-studio-reg]{: new_window} では、{{site.data.keyword.visualrecognitionshort}} や他の {{site.data.keyword.cloud_notm}} のサービスとリソースが既にサポートされています。

既存の分類子はすべて {{site.data.keyword.DSX}} でも使用できるようになる予定です。しかし、確実に既存の分類子を再作成したい場合は、2018 年 7 月 31 より前にクラシック・ツールキットからトレーニング・データをダウンロードしておいてください。

[API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/natural-language-classifier){: new_window} を直接使用している場合は、ツールの移行に伴う変更はありません。

### 2018 年 3 月 16 日
{: #16march2018}

- **複数の句の分類**

    1 つの要求で最大 30 個のテキスト句を送信できる**複数の句を分類する**メソッドが、新しく提供されました。この `POST /v1/classifiers/{classifier_id}/classify_collection` メソッドでは、元のメソッドと同じ言語で複数の句の分類が可能です。ただし、日本語は例外です。日本語の場合は、ベータ版機能として起動します。

    API 呼び出しの詳細については、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window} で**複数の句を分類する**メソッドを参照してください。

- **大きなデータ・セットによるトレーニング**

    トレーニング・データに最大 20,000 件のレコードを含められるようになりました。分類子のトレーニングが IBM Deep Learning as a Service によって拡張されています。このオファリングは、グラフィックス処理ユニット (GPU) の柔軟なクラスターを使用して大きなデータ・セットを処理するニューラル・ネットワーク・トレーニング・インフラストラクチャーです。フランクフルト・ロケーションのユーザーや {{site.data.keyword.Bluemix_dedicated_notm}} のユーザーの場合は、トレーニング・データの最大サイズは 15,000 レコードのままです。

### 2017 年 7 月 10 日
{: #10july2017}

**追加の言語:** このサービスでは、アラビア語、英語、フランス語、ドイツ語、日本語、イタリア語、ポルトガル語、スペイン語に加えて、韓国語がサポートされるようになりました。 トレーニング・データの言語は、分類するテキストの言語と一致する必要があります。

言語に関する詳細は、[独自データの使用](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#languages)を参照してください。 API 呼び出しの詳細については、[API リファレンス ![「外部リンク」アイコン](../../icons/launch-glyph.svg "「外部リンク」アイコン")](https://{DomainName}/apidocs/natural-language-classifier){:new_window} で `Create classifier` メソッドを参照してください。

### 2016 年 4 月 6 日
{: #06april2016}

**追加の言語:** このサービスでは、アラビア語、英語、フランス語、日本語、イタリア語、ポルトガル語、スペイン語に加えて、ドイツ語がサポートされるようになりました。 トレーニング・データの言語は、分類するテキストの言語と一致する必要があります。

### 2016 年 2 月 29 日
{: #29february2016}

**追加の言語:** このサービスでは、アラビア語、英語、フランス語、イタリア語、ポルトガル語、スペイン語に加えて、日本語がサポートされるようになりました。

### 2015 年 12 月 7 日
{: #07december2015}

**追加の言語:** このサービスでは、英語、ポルトガル語、スペイン語に加えて、アラビア語、フランス語、イタリア語がサポートされるようになりました。

### 2015 年 11 月 16 日
{: #16november2015}

**追加の言語:** このサービスでは、英語に加えて、ポルトガル語とスペイン語がサポートされるようになりました。
