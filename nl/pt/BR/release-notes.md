---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-17"

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

# Nota sobre a Liberação
{: #release-notes}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.
{: shortdesc}

## Recursos Beta
{: #beta}

O {{site.data.keyword.IBM_notm}} libera os serviços, os recursos e o suporte ao idioma para sua avaliação que são classificados como beta. Esses recursos podem ficar instáveis, podem mudar frequentemente e podem ser descontinuados com breve aviso. Os recursos beta podem também não fornecer o mesmo nível de desempenho ou compatibilidade que os recursos geralmente disponíveis fornecem e não são destinados ao uso em um ambiente de produção. Os recursos beta são suportados apenas em [IBM Developer Answers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/answers/topics/natural-language-classifier.html){: new_window}.

## Mudanças
{: #changelog}

Os novos recursos e mudanças a seguir para o serviço estão disponíveis.

### 25 de janeiro de 2019
{: #25jan2019}

**O local de Frankfurt agora suporta treinamento com dados maiores**

As instâncias de serviço do {{site.data.keyword.nlclassifiershort}} hospedadas em Frankfurt podem agora ser treinadas em conjuntos de dados maiores. É possível incluir até 20.000 registros em seus dados de treinamento.

O tamanho de dados maior agora é suportado em todos os locais do {{site.data.keyword.nlclassifiershort}}. Para obter mais detalhes sobre os dados de treinamento, consulte [Preparação de dados](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data).

### 13 de novembro de 2018
{: #18November2018}

**Número máximo de classes**

Os dados de treinamento agora podem suportar um máximo de 3.000 classes, embora usar menos classes possa resultar em melhor desempenho. Para obter detalhes, consulte [Preparação de dados](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#training-limits) e [Melhores práticas para classificadores](/docs/services/natural-language-classifier?topic=natural-language-classifier-best-practices-overview#training-guidelines).

### 9 de novembro de 2018
{: #9November2018}

** Local de Nova Tóquio **

Agora é possível criar instâncias de serviço do {{site.data.keyword.nlclassifiershort}} que são hospedadas no local de Tóquio.

### 30 de outubro de 2018
{: #30october2018}

Em 30 de outubro de 2018, os locais Sul dos EUA e Alemanha fizeram a transição para usar a autenticação do Identity and Access Management (IAM) baseada em token. O {{site.data.keyword.nlclassifiershort}} migrou cada local nas datas a seguir:

- Sul dos EUA (Dallas): 30 de outubro de 2018
- Alemanha (Frankfurt): 30 de outubro de 2018
- Leste dos EUA: 12 de outubro de 2018

A migração para a autenticação do IAM afeta as instâncias de serviço novas e existentes de forma diferente:

- Com as instâncias de serviço *novas* que você cria nos locais e datas listados anteriormente, você autentica para a API usando o IAM. É possível passar um token de acesso em um cabeçalho de Autorização ou em uma chave de API. Os tokens suportam solicitações autenticadas sem as credenciais de serviço incorporadas em cada chamada. As chaves API usam autenticação básica.

    Quando você usa qualquer um dos SDKs do {{site.data.keyword.watson}}, é possível passar a chave de API e deixar que o SDK gerencie o ciclo de vida dos tokens.
- Com as instâncias de serviço *existentes* que você criou antes das datas indicadas, você continua a autenticar fornecendo o nome do usuário e a senha para a instância de serviço. Será possível usar esses serviços até outubro de 2019, data em que você deverá migrar para o IAM.

Mais informações:
- Para saber qual processo de autenticação usar com a instância de serviço, visualize as credenciais de serviço clicando na instância no {{site.data.keyword.cloud_notm}} Painel do [ ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/dashboard/apps?watson){: new_window}.
- Para obter mais informações e exemplos sobre o SDK, consulte [Autenticação ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier?language=java#authentication){: new_window} na referência de API.
- Para obter mais informações sobre como usar tokens do IAM com serviços do Watson, consulte [Autenticando com tokens do IAM](/docs/services/watson?topic=watson-iam#iam).
- Para obter mais informações sobre como usar as chaves de API do IAM com serviços do Watson, consulte [Chaves de API de serviço do IAM](/docs/services/watson?topic=watson-api-key-bp#api-key-bp).
- Para obter mais informações sobre a migração de instâncias do Cloud Foundry, consulte [Migrando instâncias de serviço do Cloud Foundry para um grupo de recursos](/docs/resources?topic=resources-migrate#migrate).

### 19 de setembro de 2018
{: #19september2018}

** Limitação de taxa introduzida **

- As chamadas de API agora são limitadas a 1500 solicitações por minuto por instância de serviço. Se você exceder o limite, o código de status de HTTP `429 Too Many Requests` será retornado.

### 7 de agosto de 2018
{: #07august2018}

** Kit de ferramentas Classic substituído **

O kit de ferramentas clássico está encerrado desde 7 de agosto de 2018 e foi substituído por [{{site.data.keyword.DSX}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")][watson-studio-reg]{: new_window}.

É possível migrar os dados de treinamento para classificadores criados fora do {{site.data.keyword.DSX}} até 30 de setembro de 2018. Após migrar, será possível atualizar facilmente os dados de treinamento e criar outro classificador no {{site.data.keyword.DSX}}.

### 2 de agosto de 2018
{: #02august2018}

** Migrar seus dados de treinamento para o  {{site.data.keyword.DSX}} **

Agora é possível migrar os dados de treinamento para classificadores criados fora do {{site.data.keyword.DSX}}. Após migrar, será possível atualizar facilmente os dados de treinamento e criar outro classificador no {{site.data.keyword.DSX}}.

É possível migrar dados até 30 de setembro de 2018.

### 6 de julho de 2018
{: #06july2018}

** Nova ferramenta beta disponível:  {{site.data.keyword.DSX}} **

O {{site.data.keyword.DSX}} é o novo ambiente integrado que inclui uma substituição para o kit de ferramentas do {{site.data.keyword.nlclassifiershort}} clássico anterior. Para a introdução ao {{site.data.keyword.DSX}}, clique em **Ativar ferramenta** em um painel de instância de serviço do {{site.data.keyword.nlclassifiershort}}. Para obter detalhes, consulte  [ Gerenciando classificadores com o  {{site.data.keyword.DSX}} ](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-toolkit#managing-toolkit).

O {{site.data.keyword.DSX}} suporta não apenas o {{site.data.keyword.nlclassifiershort}}, mas também o {{site.data.keyword.visualrecognitionshort}} e muitos outros serviços e recursos do {{site.data.keyword.cloud_notm}}. O {{site.data.keyword.DSX}} fornece um ambiente colaborativo na nuvem. Com o {{site.data.keyword.DSX}}, os desenvolvedores, os especialistas no assunto, os cientistas de dados e outros podem construir e treinar o {{site.data.keyword.nlclassifiershort}} e outros modelos de IA. Também é possível usar o {{site.data.keyword.DSX}} para testar seus classificadores.

É possível usar o {{site.data.keyword.DSX}} com todas as instâncias e classificadores existentes do {{site.data.keyword.nlclassifiershort}}. O kit de ferramentas clássico permanece disponível até 7 de agosto de 2018.

### 8 de junho de 2018
{: #08june2018}

**Faça download de seus dados de treinamento para a nova ferramenta**

O kit de ferramentas clássico do {{site.data.keyword.nlclassifiershort}} existente está planejado para encerrar em 31 de julho de 2018. A substituição planejada para o kit de ferramentas é **{{site.data.keyword.DSX}}**, o novo ambiente integrado. O [{{site.data.keyword.DSX}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")][watson-studio-reg]{: new_window} já suporta o {{site.data.keyword.visualrecognitionshort}} e outros serviços e recursos do {{site.data.keyword.cloud_notm}}.

Esperamos que todos os seus classificadores existentes estejam disponíveis no {{site.data.keyword.DSX}}. No entanto, se você desejar ter certeza de que possa recriar os seus classificadores existentes, faça download dos dados de treinamento do kit de ferramentas clássico antes de 31 de julho de 2018.

Para aqueles que usam a [API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier){: new_window} diretamente, não há nenhuma mudança com a migração da ferramenta.

### 16 de março de 2018
{: #16march2018}

- ** Classificar múltiplas frases **

    Está disponível um novo método **Classificar múltiplas frases** que suporta o envio de até 30 frases de texto em uma solicitação. O método `POST /v1/classifiers/{classifier_id}/classify_collection` suporta a classificação de frases nas mesmas linguagens que para o método original, exceto para japonês, que é ativado como um recurso beta.

    Para obter detalhes sobre a chamada de API, consulte o método **Classificar múltiplas frases** na [Referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}.

- ** Treinar com conjuntos de dados maiores **

    Agora é possível incluir até 20.000 registros em seus dados de treinamento. O treinamento do classificador é agora aprimorado pelo IBM Deep Learning como um Serviço. Essa oferta é uma infraestrutura de treinamento de rede neural que usa um cluster elástico de unidades de processamento de gráficos (GPU) para manipular conjuntos de dados maiores. O tamanho máximo dos dados de treinamento permanece em 15.000 registros para usuários no local de Frankfurt ou usuários com o {{site.data.keyword.Bluemix_dedicated_notm}}.

### 10 de julho de 2017
{: #10july2017}

**Linguagens adicionais:** o serviço agora suporta coreano, além de árabe, inglês, francês, alemão, japonês, italiano, português e espanhol. O idioma dos dados de treinamento deve corresponder ao idioma do texto que você pretende classificar.

Para obter detalhes sobre os idiomas, veja [Usando seus próprios dados](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#languages). Para obter detalhes sobre a chamada API, veja o método `Criar classificador` na [Referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}.

### 06 de abril de 2016
{: #06april2016}

**Idiomas adicionais:** o serviço agora suporta alemão, além de árabe, inglês, francês, japonês, italiano, português e espanhol. O idioma dos dados de treinamento deve corresponder ao idioma do texto que você pretende classificar.

### 29 de fevereiro de 2016
{: #29february2016}

**Idiomas adicionais:** o serviço agora suporta japonês, além de árabe, inglês, francês, italiano, português e espanhol.

### 7 de dezembro de 2015
{: #07december2015}

**Idiomas adicionais:** o serviço agora suporta árabe, francês e italiano, além de inglês, português e espanhol.

### 16 de novembro de 2015
{: #16november2015}

**Idiomas adicionais:** o serviço agora suporta os idiomas português e espanhol, além de inglês.
