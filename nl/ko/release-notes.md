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

# 릴리스 정보
{: #release-notes}

다음의 새 기능과 서비스에 대한 변경사항을 사용할 수 있습니다.
{: shortdesc}

## 베타 기능
{: #beta}

{{site.data.keyword.IBM_notm}}은 베타로 분류된 평가에 대해 서비스, 기능 및 언어 지원을 릴리스합니다. 이러한 기능은 불안정하고 자주 변경될 수 있으며 충분한 예고 없이 중단될 수 있습니다. 또한 베타 기능은 일반적으로 사용 가능한(GA) 기능에서 제공하는 것과 동일한 레벨의 성능이나 호환성을 제공하지 않을 수 있으며, 프로덕션 환경에서 사용하도록 제공되지는 않습니다. 베타 기능은 [IBM Developer Answers![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/answers/topics/natural-language-classifier.html){: new_window}에서만 지원됩니다. 

## 변경사항
{: #changelog}

다음의 새 기능과 서비스에 대한 변경사항을 사용할 수 있습니다.

### 2019년 1월 25일
{: #25jan2019}

**프랑크푸르트 위치에서 대형 데이터를 사용한 훈련을 지원함**

프랑크푸르트에서 호스팅되는 {{site.data.keyword.nlclassifiershort}} 서비스 인스턴스를 이제 대형 데이터 세트에서
훈련시킬 수 있습니다. 훈련 데이터에 최대 20,000개의 레코드가 포함될 수 있습니다. 

대형 데이터 크기가 이제 모든 {{site.data.keyword.nlclassifiershort}} 위치에서 지원됩니다. 훈련 데이터에 대한 자세한 내용은 [데이터 준비](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data)를 참조하십시오. 

### 2018년 11월 13일
{: #18November2018}

**최대 클래스 수**

훈련 데이터가 이제 최대 3,000개의 클래스를 지원할 수 있습니다. 그러나 클래스가 적을수록 성능이 향상됩니다. 자세한 내용은 [데이터 준비](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#training-limits) 및 [분류자에 대한 우수 사례](/docs/services/natural-language-classifier?topic=natural-language-classifier-best-practices-overview#training-guidelines)를 참조하십시오. 

### 2018년 11월 9일
{: #9November2018}

**새로운 도쿄 위치**

이제 도쿄에서 호스팅되는 {{site.data.keyword.nlclassifiershort}} 서비스 인스턴스를 작성할 수 있습니다. 

### 2018년 10월 30일
{: #30october2018}

2018년 10월 30일부로, 미국 남부 및 독일 위치가 토큰 기반 IAM(Identity and Access Management) 인증을 사용하도록 전환되었습니다. {{site.data.keyword.nlclassifiershort}}는 다음 날짜에 각 위치를 마이그레이션했습니다. 

- 미국 남부(댈러스): 2018년 10월 30일
- 독일(프랑크푸르트): 2018년 10월 30일
- 미국 동부: 2018년 10월 12일

IAM 인증으로의 마이그레이션은 새 서비스 인스턴스와 기존 서비스 인스턴스에 다르게 영향을 미칩니다. 

- 위에 나열된 위치와 날짜에 작성한 *새* 서비스 인스턴스를 사용할 경우 IAM을 사용하여 API를 인증하십시오. 운반자 토큰을 권한 헤더 또는 API 키에 전달할 수 있습니다. 토큰은 호출 시마다 서비스 인증 정보를 임베드하지 않고도 인증된 요청을 지원합니다. API 키는 기본 인증을 사용합니다. 

    {{site.data.keyword.watson}} SDK를 사용할 경우 API 키를 전달하여 SDK에서 토큰의 라이프사이클을 관리하도록 할 수 있습니다.
- 표시된 날짜 이전에 작성한 *기존* 서비스 인스턴스를 사용할 경우 서비스 인스턴스에 대해 사용자 이름과 비밀번호를 제공하여 계속 인증하십시오. IAM으로 마이그레이션해야 할 경우 2019년 10월까지 이 서비스를 사용할 수 있습니다. 

자세한 정보: 
- 서비스 인스턴스에서 사용할 인증 프로세스에 대해 알아보려면 {{site.data.keyword.cloud_notm}} [대시보드![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/dashboard/apps?watson){: new_window}에서 인스턴스를 클릭하여 서비스 인증 정보를 확인하십시오. 
- SDK 예에 대한 자세한 정보는 API 참조서에서 [인증![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier?language=java#authentication){: new_window}을 참조하십시오. 
- Watson 서비스에서 IAM 토큰 사용에 대한 자세한 정보는 [IAM 토큰을 사용한 인증](/docs/services/watson?topic=watson-iam#iam)을 참조하십시오. 
- Watson 서비스에서 IAM API 키 사용에 대한 자세한 정보는 [IAM 서비스 API 키](/docs/services/watson?topic=watson-api-key-bp#api-key-bp)를 참조하십시오. 
- Cloud Foundry 인스턴스 마이그레이션에 대한 자세한 정보는 [Cloud Foundry 서비스 인스턴스를 리소스 그룹으로 마이그레이션](/docs/resources?topic=resources-migrate#migrate)을 참조하십시오. 

### 2018년 9월 19일
{: #19september2018}

**비율 제한이 도입됨**

- API 호출이 이제 서비스 인스턴스당 15,000개 요청(분당)으로 제한됩니다. 이 한계를 초과할 경우 HTTP 상태 코드 `429 Too Many Requests`가 리턴됩니다. 

### 2018년 8월 7일
{: #07august2018}

**클래식 툴킷이 대체됨**

클래식 툴킷이 2018년 8월 7일부로 종료되고 [{{site.data.keyword.DSX}}![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")][watson-studio-reg]{: new_window}로 대체되었습니다. 

{{site.data.keyword.DSX}} 외부에서 작성된 분류자에 대한 훈련 데이터는 2018년 9월 30일까지 [마이그레이션](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#migrating)할 수 있습니다. 마이그레이션한 후에는 훈련 데이터를 손쉽게 업데이트하고 {{site.data.keyword.DSX}} 내에 다른 분류자를 작성할 수 있습니다. 

### 2018년 8월 2일
{: #02august2018}

**{{site.data.keyword.DSX}}로 훈련 데이터 마이그레이션**

이제 {{site.data.keyword.DSX}} 외부에서 작성된 분류자에 대한 훈련 데이터를 [마이그레이션](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#migrating)할 수 있습니다. 마이그레이션한 후에는 훈련 데이터를 손쉽게 업데이트하고 {{site.data.keyword.DSX}} 내에 다른 분류자를 작성할 수 있습니다. 

데이터는 2018년 9월 30일까지 마이그레이션할 수 있습니다. 

### 2018년 7월 6일
{: #06july2018}

**새로운 베타 도구 사용 가능: {{site.data.keyword.DSX}}**

{{site.data.keyword.DSX}}는 이전의 클래식 {{site.data.keyword.nlclassifiershort}} 툴킷의 대체 툴깃을 제공하는 새로운 통합 환경입니다. {{site.data.keyword.DSX}}를 시작하려면 {{site.data.keyword.nlclassifiershort}} 서비스 인스턴스 대시보드에서 **도구 실행**을 클릭하십시오. 자세한 내용은 [{{site.data.keyword.DSX}}로 분류자 관리](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#studio)를 참조하십시오. 

{{site.data.keyword.DSX}}는 {{site.data.keyword.nlclassifiershort}}뿐 아니라 {{site.data.keyword.visualrecognitionshort}} 및 다른 여러 {{site.data.keyword.cloud_notm}} 서비스와 리소스도 지원합니다. {{site.data.keyword.DSX}}는 클라우드에서 협업 환경을 제공합니다. {{site.data.keyword.DSX}}를 사용할 경우 개발자, 관련 주제 전문가, 데이터 과학자 등은 {{site.data.keyword.nlclassifiershort}} 및 다른 AI 모델을 빌드하고 훈련시킬 수 있습니다. {{site.data.keyword.DSX}}를 사용하여 분류자를 테스트할 수도 있습니다. 

기존의 모든 {{site.data.keyword.nlclassifiershort}} 인스턴스 및 분류자와 함께 {{site.data.keyword.DSX}}를 사용할 수 있습니다. 2018년 8월 7일까지는 클래식 툴킷이 사용 가능합니다. 

### 2018년 6월 8일
{: #08june2018}

**새 도구에 대한 훈련 데이터 다운로드**

기존의 {{site.data.keyword.nlclassifiershort}} 클래식 툴킷은 2018년 7월 31일에 종료될 예정입니다. 해당 툴킷은 새로운 통합 환경인 **{{site.data.keyword.DSX}}**로 대체되도록 계획되어 있습니다. [{{site.data.keyword.DSX}}![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")][watson-studio-reg]{: new_window}는 이미 {{site.data.keyword.visualrecognitionshort}} 및 다른 {{site.data.keyword.cloud_notm}} 서비스와 리소스를 지원합니다. 

기존의 모든 분류자가 {{site.data.keyword.DSX}}에서 사용 가능할 것으로 예상됩니다. 그러나 기존 분류자를 다시 작성할 수 있는지 확인하려는 경우에는 2018년 7월 31일 이전에 클래식 툴킷에서 훈련 데이터를 다운로드하십시오. 

[API![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier){: new_window}를 직접 사용하는 사용자의 경우 도구 마이그레이션과 관련하여 변경할 사항이 없습니다. 

### 2018년 3월 16일
{: #16march2018}

- **여러 문구 분류**

    최대 30개의 텍스트 문구를 한 개의 요청으로 전송하는 기능을 지원하는 새로운 **여러 문구 분류** 메소드가 사용 가능합니다. `POST /v1/classifiers/{classifier_id}/classify_collection` 메소드는 문구를 원래 메소드의 언어와 동일한 언어로 분류하는 기능을 지원합니다. 단, 베타 기능으로 실행되는 일본어는 예외입니다. 

    API 호출에 대한 세부사항은 [API 참조서![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}에서 **여러 문구 분류** 메소드를 참조하십시오. 

- **대형 데이터 세트를 사용한 훈련**

    이제 훈련 데이터에 최대 20,000개의 레코드가 포함될 수 있습니다. IBM Deep Learning as a Service를 통해 분류자 훈련이 개선되었습니다. 이 오퍼링은 그래픽 처리 장치(GPU)의 탄력적 클러스터를 사용하여 대형 데이터 세트를 처리하는 신경망 훈련 인프라입니다. 훈련 데이터의 최대 크기는 프랑크푸르트 위치의 사용자 또는 {{site.data.keyword.Bluemix_dedicated_notm}}를 사용하는 사용자에 대해 최대 15,000개의 레코드로 유지되고 있습니다. 

### 2017년 7월 10일
{: #10july2017}

**추가 언어:** 이제 서비스는 아랍어, 영어, 프랑스어, 독일어, 일본어, 이탈리아어, 포르투갈어, 스페인어와 함께 한국어도 지원합니다. 훈련 데이터의 언어는 분류하고자 하는 텍스트의 언어와 일치해야 합니다.

언어에 대한 세부사항은 [자체 데이터 사용](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#languages)을 참조하십시오. API 호출에 대한 세부사항은 [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}의 `Create classifier` 메소드를 참조하십시오.

### 2016년 4월 6일
{: #06april2016}

**추가 언어:** 이제 서비스는 아랍어, 영어, 프랑스어, 일본어, 이탈리아어, 포르투갈어, 스페인어와 함께 독일어도 지원합니다. 훈련 데이터의 언어는 분류하고자 하는 텍스트의 언어와 일치해야 합니다.

### 2016년 2월 29일
{: #29february2016}

**추가 언어:** 이제 서비스는 아랍어, 영어, 프랑스어, 이탈리아어, 포르투갈어, 스페인어와 함께 일본어도 지원합니다.

### 2015년 12월 7일
{: #07december2015}

**추가 언어:** 이제 서비스는 영어, 포르투갈어, 스페인어와 함께 아랍어, 프랑스어, 이탈리아어도 지원합니다.

### 2015년 11월 16일
{: #16november2015}

**추가 언어:** 이제 서비스는 영어와 함께 포르투갈어, 스페인어도 지원합니다.
