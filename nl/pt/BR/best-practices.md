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

# Melhores práticas para classificadores
{: #best-practices-overview}

Seguindo algumas diretrizes e adotando alguns padrões de design, é possível fornecer a melhor experiência para os seus usuários e ajudar a assegurar que o seu aplicativo possa manipular o que você deseja que ele classifique.

## Número de classificadores
{: #classifier-limits}

Cada instância do serviço do {{site.data.keyword.nlclassifiershort}} pode ter até oito classificadores, cada um com um ID de classificador exclusivo. Para suportar mais de oito classificadores, crie outra instância do {{site.data.keyword.nlclassifiershort}}. É possível criar uma instância de serviço por meio da página [Procurar serviços ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/developer/watson/services){: new_window} do console do {{site.data.keyword.watson}}.

## Classificar Diversas Frases
{: #best-practices-multiple}

Use o método **Classificar uma frase** para classificar uma sequência de texto única. Com o método **Classificar múltiplas frases**, é possível enviar até 30 frases de texto em uma única solicitação. Para obter detalhes, veja a [Referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}.

## Linguagens
{: #language-support}

Embora o idioma padrão seja o inglês, é possível especificar o idioma dos dados de treinamento ao criar o classificador. O idioma dos dados de treinamento deve corresponder ao idioma do texto que você pretende classificar. Para obter detalhes, veja a [Referência de API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/natural-language-classifier#create-classifier){:new_window}.

O classificador suporta inglês (en), árabe (ar), francês (fr), alemão (de), italiano (it), japonês (ja), coreano (ko), português (brasileiro) (pt) e espanhol (es).

Classificar textos em japonês com o método **Classificar múltiplas frases** é um recurso beta.
{: note}

## Diretrizes para um bom treinamento
{: #training-guidelines}

As diretrizes a seguir não são aplicadas pela API. No entanto, o classificador tende a executar melhor quando os dados de treinamento aderem a eles:

- Limitar o comprimento do texto de entrada a menos de 60 palavras.
- Limitar o número de classes a várias centenas de classes. O suporte para números maiores de classes poderá ser incluído em versões posteriores do serviço.
- Certificar-se de que cada classe seja correspondida a pelo menos 5 a 10 registros quando cada registro de texto tiver apenas uma classe. Esse número fornece treinamento suficiente nessa classe.
- Avaliar a necessidade de múltiplas classes. Duas razões comuns direcionam múltiplas classes:
    - Quando o texto é vago, identificar uma única classe nem sempre é claro.
    - Quando os especialistas interpretam o texto de diferentes maneiras, múltiplas classes suportam essas interpretações.

    No entanto, se muitos textos em seus dados de treinamento incluírem múltiplas classes ou se alguns textos tiverem mais de três classes, talvez seja necessário refinar as classes. Por exemplo, revise se as classes são hierárquicas. Se forem hierárquicas, inclua o nó folha como a classe.
- Inclua termos hifenizados padrão quando eles fizerem parte dos dados de treinamento (`back-to-back` ou ` part-time job`).

    No entanto, não conecte palavras adjacentes para criar novos termos não localizados no idioma dos dados de treinamento. Por exemplo, em vez de definir `dish-ran-away` ou `with_the_spoon`, defina as frases relevantes como palavras separadas (`dish ran away` e `with the spoon`) com a classe apropriada.

## Construindo dados de treinamento
{: #best-practices-training-data}

O aprendizado de máquina descreve um processo de aprender algumas propriedades de um conjunto de dados e, em seguida, aplicar as propriedades a novos dados. O serviço {{site.data.keyword.nlclassifiershort}} segue esse processo. Ele é treinado para conectar classes predefinidas a textos de exemplo e, em seguida, aplicar essas classes a novas entradas.

Portanto, o classificador treinado é apenas tão bom quanto os dados de treinamento. Cada valor de texto nos dados deve representar os tipos de textos que você espera que o classificador prediga. Cada classe que você espera que seja retornada também deve estar nos dados de treinamento e as classes que você associa a cada texto devem estar corretas.

Por exemplo, quando os textos em seus dados de treinamento forem perguntas, use perguntas que sejam representativas e típicas das perguntas que seus usuários fazem. É possível coletar esses textos de dados de usuários reais ou é possível ter pessoas especialistas em seu campo para criar os textos.

Essa natureza representativa e precisa dos dados é importante porque direciona todos os processos e resultados do classificador. Além disso, quanto mais registros você incluir nos dados de treinamento, mais oportunidade terá o classificador de localizar uma correspondência.

## Recursos adicionais
{: #best-practices-next-steps}

Veja mais [Melhores práticas e padrões de design ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/watson/assets-watson/pdf/Watson-NLC-Links-Best-Practices-Design-Patterns.pdf){: new_window} para o {{site.data.keyword.nlclassifiershort}}.
