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

# 分類子に関するベスト・プラクティス
{: #best-practices-overview}

いくつかのガイドラインに従い、いくつかの設計パターンを採用すれば、最高のユーザー・エクスペリエンスを実現し、望んだとおりの分類をアプリケーションに実行させることができます。

## 分類子の数
{: #classifier-limits}

{{site.data.keyword.nlclassifiershort}} サービスではインスタンスごとに最大 8 個の分類子を作成できます。それぞれに固有の分類子 ID が付きます。8 個を超える分類子をサポートするためには、もう 1 つ {{site.data.keyword.nlclassifiershort}} インスタンスを作成する必要があります。{{site.data.keyword.watson}} コンソールの[「サービスの参照」![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/developer/watson/services){: new_window} ページからサービス・インスタンスを作成できます。

## 複数の句の分類
{: #best-practices-multiple}

1 つのテキスト・ストリングを分類する場合は、**「句の分類 (Classify a phrase)」**メソッドを使用します。**「複数の句の分類 (Classify multiple phrases)」**メソッドを使用すれば、1 つの要求で最大 30 個のテキスト句を送信できます。詳細については、[API リファレンス ![「外部リンク」アイコン](../../icons/launch-glyph.svg "「外部リンク」アイコン")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window} を参照してください。

## 言語
{: #language-support}

デフォルトの言語は英語ですが、分類子の作成時にはトレーニング・データの言語を指定することができます。 トレーニング・データの言語は、分類するテキストの言語と一致する必要があります。 詳細については、[API リファレンス ![「外部リンク」アイコン](../../icons/launch-glyph.svg "「外部リンク」アイコン")](https://{DomainName}/apidocs/natural-language-classifier#create-classifier){:new_window} を参照してください。

分類子では、英語 (en)、アラビア語 (ar)、フランス語 (fr)、ドイツ語 (de)、イタリア語 (it)、日本語 (ja)、韓国語 (ko)、ポルトガル語 (ブラジル) (pt)、スペイン語 (es) がサポートされています。

**「複数の句の分類 (Classify multiple phrases)」**メソッドによる日本語テキストの分類はベータ機能です。
{: note}

## 適切なトレーニングのガイドライン
{: #training-guidelines}

以下のガイドラインは、API によって強制されるものではありません。 ただし、トレーニング・データがこれらに準拠していると、分類子のパフォーマンスが向上する傾向があります。

- 入力テキストの長さは、60 語未満に制限してください。
- クラスの数は、数百個に制限してください。 サービスの将来のバージョンでは、より多くの数のクラスのサポートが導入される可能性があります。
- 各テキスト・レコードにクラスが 1 つしかない場合、少なくとも 5 個から 10 個のレコードで各クラスをマッチングさせるようにしてください。 この数により、そのクラスで十分なトレーニングが行われるようになります。
- 複数のクラスのニーズを評価します。 一般的に、複数のクラスが推奨される理由は以下の 2 つです。
    - テキストがあいまいである場合は、1 つのクラスを特定することは常に明確であるとは限りません。
    - 複数の専門家がテキストをそれぞれ異なる方法で解釈する場合は、複数のクラスがそれらの解釈をサポートします。

    ただし、トレーニング・データ内の多くのテキストに複数のクラスが含まれている場合、またはいくつかのテキストに 3 つより多くのクラスがある場合は、クラスの絞り込みが必要になることがあります。 例えば、クラスが階層であるかどうかを確認してください。 階層である場合は、リーフ・ノードをクラスとして含めてください。
- トレーニング・データの一部である (`back-to-back` や `part-time job`) 場合は、行末ハイフン付けした標準の用語を含めます。

    ただし、トレーニング・データの言語にない新しい用語を作成する場合に、隣接する用語をつなげないでください。 例えば、`dish-ran-away` や `with_the_spoon` を定義するのではなく、適切なクラスを使用して、関連する句を別個の用語 (`dish ran away` や `with the spoon`) として定義します。

## トレーニング・データの構成
{: #best-practices-training-data}

機械学習とは、データのセットからいくつかの特性を学習した後で、それらの特性を新規データに適用するプロセスのことです。 {{site.data.keyword.nlclassifiershort}} サービスは以下のプロセスに従います。 このサービスは、事前定義クラスをサンプル・テキストに関連付けるようにトレーニングされた後で、それらのクラスを新規の入力に適用します。

そのため、トレーニングされた分類子の精度は、トレーニング・データの品質によって決定します。 データ内の各テキスト値は、その分類子で予測すると予期されるテキストの種類を表している必要があります。 返されると予期される各クラスも、トレーニング・データ内に存在する必要があります。また、各テキストに関連付けるクラスが正しい必要があります。

例えば、トレーニング・データのテキストが質問の場合、ユーザーが尋ねる典型的な質問を使用します。 これらのテキストは実際のユーザー・データから収集することも、この分野の専門家にテキストを作成してもらうこともできます。

分類子のすべてのプロセスおよび結果はこのデータから導出されるため、典型的かつ正確なデータを使用することが重要です。 また、トレーニング・データ内に含めるレコードが多くなるほど、分類子が一致を検出する可能性も高くなります。

## 追加リソース
{: #best-practices-next-steps}

詳細については、{{site.data.keyword.nlclassifiershort}} の[ベスト・プラクティスと設計パターン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/assets-watson/pdf/Watson-NLC-Links-Best-Practices-Design-Patterns.pdf){: new_window} を参照してください。
