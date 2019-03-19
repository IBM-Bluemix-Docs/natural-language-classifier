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

# Segurança de informações
{: #information-security}

A IBM está comprometida em fornecer aos nossos clientes e parceiros soluções inovadoras de privacidade de dados, segurança e governança.
{: shortdesc}

**Aviso:**
os clientes são responsáveis por assegurar sua própria conformidade com várias leis e regulamentações, incluindo o Regulamento Geral sobre a Proteção de Dados da União Europeia. Os clientes são os únicos responsáveis por obter aconselhamento de consultoria jurídica competente quanto à identificação e interpretação de quaisquer leis e regulamentos relevantes que possam afetar os negócios dos clientes e quaisquer ações que os clientes possam precisar tomar para cumprir tais leis e regulamentações.

Os produtos, serviços e outros recursos descritos aqui não são adequados para todas as situações do cliente e podem ter disponibilidade restrita. A IBM não fornece aviso jurídico, contábil ou de auditoria nem representa ou garante que os seus serviços ou produtos assegurarão que os clientes estejam em conformidade com qualquer lei ou regulamentação.

## Regulamento Geral sobre a Proteção de Dados (GDPR) da União Europeia
{: #gdpr}

A IBM está comprometida em fornecer aos nossos clientes e parceiros soluções inovadoras de privacidade de dados, segurança e controle para auxiliá-los em sua jornada para a conformidade com GDPR.

Saiba mais sobre a própria jornada de prontidão GDPR da IBM e nossas capacidades e ofertas de GDPR para suportar sua jornada de conformidade [aqui ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/gdpr){: new_window}.

## Rotulando e excluindo dados no  {{site.data.keyword.nlclassifiershort}}
{: #gdpr-in-service}

O {{site.data.keyword.nlclassifiershort}} não suporta Dados pessoais nos dados de treinamento quando você cria um classificador. Nenhum Dado pessoal deve ser inserido nos dados de treinamento. Além disso, nenhum dado é capturado ou retido quando você classifica uma frase ou classifica múltiplas frases.

Os dados de treinamento são armazenados durante a vida do classificador. Para excluir dados de treinamento que estiverem associados a um classificador, use o método **Excluir classificador** para remover o classificador.
