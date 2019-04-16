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

# Releaseinformationen
{: #release-notes}

Für diesen Service stehen folgende neue Features und Änderungen zur Verfügung.
{: shortdesc}

## Beta-Features
{: #beta}

{{site.data.keyword.IBM_notm}} gibt Services, Funktionen und Sprachunterstützung frei, die Sie testen können und die als Betaversionen klassifiziert sind. Diese Funktionen sind möglicherweise instabil; sie können sich häufig ändern und werden möglicherweise kurzfristig eingestellt. Beta-Features bieten eventuell nicht die gleiche Leistung oder Kompatibilität, die allgemein verfügbare Funktionen bereitstellen, und sind nicht für die Verwendung in einer Produktionsumgebung vorgesehen. Beta-Features werden ausschließlich über die Website [IBM Developer Answers  ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/answers/topics/natural-language-classifier.html){: new_window} unterstützt. 

## Änderungen
{: #changelog}

Für diesen Service stehen folgende neue Features und Änderungen zur Verfügung.

### 25. Januar 2019
{: #25jan2019}

**Am Standort Frankfurt wird jetzt das Training mit mehr Daten unterstützt**

In Frankfurt gehostete {{site.data.keyword.nlclassifiershort}}-Serviceinstanzen können jetzt mit größeren Datasets trainiert werden. Sie können bis zu 20.000 Datensätze in Ihre Trainingsdaten aufnehmen. 

Die größeren Datasets werden jetzt an allen {{site.data.keyword.nlclassifiershort}}-Standorten unterstützt. Weitere Informationen zu Trainingsdaten finden Sie in [Datenaufbereitung](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#using-your-data). 

### 13. November 2018
{: #18November2018}

**Maximale Anzahl der Klassen**

Die Trainingsdaten können nun maximal 3.000 Klassen unterstützen, obwohl weniger Klassen zu einer besseren Leistung führen können. Weitere Informationen finden Sie in [Datenaufbereitung](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#training-limits) und [Bewährte Verfahren für Klassifikationsmerkmale](/docs/services/natural-language-classifier?topic=natural-language-classifier-best-practices-overview#training-guidelines). 

### 9. November 2018
{: #9November2018}

**Neuer Standort in Tokio**

Sie können jetzt {{site.data.keyword.nlclassifiershort}}-Serviceinstanzen erstellen, die am Standort Tokio gehostet werden. 

### 30. Oktober 2018
{: #30october2018}

Am 30. Oktober 2018 wurde an den Standorten Vereinigte Staaten - Süden und Deutschland die tokenbasierte IAM-Authentifizierung eingeführt (IAM - Identity and Access Management, Identitäts- und Zugriffsmanagement). Die einzelnen Standorte für {{site.data.keyword.nlclassifiershort}} wurden an den folgenden Daten migriert: 

- Vereinigte Staaten - Süden (Dallas): 30. Oktober 2018
- Deutschland (Frankfurt): 30. Oktober 2018
- Vereinigte Staaten - Osten: 12. Oktober 2018

Die Migration auf die IAM-Authentifizierung wirkt sich auf neue und vorhandene Serviceinstanzen unterschiedlich aus: 

- Bei *neuen* Serviceinstanzen, die Sie an den oben aufgeführten Standorten und nach den oben aufgeführten Daten erstellen, authentifizieren Sie sich über IAM bei der API. Sie können entweder ein Trägertoken im Berechtigungsheader oder einen API-Schlüssel übergeben. Tokens unterstützen authentifizierte Anforderungen ohne Einbettung von Serviceberechtigungsnachweisen in jeden Aufruf. API-Schlüssel verwenden die Basisauthentifizierung. 

Wenn Sie eines der {{site.data.keyword.watson}}-SDKs verwenden, können Sie den API-Schlüssel übergeben und das Lebenszyklusmanagement der Tokens dem SDK überlassen.
- Bei *vorhandenen* Serviceinstanzen, die Sie vor den angegebenen Daten erstellt haben, authentifizieren Sie sich weiterhin durch Angabe des Benutzernamens und Kennworts für die Serviceinstanz. Sie können diese Services bis Oktober 2019 verwenden. Dann müssen Sie eine Migration auf IAM durchführen. 

Weitere Informationen:
- Wenn Sie ermitteln möchten, welcher Authentifizierungsprozess für Ihre Serviceinstanz zu verwenden ist, können Sie die Serviceberechtigungsnachweise anzeigen, indem Sie im {{site.data.keyword.cloud_notm}} [Dashboard ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/dashboard/apps?watson){: new_window} auf die Instanz klicken. 
- Weitere Informationen und Beispiele zum SDK finden Sie in [Authentifizierung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier?language=java#authentication){: new_window} in der API-Referenz. 
- Weitere Informationen zur Verwendung von IAM-Tokens mit Watson-Services finden Sie in [Mit IAM-Tokens authentifizieren](/docs/services/watson?topic=watson-iam#iam). 
- Weitere Informationen zur Verwendung von IAM-API-Schlüsseln mit Watson-Services finden Sie in [API-Schlüssel des IAM-Service](/docs/services/watson?topic=watson-api-key-bp#api-key-bp). 
- Weitere Informationen zum Migrieren von Cloud Foundry-Instanzen finden Sie in [Cloud Foundry-Serviceinstanzen in eine Ressourcengruppe migrieren](/docs/resources?topic=resources-migrate#migrate). 

### 19. September 2018
{: #19september2018}

**Begrenzung der Anforderungsrate eingeführt**

- API-Aufrufe sind jetzt auf 1500 Anforderungen pro Minute pro Serviceinstanz begrenzt. Wenn Sie den Grenzwert überschreiten, wird der HTTP-Statuscode `429 Zu viele Anforderungen` zurückgegeben. 

### 7. August 2018
{: #07august2018}

**Klassisches Toolkit ersetzt**

Das klassische Toolkit wurde am 7. August 2018 außer Betrieb gesetzt und durch [{{site.data.keyword.DSX}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")][watson-studio-reg]{: new_window} ersetzt. 

Sie können die Trainingsdaten für Klassifikationsmerkmale, die außerhalb von {{site.data.keyword.DSX}} erstellt wurden, bis zum 30. September 2018 [migrieren](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#migrating). Nach der Migration können Sie innerhalb von {{site.data.keyword.DSX}} sehr einfach die Trainingsdaten aktualisieren und weitere Klassifikationsmerkmale erstellen. 

### 2. August 2018
{: #02august2018}

**Migrieren Sie Ihre Trainingsdaten auf {{site.data.keyword.DSX}}**

Sie können jetzt die Trainingsdaten für Klassifikationsmerkmale, die außerhalb von {{site.data.keyword.DSX}} erstellt wurden, [migrieren](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#migrating). Nach der Migration können Sie innerhalb von {{site.data.keyword.DSX}} sehr einfach die Trainingsdaten aktualisieren und weitere Klassifikationsmerkmale erstellen. 

Sie können die Daten bis zum 30. September 2018 migrieren. 

### 6. Juli 2018
{: #06july2018}

**Neues Beta-Tool verfügbar: {{site.data.keyword.DSX}}**

{{site.data.keyword.DSX}} ist die neue integrierte Umgebung, die einen Ersatz für das frühere klassische {{site.data.keyword.nlclassifiershort}}-Toolkit enthält. Wenn Sie mit {{site.data.keyword.DSX}} beginnen möchten, klicken Sie auf **Tool starten** im Dashboard einer {{site.data.keyword.nlclassifiershort}}-Serviceinstanz. Weitere Informationen finden Sie in [Klassifikationsmerkmale mit {{site.data.keyword.DSX}} verwalten](/docs/services/natural-language-classifier?topic=natural-language-classifier-managing-classifiers-with-watson-studio#studio). 

{{site.data.keyword.DSX}} unterstützt nicht nur {{site.data.keyword.nlclassifiershort}}, sondern auch {{site.data.keyword.visualrecognitionshort}} und viele andere {{site.data.keyword.cloud_notm}}-Services und -Ressourcen. {{site.data.keyword.DSX}} stellt eine Umgebung für die Onlinezusammenarbeit in der Cloud zur Verfügung. Mit {{site.data.keyword.DSX}} können Entwickler, Experten, Data-Scientists und andere Personen {{site.data.keyword.nlclassifiershort}} und andere KI-Modelle trainieren. Sie können {{site.data.keyword.DSX}} auch zum Testen Ihrer Klassifikationsmerkmale verwenden. 

Sie können {{site.data.keyword.DSX}} mit allen Ihren vorhandenen {{site.data.keyword.nlclassifiershort}}-Instanzen und -Klassifikationsmerkmalen verwenden. Das klassische Toolkit bleibt bis zum 7. August 2018 verfügbar. 

### 8. Juni 2018
{: #08june2018}

**Laden Sie Ihre Trainingsdaten für das neue Tool herunter**

Gemäß Plan wird das vorhandene klassische {{site.data.keyword.nlclassifiershort}}-Toolkit am 31. Juli 2018 außer Betrieb gesetzt. Der geplante Ersatz für das Toolkit ist **{{site.data.keyword.DSX}}**, die neue integrierte Umgebung. [{{site.data.keyword.DSX}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")][watson-studio-reg]{: new_window} unterstützt bereits {{site.data.keyword.visualrecognitionshort}} und andere {{site.data.keyword.cloud_notm}}-Services und -Ressourcen. 

Wir erwarten, dass alle Ihre vorhandenen Klassifikationsmerkmale in {{site.data.keyword.DSX}} verfügbar sein werden. Wenn Sie jedoch sicherstellen möchten, dass Sie Ihre vorhandenen Klassifikationsmerkmale erneut erstellen können, laden Sie die Trainingsdaten aus dem klassischen Toolkit vor dem 31. Juli 2018 herunter. 

Für diejenigen Benutzer, die die [API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier){: new_window} direkt verwenden, bringt die Toolmigration keine Änderung mit sich. 

### 16. März 2018
{: #16march2018}

- **Mehrere Ausdrücke klassifizieren**

    Die neue Methode **Mehrere Ausdrücke klassifizieren** ist verfügbar. Sie unterstützt das Senden von bis zu 30 Textausdrücken in einer einzigen Anforderung. Die Methode `POST /v1/classifiers/{classifier_id}/classify_collection` unterstützt die Klassifizierung von Ausdrücken in denselben Sprachen wie die ursprüngliche Methode, mit Ausnahme von Japanisch, das als Beta-Feature eingeführt wird. 

    Details zum API-Aufruf finden Sie in der Beschreibung der Methode **Mehrere Ausdrücke klassifizieren** in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier#classify-multiple-phrases){:new_window}. 

- **Training mit größeren Datasets**

    Sie können nun bis zu 20.000 Datensätze in Ihre Trainingsdaten aufnehmen. Das Training von Klassifikationsmerkmalen wird jetzt durch IBM Deep Learning als Service erweitert. Dieses Angebot beinhaltet ein neuronales Netz als Trainingsinfrastruktur, das einen elastischen Cluster von GPUs (Graphics Processing Units) für die Verarbeitung größerer Datasets verwendet. Für Benutzer am Standort Frankfurt oder für Benutzer mit {{site.data.keyword.Bluemix_dedicated_notm}} bleibt die maximale Größe der Trainingsdaten unverändert bei 15.000 Datensätzen. 

### 10. Juli 2017
{: #10july2017}

**Zusätzliche Sprachen:** Der Service unterstützt nun zusätzlich zu Arabisch, Englisch, Französisch, Deutsch, Japanisch, Italienisch, Portugiesisch und Spanisch auch Koreanisch. Die Sprache der Trainingsdaten muss mit der Sprache des Textes übereinstimmen, den Sie klassifizieren wollen.

Details zu Sprachen finden Sie in [Eigene Daten verwenden](/docs/services/natural-language-classifier?topic=natural-language-classifier-using-your-data#languages). Details zum API-Aufruf finden Sie in der Methode `Create classifier` in der [API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/natural-language-classifier){:new_window}.

### 6. April 2016
{: #06april2016}

**Zusätzliche Sprachen:** Der Service unterstützt nun zusätzlich zu Arabisch, Englisch, Französisch, Japanisch, Italienisch, Portugiesisch und Spanisch auch Deutsch. Die Sprache der Trainingsdaten muss mit der Sprache des Textes übereinstimmen, den Sie klassifizieren wollen.

### 29. Februar 2016
{: #29february2016}

**Zusätzliche Sprachen:** Der Service unterstützt nun zusätzlich zu Arabisch, Englisch, Französisch, Italienisch, Portugiesisch und Spanisch auch Japanisch.

### 7. Dezember 2015
{: #07december2015}

**Zusätzliche Sprachen:** Der Service unterstützt nun zusätzlich zu Englisch, Portugiesisch und Spanisch auch Arabisch, Französisch und Italienisch.

### 16. November 2015
{: #16november2015}

**Zusätzliche Sprachen:** Der Service unterstützt nun zusätzlich zu Englisch auch Portugiesisch und Spanisch.
