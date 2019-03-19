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

# 분류자 우수 사례
{: #best-practices-overview}

가이드라인을 따르고 몇 가지 디자인 패턴을 채택하여 사용자에게 최상의 경험을 제공하고 애플리케이션이 분류 관련 사항을 처리할 수 있도록 지원할 수 있습니다. 

## 분류자 수
{: #classifier-limits}

{{site.data.keyword.nlclassifiershort}} 서비스의 각 인스턴스에는 최대 8개의 분류자가 있을 수 있으며, 각 분류자는 고유한 분류자 ID를 갖습니다. 분류자를 8개 이상 지원하려면 {{site.data.keyword.nlclassifiershort}}의 다른 인스턴스를 작성하십시오. 서비스 인스턴스는 {{site.data.keyword.watson}} 콘솔의 [서비스 찾아보기![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/developer/watson/services){: new_window} 페이지에서 작성할 수 있습니다. 

## 여러 문구 분류
{: #best-practices-multiple}

하나의 텍스트 문자열을 분류하려면 **문구 분류** 메소드를 사용하십시오. **여러 문구 분류** 메소드를 사용할 경우 최대 30개의 텍스트 문구를 한 개의 요청으로 전송할 수 있습니다. 세부사항은 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}을 참조하십시오.

## 언어
{: #language-support}

기본 언어는 영어지만, 분류자를 작성할 때 훈련 데이터의 언어를 지정할 수 있습니다. 훈련 데이터의 언어는 분류하고자 하는 텍스트의 언어와 일치해야 합니다. 세부사항은 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier#create-classifier){:new_window}을 참조하십시오.

분류자는 영어(en), 아랍어(ar), 프랑스어(fr), 독일어(de), 이탈리아어(it), 일본어(ja), 한국어(ko), 브라질 포르투갈어(pt) 및 스페인어(es)를 지원합니다. 

**여러 문구 분류** 메소드를 사용하여 일본어 텍스트를 분류하는 것은 베타 기능입니다.
{: note}

## 좋은 훈련을 위한 가이드라인
{: #training-guidelines}

API에서 다음 가이드라인을 반드시 따르도록 요구하지는 않습니다. 그러나 훈련 데이터가 이를 준수하면 분류자가 보다 잘 수행되는 경향이 있습니다.

- 입력 텍스트의 길이를 60자 미만으로 제한합니다.
- 클래스의 수를 수 백개의 클래스로 제한합니다. 많은 수의 클래스에 대한 지원은 서비스의 후속 버전에서 포함될 수 있습니다.
- 각 텍스트 레코드에 오직 하나의 클래스만 있을 때 각각의 클래스가 최소한 5 - 10개의 레코드와 일치하는지 확인합니다. 이 정도의 수는 해당 클래스에 대해 충분한 훈련을 제공합니다.
- 다중 클래스에 대한 요구사항을 평가합니다. 두 개의 일반적인 이유로 다중 클래스가 사용됩니다.
    - 텍스트가 애매한 경우, 단일 클래스의 식별이 항상 명료하지는 않습니다.
    - 전문가가 해당 텍스트를 다른 방식으로 해석하는 경우, 다중 클래스는 해당 해석을 지원합니다.

그러나 훈련 데이터의 많은 텍스트에 다중 클래스가 포함되어 있거나 일부 텍스트의 클래스가 세 개를 초과하는 경우에는 클래스를 세분화해야 할 수 있습니다. 예를 들어, 클래스가 계층 구조인지 여부를 검토하십시오. 계층 구조인 경우에는 클래스로서 리프 노드를 포함하십시오.
- 훈련 데이터의 일부인 경우에는 하이픈으로 연결한 표준 용어를 포함하십시오(`back-to-back` 또는 ` part-time job`).

    그러나 인접한 단어를 연결하여 훈련 데이터의 언어에서 찾을 수 없는 새 용어를 만들지는 마십시오. 예를 들어, `dish-ran-away` 또는 `with_the_spoon`을 정의하는 대신에 적합한 클래스의 개별 단어(`dish ran away` 및 `with the spoon`)로서 관련 문구를 정의하십시오.

## 훈련 데이터 구성
{: #best-practices-training-data}

기계 학습은 데이터 세트에서 일부 특성을 학습한 후에 해당 특성을 새 데이터에 적용하는 프로세스를 기술합니다. {{site.data.keyword.nlclassifiershort}} 서비스는 이 프로세스를 따릅니다. 이는 사전 정의된 클래스를 예제 텍스트에 연결한 후에 해당 클래스를 새 입력에 적용하도록 훈련되어 있습니다.

따라서 훈련된 분류자는 단지 훈련 데이터와 유사합니다. 데이터의 각 텍스트 값은 분류자가 예측할 것으로 예상되는 텍스트 유형을 표시해야 합니다. 리턴이 예상되는 모든 클래스는 훈련 데이터에도 있어야 하며, 각 텍스트와 연관되는 클래스는 오류가 없어야 합니다.

예를 들어, 훈련 데이터의 텍스트가 질문인 경우에는 대표적이며 사용자가 묻는 일반적인 질문 유형인 질문을 사용하십시오. 실제 사용자 데이터로부터 이러한 텍스트를 수집하거나, 해당 분야의 전문가인 개인이 텍스트를 작성하도록 할 수 있습니다.

데이터의 이 대표성 및 정확성 특성은 분류자의 모든 프로세스와 결과를 드라이브하므로 매우 중요합니다. 또한 훈련 데이터에 레코드를 더 많이 포함할수록 분류자가 일치 항목을 찾을 가능성이 더 높아집니다.

## 추가 리소스
{: #best-practices-next-steps}

{{site.data.keyword.nlclassifiershort}}에 대한 자세한 [우수 사례 및 디자인 패턴![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/assets-watson/pdf/Watson-NLC-Links-Best-Practices-Design-Patterns.pdf){: new_window}을 참조하십시오. 
