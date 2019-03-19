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

# Notas del release
{: #release-notes}

Están disponibles los siguientes cambios y nuevas características del servicio.
{: shortdesc}

## Características beta
{: #beta}

{{site.data.keyword.IBM_notm}} publica servicios, características y soporte de idioma clasificados como beta, para evaluarlos. Estas características pueden ser inestables, pueden cambiar con frecuencia y pueden dejar de recibir soporte tras un aviso con poca antelación. Las características beta también pueden no proporcionar el mismo nivel de rendimiento o compatibilidad que proporcionan las características con disponibilidad general, y no están pensadas para su uso en un entorno de producción. Las características beta solo reciben soporte en [IBM Developer Answers ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/answers/topics/natural-language-classifier.html){: new_window}.

## Cambios
{: #changelog}

Están disponibles los siguientes cambios y nuevas características del servicio.

### 25 de enero de 2019
{: #25jan2019}

**La ubicación de Frankfurt ahora da soporte al entrenamiento con datos de mayor tamaño**

Las instancias del servicio {{site.data.keyword.nlclassifiershort}} en Frankfurt ahora se pueden entrenar en conjuntos de datos de mayor tamaño. Puede incluir un máximo de 20.000 registros en los datos de entrenamiento.

El mayor tamaño de los datos ahora recibe soporte en todas las ubicaciones de {{site.data.keyword.nlclassifiershort}}. Para obtener más información sobre los datos de entrenamiento, consulte [Preparación de los datos](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data).

### 13 de noviembre de 2018
{: #18November2018}

**Número máximo de clases**

Ahora los datos de entrenamiento pueden ahora dar soporte a un máximo de 3.000 clases, aunque es posible que menos clases den como resultado un mejor rendimiento. Para obtener más información, consulte [Preparación de los datos](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#training-limits) y [Prácticas recomendadas para clasificadores](/docs/services/natural-language-classifier?topic=natural-language-classifier-best-practices-overview#training-guidelines).

### 9 de noviembre de 2018
{: #9November2018}

**Nueva ubicación en Tokio**

Ahora puede crear instancias del servicio {{site.data.keyword.nlclassifiershort}} alojadas en la ubicación de Tokio.

### 30 de octubre de 2018
{: #30october2018}

El 30 de octubre de 2018, las ubicaciones EE. UU. sur y Alemania pasaron a utilizar la autenticación de Identity and Access Management (IAM) basada en señales. {{site.data.keyword.nlclassifiershort}} migró cada ubicación en las fechas siguientes:

- EE. UU. sur (Dallas): 30 de octubre de 2018
- Alemania (Frankfurt): 30 de octubre de 2018
- EE. UU. este: 12 de octubre de 2018

La migración a la autenticación IAM afecta de forma distinta a las instancias de servicio nuevas y existentes:

- Con las *nuevas* instancias de servicio que se crean en las ubicaciones y las fechas indicadas anteriormente, se autenticará en la API mediante IAM. Puede pasar una señal de portadora (bearer) en una cabecera de autorización o en una clave de API. Las señales dan soporte a solicitudes autenticadas sin incluir credenciales de servicio en cada llamada. Las claves de API utilizan la autenticación básica.

    Si utiliza cualquiera de los SDK de {{site.data.keyword.watson}}, puede pasar la clave de API y dejar que el SDK gestione el ciclo de vida de las señales.
- Con las instancias de servicio *existentes* que ha creado antes de las fechas indicadas, continúe autenticándose proporcionando el nombre de usuario y la contraseña correspondientes a la instancia de servicio. Puede utilizar estos servicios hasta octubre de 2019, fecha en la que debe migrar a IAM.

Más información:
- Para saber qué proceso de autenticación debe utilizar con su instancia de servicio, visualice las credenciales de servicio pulsando la instancia en el {{site.data.keyword.cloud_notm}} [Panel de control ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/dashboard/apps?watson){: new_window}.
- Para obtener más información y ver ejemplos sobre el SDK, consulte [Autenticación ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/natural-language-classifier?language=java#authentication){: new_window} en la consulta de API.
- Para obtener más información sobre cómo utilizar señales de IAM con servicios Watson, consulte [Autenticación con señales de IAM](/docs/services/watson?topic=watson-iam#iam).
- Para obtener más información sobre cómo utilizar claves de API de IAM con servicios Watson, consulte [Claves de API de servicio de IAM](/docs/services/watson?topic=watson-api-key-bp#api-key-bp).
- Para obtener más información sobre cómo migrar instancias de Cloud Foundry, consulte [Migración de instancias de servicio de Cloud Foundry a un grupo de recursos](/docs/resources?topic=resources-migrate#migrate).

### 19 de septiembre de 2018
{: #19september2018}

**Incorporación de limitación de uso**

- Las llamadas a API se han limitado a 1500 solicitudes por minuto por instancia de servicio. Si supera el límite, se devuelve el código de estado de HTTP `429 Demasiadas solicitudes`.

### 7 de agosto de 2018
{: #07august2018}

**Sustitución del kit de herramientas clásico**

El kit de herramientas clásico se ha dejado de utilizar el 7 de agosto de 2018 y se ha sustituido por [{{site.data.keyword.DSX}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")][watson-studio-reg]{: new_window}.

Puede [migrar](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#migrating) los datos de entrenamiento correspondientes a los clasificadores creados fuera de {{site.data.keyword.DSX}} hasta el 30 de septiembre de 2018. Después de realizar la migración, puede actualizar fácilmente los datos de entrenamiento y crear otro clasificador en {{site.data.keyword.DSX}}.

### 2 de agosto de 2018
{: #02august2018}

**Migración de los datos de entrenamiento a {{site.data.keyword.DSX}}**

Ahora puede [migrar](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#migrating) los datos de entrenamiento correspondientes a los clasificadores creados fuera de {{site.data.keyword.DSX}}. Después de realizar la migración, puede actualizar fácilmente los datos de entrenamiento y crear otro clasificador en {{site.data.keyword.DSX}}.

Puede migrar datos hasta el 30 de septiembre de 2018.

### 6 de julio de 2018
{: #06july2018}

**Nueva herramienta beta disponible: {{site.data.keyword.DSX}}**

{{site.data.keyword.DSX}} es el nuevo entorno integrado que incluye un sustituto para el kit de herramientas {{site.data.keyword.nlclassifiershort}} clásico. Para empezar a trabajar con {{site.data.keyword.DSX}}, pulse **Iniciar herramienta** desde el panel de control de una instancia de servicio de {{site.data.keyword.nlclassifiershort}}. Para obtener detalles, consulte [Gestión de clasificadores con {{site.data.keyword.DSX}}](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#studio).

{{site.data.keyword.DSX}} da soporte no solo a {{site.data.keyword.nlclassifiershort}}, sino también a {{site.data.keyword.visualrecognitionshort}} y a muchos otros servicios y recursos de {{site.data.keyword.cloud_notm}}. {{site.data.keyword.DSX}} proporciona un entorno de colaboración en la nube. Con {{site.data.keyword.DSX}}, los desarrolladores, los expertos en la materia, los científicos de datos y otros pueden crear y entrenar {{site.data.keyword.nlclassifiershort}} y otros modelos de IA. También puede utilizar {{site.data.keyword.DSX}} para probar los clasificadores.

Puede utilizar {{site.data.keyword.DSX}} con todas las instancias y clasificadores existentes de {{site.data.keyword.nlclassifiershort}}. El kit de herramientas clásico está disponible hasta el 7 de agosto de 2018.

### 8 de junio de 2018
{: #08june2018}

**Descarga de datos de entrenamiento para la nueva herramienta**

Está previsto que el kit de herramientas clásico de {{site.data.keyword.nlclassifiershort}} existente deje de funcionar el 31 de julio de 2018. El sustituto planificado para el kit de herramientas es **{{site.data.keyword.DSX}}**, el nuevo entorno integrado. [{{site.data.keyword.DSX}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")][watson-studio-reg]{: new_window} ya da soporte a {{site.data.keyword.visualrecognitionshort}} y a otros servicios y recursos de {{site.data.keyword.cloud_notm}}.

Esperamos que todos los clasificadores existentes estén disponibles en {{site.data.keyword.DSX}}. Sin embargo, si desea asegurarse de que puede volver a crear los clasificadores existentes, descargue los datos de entrenamiento del kit de herramientas clásico antes del 31 de julio de 2018.

Para aquellos que utilicen la [API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/natural-language-classifier){: new_window} directamente, no hay ningún cambio con la migración de la herramienta.

### 16 de marzo de 2018
{: #16march2018}

- **Clasificar varias frases**

    Dispone de un nuevo método para **Clasificar varias frases** que permite enviar hasta 30 frases de texto en una solicitud. El método `POST /v1/classifiers/{classifier_id}/classify_collection` permite clasificar frases en los mismos idiomas que el método original excepto en japonés, para el que hay una característica beta.

    Para ver detalles sobre la llamada de API, consulte el método **Clasificar varias frases** en la [Consulta de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}.

- **Entrenamiento con conjuntos de datos de mayor tamaño**

    Ahora puede incluir un máximo de 20.000 registros en los datos de entrenamiento. El entrenamiento del clasificador se ha mejorado mediante IBM Deep Learning as a Service. Esta oferta constituye una infraestructura de entrenamiento de red neural que utiliza un clúster elástico de unidades de proceso de gráficos (GPU) para manejar conjuntos de datos mayores. El tamaño máximo de los datos de entrenamiento sigue siendo 15.000 registros para los usuarios de la ubicación de Frankfurt o los usuarios con {{site.data.keyword.Bluemix_dedicated_notm}}.

### 10 de julio de 2017
{: #10july2017}

**Idiomas adicionales:** ahora el servicio da soporte al coreando además de al árabe, inglés, francés, alemán, japonés, italiano, portugués y español. El idioma de los datos de formación debe coincidir con el idioma del texto que tiene intención de clasificar.

Para ver más información sobre idiomas, consulte el apartado sobre [Utilización de sus propios datos](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#languages). Para ver detalles sobre la llamada de API, utilice el método `Crear clasificador` de la [Consulta de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}.

### 6 de abril de 2016
{: #06april2016}

**Idiomas adicionales:** Ahora el servicio da soporte al alemán además de al árabe, inglés, francés, japonés, italiano, portugués y español. El idioma de los datos de formación debe coincidir con el idioma del texto que tiene intención de clasificar.

### 29 de febrero de 2016
{: #29february2016}

**Idiomas adicionales:** Ahora el servicio da soporte al japonés además de al árabe, inglés, francés, italiano, portugués y español.

### 7 de diciembre de 2015
{: #07december2015}

**Idiomas adicionales:** Ahora el servicio da soporte al árabe, al francés y al italiano además de al inglés, portugués y español.

### 16 de noviembre 2015
{: #16november2015}

**Idiomas adicionales:** Ahora el servicio da soporte al portugués y al español, además de al inglés.
