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

# Prácticas recomendadas para los clasificadores
{: #best-practices-overview}

Si sigue algunas directrices y adopta algunos patrones de diseño, puede proporcionar la a los usuarios una mejor experiencia y puede garantizar que la aplicación pueda manejar lo que desea que clasifique.

## Número de clasificadores
{: #classifier-limits}

Cada instancia del servicio {{site.data.keyword.nlclassifiershort}} puede tener hasta 8 clasificadores, cada uno de ellos con un ID de clasificador exclusivo. Para dar soporte a más de 8 clasificadores, cree otra instancia de {{site.data.keyword.nlclassifiershort}}. Puede crear una instancia de servicio desde la consola de {{site.data.keyword.watson}}, página [Examinar servicios ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/developer/watson/services){: new_window}.

## Clasificar varias frases
{: #best-practices-multiple}

Utilice el método **Clasificar una frase** para clasificar una única serie de texto. Con el método **Clasificar varias frases**, puede enviar un máximo de 30 frases de texto en una sola solicitud. Para obtener detalles, consulte la [Consulta de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}.

## Idiomas
{: #language-support}

Aunque el idioma predeterminado es el inglés, puede especificar el idioma de los datos de entrenamiento cuando cree el clasificador. El idioma de los datos de formación debe coincidir con el idioma del texto que tiene intención de clasificar. Para obtener detalles, consulte la [Consulta de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/natural-language-classifier#create-classifier){:new_window}.

El clasificador admite los siguientes idiomas: inglés (en), árabe (ar), francés (fr), alemán (de), italiano (it), japonés (ja), coreano (ko), portugués (de Brasil) (pt) y español (es).

La clasificación de textos en japonés con el método **Clasificar varias frases** es una característica beta.
{: note}

## Directrices para un buen entrenamiento
{: #training-guidelines}

La API no impone las siguientes directrices. Sin embargo, el clasificador tiende a ofrecer un mejor rendimiento cuando los datos de entrenamiento las cumplen:

- Limite la longitud del texto de entrada a menos de 60 palabras.
- Limite el número de clases a unos cuantos cientos de clases. Es posible que se incorpore soporte para un mayor número de clases en posteriores versiones del servicio.
- Asegúrese de que cada clase coincida con al menos 5 - 10 registros cuando cada registro de texto tiene una sola clase. Este número ofrece suficiente entrenamiento en dicha clase.
- Evalúe la necesidad de disponer de varias clases. Hay dos motivos comunes por los que disponer de varias clases:
    - Cuando el texto implica cierta ambigüedad, el hecho de identificar una sola clase no siempre ofrece resultados claros.
    - Cuando los expertos interpretan el texto de distintas maneras, varias clases dan soporte a dichas interpretaciones.

    Sin embargo, si muchos textos de los datos de entrenamiento incluyen varias clases, o si algunos textos tienen más de tres clases, es posible que tenga que definir mejor las clases. Por ejemplo, revise si las clases son jerárquicas. Si lo son, incluya el nodo hoja como la clase.
- Incluya términos estándares con guiones cuando forman parte de los datos de entrenamiento (por ejemplo, `calidad-precio` o `inglés-español`).

    Sin embargo, no conecte palabras adyacentes para crear nuevos términos que no estén en el idioma de los datos de entrenamiento. Por ejemplo, en lugar de definir `plato-escurrido` o `con_la_cuchara`, defina las frases como palabras separadas (`plato escurrido` y `con la cuchara`) con la clase adecuada.

## Construcción de datos de entrenamiento
{: #best-practices-training-data}

El aprendizaje de máquina describe el proceso de aprender algunas propiedades a partir de un conjunto de datos y luego aplicar las propiedades a datos nuevos. El servicio {{site.data.keyword.nlclassifiershort}} sigue este proceso. Está entrenado para conectar clases predefinidas a textos de ejemplo y luego aplicar dichas clases a entradas nuevas.

Por lo tanto, el clasificador entrenado es tan bueno como los datos de entrenamiento. Cada valor de texto de los datos debe representar los tipos de textos sobre los que desea que el clasificador realice su predicción. Cada clase que espera devolver debe estar en los datos de entrenamiento, y las clases que asocie a cada texto deben ser las correctas.

Por ejemplo, si los textos de los datos de entrenamiento son preguntas, utilice preguntas que representen y sean las preguntas típicas que realizan sus usuarios. Puede recopilar estos textos de datos reales de los usuarios o puede utilizar textos creados por personas que sean expertas en el campo.

Esta naturaleza representativa y precisa de los datos es importante, ya que controla todos los procesos y resultados del clasificador. Además, cuantos más registros incluya en los datos de entrenamiento, más posibilidades tiene el clasificador de encontrar una coincidencia.

## Recursos adicionales
{: #best-practices-next-steps}

Consulte más [Prácticas recomendadas y patrones de diseño ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/assets-watson/pdf/Watson-NLC-Links-Best-Practices-Design-Patterns.pdf){: new_window} para {{site.data.keyword.nlclassifiershort}}.
