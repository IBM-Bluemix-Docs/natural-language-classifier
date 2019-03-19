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

# 정보 보안
{: #information-security}

IBM은 당사의 고객과 파트너에게 혁신적인 데이터 개인정보 보호, 보안 및 통제 솔루션을 제공하기 위해 노력하고 있습니다.
{: shortdesc}

**알림:**
고객은 유럽 연합(EU)의 일반 개인정보 보호법률(General Data Protection Regulation)을 포함한 다양한 법령과 규정을 준수해야 할 책임이 있습니다. 고객은 고객의 비즈니스에 영향을 줄 수 있는 관련 법령 및 규정에 대한 확인과 해석,
그러한 법령 및 규정의 준수를 위해 필요한 고객의 모든 조치와 관련하여 적절한 법률 자문을 받아야 할
단독 책임이 있습니다.

여기에서 설명하는 제품, 서비스 및 기타 기능은 일부 고객의 상황에는 해당되지 않을 수 있으며
그 가용성이 제한될 수 있습니다. IBM은 법률, 회계 또는 감사 관련 자문을 제공하지 않으며, IBM의 서비스나 제품 사용이 고객의 관련 법령이나 규정 준수를 보장한다는 진술이나 보증을 제공하지 않습니다.

## EU의 일반 개인정보 보호법률(GDPR)
{: #gdpr}

IBM은 당사의 고객과 파트너가 GDPR을 준수할 수 있도록 혁신적인 데이터 개인정보 보호, 보안 및 통제 솔루션을 제공하기 위해 노력하고 있습니다. 

IBM의 자체 GDPR 대비 과정 및 고객의 준수 과정을 지원하기 위한 당사의 GDPR 기능과 오퍼링에 대해 알아보려면 [여기![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/gdpr){: new_window}를 클릭하십시오. 

## {{site.data.keyword.nlclassifiershort}}에서 데이터 레이블 지정 및 삭제
{: #gdpr-in-service}

분류자를 작성할 때 {{site.data.keyword.nlclassifiershort}}는 훈련 데이터에서 개인 데이터를 지원하지 않습니다. 개인 데이터는 훈련 데이터에 입력되지 않습니다. 또한 한 개의 문구 또는 여러 문구를 분류할 때 데이터가 캡처되거나 보존되지 않습니다. 

훈련 데이터는 분류자가 사용 가능한 동안에만 저장됩니다. 분류자와 연관된 훈련 데이터를 삭제하려면 **분류자 삭제** 메소드를 사용하여 분류자를 제거하십시오. 
