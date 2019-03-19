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

# Meilleures pratiques en matière de discriminants
{: #best-practices-overview}

En suivant certaines instructions et en adoptant certains modèles de conception, vous offrirez à vos utilisateurs la meilleure expérience possible et leur garantirez que votre application est capable de gérer les éléments qu'elle doit classifier.

## Nombre de discriminants
{: #classifier-limits}

Chaque instance du service {{site.data.keyword.nlclassifiershort}} accepte jusqu'à 8 discriminants ayant chacun un ID de discriminant unique. Pour prendre en charge plus de 8 discriminants, créez une autre instance de {{site.data.keyword.nlclassifiershort}}. Vous pouvez créer une instance de service à partir de la console {{site.data.keyword.watson}} sur la page [Browse Services ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/developer/watson/services){: new_window}.

## Classification de plusieurs phrases
{: #best-practices-multiple}

La méthode **Classify a phrase** permet de classifier une seule chaîne de texte. Avec la méthode **Classify multiple phrases**, vous pouvez envoyer jusqu'à 30 phrases de texte dans une même demande. Pour des détails, voir la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}.

## Langues
{: #language-support}

La langue par défaut est l'anglais, mais vous pouvez spécifier la langue des données d'apprentissage lorsque vous créez le discriminant. La langue des données d'apprentissage doit correspondre à celle du texte que vous prévoyez de classifier. Pour des détails, voir la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/natural-language-classifier#create-classifier){:new_window}.

Le discriminant prend en charge l'anglais (en), l'arabe (ar), le français (fr), l'allemand (de), l'italien (it), le japonais (ja), le coréen (ko), le portugais (Brésil - pt) et l'espagnol (es).

La classification de textes en japonais avec la méthode **Classify multiple phrases** est une fonction bêta.
{: note}

## Instruction pour un apprentissage réussi
{: #training-guidelines}

Les instructions ci-après ne sont pas imposées par l'API. Cependant, le
discriminant est plus performant lorsque les données d'apprentissage les respectent :

- Limitez la longueur du texte d'entrée à moins de 60 mots.
- Limitez le nombre de classes à plusieurs centaines de classes. Des versions ultérieures du service pourront prendre en charge des nombres de
classes plus élevés.
- Assurez-vous que chaque classe correspond à au moins 5 à 10 enregistrements,
où chaque enregistrement de texte est associé à une classe seulement. Ce nombre permet
un apprentissage suffisant pour la classe.
- Evaluez la nécessité d'utiliser plusieurs classes. Deux raisons fréquentes motivent
l'utilisation de plusieurs classes :
    - Lorsque le texte est vague, l'identification d'une seule classe n'est pas
toujours claire.
    - Lorsque des experts interprètent le texte de différentes façons, plusieurs
classes prennent en charge les interprétations.

    Toutefois, si de nombreux textes dans vos données d'apprentissage incluent
plusieurs classes, ou si certains textes sont associés à plus de trois classes, il
peut être nécessaire d'affiner les classes. Par exemple, déterminez si les classes sont
hiérarchiques. Si tel est le cas, incluez le noeud feuille comme classe.
- Incluez des termes standard comportant des traits d'union lorsqu'ils font
partie des données d'apprentissage (`qualité-prix` ou
`travail à
mi-temps`).

    Toutefois, n'associez pas de mots adjacents pour créer de nouveaux termes
qui n'existent pas dans la langue des données d'apprentissage. Par exemple, au lieu de
définir `le-petit` ou
`chaperon_rouge`, définissez les expressions
pertinentes à l'aide
de mots distincts (`le petit` et `chaperon rouge`) avec la classe appropriée.

## Construction des données d'apprentissage
{: #best-practices-training-data}

L'apprentissage automatique est un processus d'apprentissage de certaines
propriétés à partir d'un ensemble de données, puis d'application des propriétés à de
nouvelles données. Le service {{site.data.keyword.nlclassifiershort}} applique ce processus. Il
est entraîné pour connecter des classes prédéfinies à des exemples de texte, puis
applique ces classes à de nouvelles entrées.

Par conséquent, les performances du discriminant entraîné dépendent des données
d'apprentissage. Chaque valeur textuelle dans les données doit représenter les sortes
de texte que le discriminant doit prévoir. Chaque classe dont vous prévoyez le renvoi doit également figurer dans les données
d'apprentissage, et les classes que vous associez à chaque texte doivent être correctes.

Par exemple, lorsque les textes figurant dans vos données d'apprentissage sont des
questions, utilisez des questions classiques représentatives des questions posées par vos utilisateurs. Vous pouvez collecter ces textes à partir des données utilisateur réelles ou demander à
des spécialistes de votre domaine de créer les textes.

Cette nature représentative et précise des données est importante car elle a un
impact sur tous les processus et les résultats du discriminant. De plus, plus le nombre d'enregistrements inclus dans les données d'apprentissage est
élevé, plus le discriminant aura une chance de trouver une correspondance.

## Ressources supplémentaires
{: #best-practices-next-steps}

Pour plus d'informations, voir [Meilleures pratiques et modèles de conception![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/watson/assets-watson/pdf/Watson-NLC-Links-Best-Practices-Design-Patterns.pdf){: new_window} pour {{site.data.keyword.nlclassifiershort}}.
