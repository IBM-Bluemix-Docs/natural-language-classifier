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

# Sicurezza delle informazioni 
{: #information-security}

IBM si impegna a offrire ai nostri clienti e partner soluzioni innovative per la privacy, la sicurezza e la governance dei dati.
{: shortdesc}

**Avviso:**
I clienti sono responsabili per la garanzia della propria conformità alle varie leggi e normative, incluso il Regolamento generale sulla protezione dei dati dell'Unione Europea. È responsabilità esclusiva dei clienti richiedere una consulenza legale qualificata per identificare e interpretare normative e regolamenti importanti che potrebbero influenzare le attività di business dei clienti ed eventuali azioni che i clienti dovranno intraprendere per rispettare la conformità a tali normative e regolamenti. 

I prodotti, servizi e altre funzionalità qui descritti non sono adatti per tutte le situazioni dei clienti e potrebbero avere una disponibilità limitata. IBM non fornisce consulenza legale, contabile o di controllo né dichiara o garantisce che i propri servizi o prodotti assicureranno che i clienti siano conformi ad eventuali norme di legge o regolamentari. 

## Regolamento generale sulla protezione dei dati dell'Unione europea (GDPR)
{: #gdpr}

IBM si impegna a offrire ai nostri clienti e partner soluzioni innovative per la privacy, la sicurezza e la governance dei dati per assisterli nel loro percorso verso la conformità GDPR. 

È possibile trovare ulteriori informazioni sul percorso di preparazione verso la disponibilità GDPR e sulle nostre funzionalità e offerte GDPR che supportano il tuo percorso di conformità [qui ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/gdpr){: new_window}.

## Etichettatura ed eliminazione dei dati in {{site.data.keyword.nlclassifiershort}}
{: #gdpr-in-service}

{{site.data.keyword.nlclassifiershort}} non supporta i dati personali nei dati di formazione quando crei un classificatore. Non deve essere inserito alcun dato personale nei dati di formazione. Inoltre, non viene acquisito o conservato alcun dato quando classifichi una o più frasi.

I dati di formazione vengono archiviati per il ciclo di vita del classificatore. Per eliminare i dati di formazione associati al classificatore, utilizza il metodo **Delete classifier** per rimuovere il classificatore.
