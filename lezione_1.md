# Introduzione
## Cos'è un SI
Insieme di dati, processi e strumenti per la loro acquisizione,
memorizzazione ed elaborazione, durante i processi aziendali.

## Evoluzione dei SI
I primi SI trattavano dati strutturati in formati predefiniti,
automatizzando attività ad alta proceduralità, come amministrazione o contabilità.

Successivamente il SI ha assunto un ruolo di rilievo nel supporto alle
decisioni per processi direzionali, trattando anche tipi di dati non strutturati come testo o immmagini, fino ai più recenti IoT e Big Data.

### Sistemi informativi operativi e di supporto alle decisioni
Un sistema informativo è operativo se pienamente automatizzato, mentre di supporto alle decisioni se un operatore utilizza lo strumento come supporto per la gestione.

# Suddivisione dei sistemi informativi
Ci sono diverse prospettive per analizzare un sistema informativo:

* [Modello organizzativo](#modello-organizzativo): a cosa serve
* [Modello funzionale](#modello-funzionale): che cosa fa
* [Modello informatico](#modello-informatico): come è fatto

## <a name="modello-organizzativo"></a>Modello organizzativo
Risponde alla domanda: *"A che cosa serve il SI?"*

Secondo questo modello, o punto di vista, i sistemi informativi sono classificabili come:

* [SI operativi](#si-operativi)
* [SI istituzionali](#si-istituzionali)
* [SI direzionali](#si-direzionali)

### <a name="si-operativi"></a>SI operativi
Un sistema informativo operativo informatizza processi volti all'esecuzione di attività, chiamati anche *Transaction operative systems*<a name="transaction-operative"></a>.
Per esempio potrebbe occuparsi della costruzione di un prodotto assemblandone le parti.

Il ruolo del SI è proporzinale all'intensità informativa del settore, per esempio è più importante in un'azienda di telecomunicazione che non in un'azienda manifatturiera.

### <a name="si-istituzionali"></a>SI istituzionali

Sono di supporto ad attività gestionali, indispensabili per l'esecuzione dei processi produttivi, ma non parte di essi.

### <a name="si-direzionali"></a>SI direzionali

Supportano il management aziendale nei processi direzionali, sono quindi di supporto alle decisioni. Sono basati sui [SI operativi](#si-operativi), dai quali importano deti elementari per produrre dati aggregati o indici. Un SI del genere può essere usato, per esempio, per cercare strategie per l'incremento delle vendite, etc.

Sono utilizzati nel modello del ciclo di controllo:
1. Definizione obiettivi del processo
2. Analisi dei risultati ottenuti
3. Definizione di azioni correttive

#### Business Intelligence
SI direzionali per la Business Intelligence analizzano i dati aziendali per ricavare nuove regole di business:
* Analisi dei clienti: profilazione
* Analisi del prodotto: affidabilità
* Analisi delle prestazioni: processi gestionali e produttivi

## <a name="modello-funzionale"></a>Modello funzionale
Risponde alla domanda: *"Che cosa fa il SI?"*

Secondo questo modello, un SI può essere descritto dalle seguenti prospettive:

* [Modello dei casi d'uso](#modello-casi-uso)
* [Modello dei processi](#modello-processi)
* [Modello dei dati](#modello-dati)

### <a name="modello-casi-uso"></a>Modello dei casi d'uso
Specifica le interazioni tra attori e sistema, solitamente UML. Descrive i requisiti delle singole elaborazioni.

Possono essere correlati ai processi (e ai dati) tramite un'estesione di UML, **Assembly Lines**, presenta ogni use case unito al processo corrispondente e ai dati da esso elaborati.

### <a name="modello-processi"></a>Modello dei processi
Activity Diagram

### <a name="modello-dati"></a>Modello dei dati
I dati si dividono in:

* Dati anagrafici: parte *statica* del SI, descrive le proprietà strutturali del dominio
* Dati dinamici: parte *dinamica*, eventi registrati (o [transazioni](#transaction-operative))
* Indici: risultati di elaborazioni periodiche.

## <a name="modello-informatico"></a>Modello informatico
Risponde alla domanda: *"Come è realizzato ~~implementato~~ il SI?"*

Fornisce una descrizione del sistema informativo attraverso:

* [Modello applicativo](#modello-applicativo)
* [Modello tecnologico](#modello-tecnologico)

### <a name="modello-applicativo">Modello applicativo
Formato da diversi strati:

1. Strato di presentazione: descrive l'interazione finale con  l'utente, solitamente tramite GUI basate sul web-based
2. Logica applicativa: procedure con cui i dati acquisiti tramite GUI o base dati sono elaborati
3. Strato dei dati: strumenti per definire le basi di dati e accedere ai dati (DBMS)

### <a name="modello-tecnologico">Modello tecnologico
* Architettura hardware: insiemi dei sistemi hardware, architettura client-server la più utilizzata
* Architettura di rete: infrastruttura di rete usata per trasmettere le informazioni
