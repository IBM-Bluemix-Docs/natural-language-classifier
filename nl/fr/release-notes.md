---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-16"

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

# Notes sur l'édition
{: #release-notes}

Les nouvelles fonctions et modifications apportées au service
ci-après sont disponibles.
{: shortdesc}

## Fonctions bêta
{: #beta}

{{site.data.keyword.IBM_notm}} propose, pour évaluation, des services, des fonctions et une prise en charge de langue, qui sont en version bêta. Ces fonctions peuvent être instables, changer fréquemment ou être arrêtées dans un délai très court. Les fonctions bêta, qui risquent de ne pas fournir le même niveau de performances ou de compatibilité que les fonctions de l'édition GA (General Availability), ne sont pas destinées à être utilisées dans un environnement de production. Les fonctions bêta sont prises en charge uniquement sur [IBM Developer Answers ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/answers/topics/natural-language-classifier.html){: new_window}.

## Modifications
{: #changelog}

Les nouvelles fonctions et modifications apportées au service
ci-après sont disponibles.

### 25 janvier 2019
{: #25jan2019}

**L'emplacement de Francfort prend désormais en charge l'apprentissage avec des données plus volumineuses**

L'apprentissage des instances de service {{site.data.keyword.nlclassifiershort}} hébergées à Frankfort peut désormais s'effectuer sur des ensembles de données plus vastes. Vous pouvez inclure jusqu'à 20 000 enregistrements dans vos données d'apprentissage.

La plus grande taille de données est désormais prise en charge dans tous les emplacements {{site.data.keyword.nlclassifiershort}}. Pour plus d'informations sur les données d'apprentissage, [Préparation des données](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data).

### 13 novembre 2018
{: #18November2018}

**Nombre maximum de classes**

Les données d'apprentissage prennent désormais en charge un maximum de 3 000 classes, même si un nombre inférieur de classes se traduit par de meilleures performances. Pour plus d'informations, voir [Préparation des données](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#training-limits) et [Meilleures pratiques en matière de discriminants](/docs/services/natural-language-classifier?topic=natural-language-classifier-best-practices-overview#training-guidelines).

### 9 novembre 2018
{: #9November2018}

**Nouvel emplacement de Tokyo**

Vous pouvez désormais créer des instances de service {{site.data.keyword.nlclassifiershort}} à Tokyo.

### 30 octobre 2018
{: #30october2018}

Le 30 octobre 2018, les emplacements du sud des Etats-Unis et d'Allemagne sont passés à l'utilisation de l'authentification IAM (Identity and Access Management, gestion des identités et des accès) basée sur des jetons. {{site.data.keyword.nlclassifiershort}} a migré chaque emplacement aux dates suivantes :

- Sud des Etats-Unis (Dallas) : 30 octobre 2018
- Allemagne (Francfort) : 30 octobre 2018
- Est des Etats-Unis : 12 octobre 2018

La migration vers l'authentification IAM affecte différemment les nouvelles instances de service et celles existantes :

- Avec des instances de service *new* que vous créez dans les emplacements et aux dates indiqués ci-dessus, vous vous authentifiez auprès de l'API à l'aide d'IAM. Vous pouvez transmettre un jeton bearer dans un en-tête d'autorisation ou une clé d'API. Les jetons prennent en charge les demandes authentifiées sans incorporer des données d'identification de service dans chaque appel. Les clés d'API utilisent l'authentification de base.

    Lorsque vous utilisez l'un des logiciels SDK de {{site.data.keyword.watson}}, vous pouvez transmettre la clé d'API et laisser le SDK gérer le cycle de vie des jetons.
- Avec des instances de service *existantes* créées avant les dates indiquées, vous continuez à vous authentifier en fournissant le nom d'utilisateur et le mot de passe de l'instance de service. Vous pouvez utiliser ces services jusqu'à octobre 2019, date à laquelle vous devrez migrer vers IAM.

Informations complémentaires :
- Pour savoir quel processus d'authentification utiliser avec vos instances de service, affichez les données d'identification du service en cliquant sur l'instance dans le [tableau de bord {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/dashboard/apps?watson){: new_window}.
- Pour plus d'informations et des exemples concernant le logiciel SDK, voir [Authentification ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/natural-language-classifier?language=java#authentication){: new_window} dans la référence d'API.
- Pour plus d'informations sur l'utilisation de jetons IAM avec des services Watson, voir [Authentification avec des jetons IAM](/docs/services/watson?topic=watson-iam#iam).
- Pour plus d'informations sur l'utilisation de clés d'API IAM avec des services Watson, voir [Clés d'API de service IAM](/docs/services/watson?topic=watson-api-key-bp#api-key-bp).
- Pour plus d'informations sur le processus de migrations d'instances Cloud Foundry, voir [Migration d'instances de service Cloud Foundry vers un groupe de ressources](/docs/resources?topic=resources-migrate#migrate).

### 19 septembre 2018
{: #19september2018}

**Introduction d'une limitation de débit**

- Les appels API sont désormais limités à 1 500 demandes par minute par instance de service. Si vous dépassez cette limite, le code d'état HTTP `429 Too Many Requests` est renvoyé.

### 7 août 2018
{: #07august2018}

**Remplacement du kit d'outils classique**

Le kit d'outils classique a été abandonné le 7 août 2018 et remplacé par [{{site.data.keyword.DSX}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")][watson-studio-reg]{: new_window}.

Vous pouvez migrer les données d'apprentissage des discriminants créées en dehors de {{site.data.keyword.DSX}} jusqu'au 30 septembre 2018. Après migration, vous pouvez facilement mettre à jour les données d'apprentissage et créer un autre discriminant dans {{site.data.keyword.DSX}}.

### 2 août 2018
{: #02august2018}

**Migration de vos données d'apprentissage vers {{site.data.keyword.DSX}}**

Vous pouvez désormais migrer les données d'apprentissage des discriminants créées en dehors de {{site.data.keyword.DSX}}. Après migration, vous pouvez facilement mettre à jour les données d'apprentissage et créer un autre discriminant dans {{site.data.keyword.DSX}}.

Vous pouvez migrer les données jusqu'au 30 septembre 2018.

### 6 juillet 2018
{: #06july2018}

**Nouvel outil bêta disponible : {{site.data.keyword.DSX}}**

{{site.data.keyword.DSX}} est le nouvel environnement intégré qui inclut le remplacement de l'ancien kit d'outils {{site.data.keyword.nlclassifiershort}} classique. Pour vous familiariser avec {{site.data.keyword.DSX}}, cliquez sur **Launch tool** à partir d'un tableau de bord d'instance de service {{site.data.keyword.nlclassifiershort}}. Pour plus d'informations, voir [Gestion des discriminants avec {{site.data.keyword.DSX}}](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#studio).

{{site.data.keyword.DSX}} prend en charge non seulement {{site.data.keyword.nlclassifiershort}} mais également {{site.data.keyword.visualrecognitionshort}} ainsi que de nombreux autres services et ressources {{site.data.keyword.cloud_notm}}. {{site.data.keyword.DSX}} offre un environnement collaboratif dans le cloud. Avec {{site.data.keyword.DSX}}, les développeurs, experts de domaine, spécialistes des données et autres professionnels peuvent générer et expérimenter {{site.data.keyword.nlclassifiershort}} et d'autres modèles d'intelligence artificielle. Vous pouvez également utiliser {{site.data.keyword.DSX}} pour tester vos discriminants.

Vous pouvez utiliser {{site.data.keyword.DSX}} avec toutes vos instances et tous vos discriminants {{site.data.keyword.nlclassifiershort}} existants. Le kit d'outils classique reste disponible jusqu'au 7 août 2018.

### 8 juin 2018
{: #08june2018}

**Téléchargement de vos données d'apprentissage pour le nouvel outil**

L'abandon du kit d'outils {{site.data.keyword.nlclassifiershort}} classique existant est prévu pour le 31 juillet 2018. Le kit d'outils sera remplacé par **{{site.data.keyword.DSX}}**, le nouvel environnement intégré. [{{site.data.keyword.DSX}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")][watson-studio-reg]{: new_window} prend déjà en charge {{site.data.keyword.visualrecognitionshort}} ainsi que d'autres services et ressources {{site.data.keyword.cloud_notm}}.

Nous prévoyons que tous vos discriminants existants soient disponibles dans {{site.data.keyword.DSX}}. Cependant, pour vous assurer de pouvoir recréer vos discriminants existants, téléchargez les données d'apprentissage à partir du kit d'outils classique avant le 31 juillet 2018.

Pour ceux qui utilisent directement l'[API![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/natural-language-classifier){: new_window}, aucun changement n'est à noter concernant la migration de l'outil.

### 16 mars 2018
{: #16march2018}

- **Classification de plusieurs phrases**

    Une nouvelle méthode, **Classify multiple phrases**, est disponible. Elle prend en charge l'envoi de jusqu'à 30 phrases de texte dans une même demande. La méthode `POST /v1/classifiers/{classifier_id}/classify_collection` prend en charge la classification des phrases dans les mêmes langues que la méthode d'origine, sauf pour le japonais, qui se lance en tant que fonction bêta.

    Pour plus d'informations sur l'appel d'API, voir la méthode **Classify multiple phrases** dans la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}.

- **Apprentissage avec des ensembles de données plus volumineux**

    Vous pouvez désormais inclure jusqu'à 20 000 enregistrements dans vos données d'apprentissage. L'apprentissage des discriminants a été amélioré avec l'apprentissage en profondeur sous forme de service d'IBM. Cette offre est une infrastructure de formation aux réseaux neuronaux qui utilise un cluster élastique d'unités de traitement graphique pour gérer des ensembles de données volumineux. La taille maximale des données d'apprentissage est maintenue à 15 000 enregistrements pour les utilisateurs de Frankfort ou ceux disposant d'{{site.data.keyword.Bluemix_dedicated_notm}}.

### 10 juillet 2017
{: #10july2017}

**Langues supplémentaires :** désormais, le service prend en charge l'arabe, l'anglais, le français, l'allemand, le japonais, l'italien, le portugais et l'espagnol. La langue des données d'apprentissage doit correspondre à celle du texte que vous prévoyez de classifier.

Pour des détails sur les langues, voir [Utilisation de vos propres données](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#languages). Pour des détails sur l'appel d'API, voir la méthode `Create classifier` dans la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}.

### 06 avril 2016
{: #06april2016}

**Langues supplémentaires :** désormais, le service prend en charge l'allemand en plus de l'arabe, de l'anglais, du français, du japonais, de l'italien, du portugais et de l'espagnol. La langue des données d'apprentissage doit correspondre à celle du texte que vous prévoyez de classifier.

### 29 février 2016
{: #29february2016}

**Langues supplémentaires :** désormais, le service prend en
charge le japonais en plus de l'arabe, de l'anglais, du français, de
l'italien, du portugais et de l'espagnol.

### 7 décembre 2015
{: #07december2015}

**Langues supplémentaires :** désormais, le service prend en
charge l'arabe, le français et l'italien en plus de l'anglais, du portugais et de
l'espagnol.

### 16 novembre 2015
{: #16november2015}

**Langues supplémentaires :** désormais, le service prend en
charge le portugais et l'espagnol en plus de l'anglais.
