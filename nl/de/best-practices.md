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

# Bewährte Verfahren für Klassifikationsmerkmale
{: #best-practices-overview}

Wenn Sie einige Richtlinien befolgen und einige Entwurfsmuster übernehmen, können Sie die beste Erfahrung für Ihre Benutzer bereitstellen und sicherstellen, dass Ihre Anwendung die von Ihnen gewünschten Klassifizierungen verarbeiten kann. 

## Anzahl der Klassifikationsmerkmale
{: #classifier-limits}

Jede Instanz des {{site.data.keyword.nlclassifiershort}}-Service kann bis zu 8 Klassifikationsmerkmale aufweisen, die jeweils über eine eindeutige Klassifikationsmerkmal-ID verfügen. Wenn mehr als 8 Klassifikationsmerkmale unterstützt werden sollen, erstellen Sie eine weitere Instanz von {{site.data.keyword.nlclassifiershort}}. Sie können eine Serviceinstanz auf der Seite [Services durchsuchen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/developer/watson/services){: new_window} der {{site.data.keyword.watson}}-Konsole erstellen. 

## Mehrere Ausdrücke klassifizieren
{: #best-practices-multiple}

Zum Klassifizieren einer einzigen Textzeichenfolge verwenden Sie die Methode **Ausdruck klassifizieren**. Mit der Methode **Mehrere Ausdrücke klassifizieren** können Sie bis zu 30 Textausdrücke in einer einzigen Anforderung senden. Details finden Sie in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}.

## Sprachen
{: #language-support}

Obwohl die voreingestellte Sprache Englisch ist, können Sie beim Erstellen des Klassifikationsmerkmals die Sprache der Trainingsdaten angeben. Die Sprache der Trainingsdaten muss mit der Sprache des Textes übereinstimmen, den Sie klassifizieren wollen. Details finden Sie in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier#create-classifier){:new_window}.

Das Klassifikationsmerkmal unterstützt Englisch (en), Arabisch (ar), Französisch (fr), Deutsch (de), Italienisch (it), Japanisch (ja), Koreanisch (ko), Portugiesisch (Brasilien) (pt) und Spanisch (es). 

Die Klassifizierung japanischer Texte mit der Methode **Mehrere Ausdrücke klassifizieren** ist ein Beta-Feature. {: note}

## Richtlinien für ein gutes Training
{: #training-guidelines}

Folgende Richtlinien werden nicht von der API erzwungen. Das Klassifikationsmerkmal erbringt jedoch eine bessere Leistung, wenn die Trainingsdaten diese Richtlinien einhalten:

- Die Länge des Eingabetextes sollte auf weniger als 60 Wörter begrenzt sein.
- Die Anzahl der Klassen sollte einige hundert Klassen nicht übersteigen. In höheren Versionen des Service wird möglicherweise Unterstützung für eine größere Anzahl Klassen enthalten sein.
- Stellen Sie sicher, dass jede Klasse eine Übereinstimmung mit mindestens 5 - 10 Datensätzen hat, wenn jeder Textdatensatz nur eine Klasse aufweist. Diese Anzahl bietet ausreichend Training für die Klasse.
- Bewerten Sie, ob es erforderlich ist, mehrere Klassen zu haben. Zwei allgemeine Gründe sprechen für das Vorhandensein mehrerer Klassen:
    - Wenn der Text vage ist, ist die Ermittlung einer einzelnen Klasse häufig nicht eindeutig.
    - Wenn Experten den Text auf unterschiedliche Weise interpretieren, werden diese Interpretationen bei Vorhandensein mehrerer Klassen unterstützt.

    Wenn jedoch viele Texte in Ihren Trainingsdaten mehrere Klassen aufweisen oder wenn einige Texte mehr als drei Klassen aufweisen, müssen Sie die Klassen möglicherweise optimieren. Überprüfen Sie beispielsweise, ob die Klassen hierarchisch sind. Wenn sie hierarchisch sind, schließen Sie den Blattknoten als Klasse ein.
- Schließen Sie standardmäßige Begriffe mit Bindestrich ein, wenn sie Teil der Trainingsdaten sind (`back-to-back` oder ` part-time job`).

    Verbinden Sie jedoch nicht aufeinander folgende Wörter, um neue Begriffe zu erstellen, die es in der Sprache der Trainingsdaten nicht gibt. Definieren Sie zum Beispiel statt `dish-ran-away` oder `with_the_spoon` (Text aus einem Kindergedicht) die relevanten Ausdrücke als einzelne Wörter (`dish ran away` und `with the spoon`) mit der entsprechenden Klasse.

## Trainingsdaten erstellen
{: #best-practices-training-data}

Das maschinelle Lernen beschreibt einen Prozess, bei dem anhand eines Datensatzes einige Eigenschaften erlernt werden und diese Eigenschaften dann auf neue Daten angewendet werden. Der Service '{{site.data.keyword.nlclassifiershort}}' folgt diesem Prozess. Er wird trainiert, um vordefinierte Klassen mit Beispieltext zu verbinden, und er wendet diese Klassen anschließend auf neue Eingaben an.

Das trainierte Klassifikationsmerkmal ist also nur so gut wie die Trainingsdaten. Jeder Textwert in den Daten muss die Art der Texte darstellen, die das Klassifikationsmerkmal vorhersagen soll. Jede Klasse, die zurückgegeben werden soll, muss auch in den Trainingsdaten enthalten sein, und die Klassen, die Sie den einzelnen Texten zuordnen, müssen richtig sein.

Wenn es sich bei den Texten in Ihren Trainingsdaten beispielsweise um Fragen handelt, verwenden Sie Fragen, die für die Fragen Ihrer Benutzer repräsentativ und typisch sind. Sie können diese Texte aus tatsächlichen Benutzerdaten erfassen oder Sie haben Experten in Ihrem Bereich, die die Texte erstellen können.

Es ist wichtig, dass die Daten repräsentativ und korrekt sind, da die Daten der Ausgangspunkt für alle Prozesse und Ergebnisse des Klassifikationsmerkmals sind. Darüber hinaus gilt, dass das Klassifikationsmerkmal eine desto größere Chance hat, eine Übereinstimmung zu finden, je mehr Datensätze Sie in die Trainingsdaten einschließen.

## Weitere Ressourcen
{: #best-practices-next-steps}

Siehe weitere [bewährte Verfahren und Entwurfsmuster ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/watson/assets-watson/pdf/Watson-NLC-Links-Best-Practices-Design-Patterns.pdf){: new_window} für {{site.data.keyword.nlclassifiershort}}. 
