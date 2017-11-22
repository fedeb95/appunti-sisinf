# Architetture Data Warehouse
Ci sono diversi livelli di rappresentazione dei dati:

* Strumenti di analisi: individuali e focalizzati usl problema in esame
* Datamart: selezione dei dati del DW, dipartimentali o settoriali
* Data Warehouse: aziendale, con dati integrati
* Sorgenti informative: dipartimentali, con dati operativi

Le sorgenti operazionali sono operative ma anche banche dati esterne. Sono, in generale, eterogenee, con differenze sintattiche e semantiche.

## Strumenti ETL

Gli strumenti di **E**xtraction, **T**ransformation e **L**oading si occupano di integrare i dati dalle diverse sorgenti in modo uniforme provenienti da sistemi diversi, quindi con descrizioni diverse. La riconciliazione avviene quando il DW viene creato e quando viene aggiornato.

## Modello multidimensionale dei dati
In questo modello, sono rilevanti:

* **Fatto**: le occorrenze dei fatti sono eventi accaduti; in ER sono relazioni fra entità
* **Misura**: proprietà numerica di un fatto, che lo descrive quantitativamente; su di esse si applicano gli operatori aggregati
* **Dimensione**: prospettiva lungo la quale effettuare l'analisi

Il modello è *denormalizzato*, rifletendo le [modalità di utilizzo](./3_business_intelligence.html#modalita-utilizzo), ottimizzato per un grande volume di dati.

Dai modelli ER va capito cosa può diventare fatto, cosa misura e cosa dimensione.

I dati multidimensionali possono essere rappresentati in cubi:

* ogni cella è un fatto e contiene un valore per ogni misura
* ogni asse è una dimensione

Con più di tre dimensioni si parla di ipercubo.

Ogni dimensione è organizzata in **gerarchie dimensionali**, con diversi livelli di aggregazione chiamati **attributi dimensionali**. Per esempio, `(regione,città,negozio)` è una gerarchia di tre attributi dimensionali in ordine crescente di dettaglio.

## Tecniche per l'analisi
Due operazioni di base sono:

* Restrizione o slicing: si riduce la dimensionalità del cubo, fissando valori per una o più dimensioni
* Aggregazione: raggruppa gli eventi in macro celle, aggregando i dati navigando la gerarchia dimensionale

## Accesso al DW
Una volta integrati i dati, ci sono tre modalità di analisi:

* reportistica: interrogazione predefinita eseguita sempre nello stesso modo e presentazione in formato grafico
* [OLAP](./3_business_intelligence.html#modalita-utilizzo): interrogazione interattiva del cubo
* [Data mining](#data-mining)

### OLAP
Una sessione OLAP è un percorso di navigazione che analizza un fatto di interesse sotto diversi aspetti, applicando vari operatori che trasformano l'interrogazione precedente:

* Roll-up: aggrega i dati
* Drill-down: disaggrega, mostrando in dettaglio
* Slice & dice: seleziona e proietta, riducendo le dimensioni e selezionando in base a condizioni
* Pivot: riorienta il cubo

### <a name="data-mining"></a> Data mining
Questa tecnica si propone di trovare informazioni nascoste nei dati, sottoforma di pattern. Individua regole di implicazione logica nei dati, quindi di individuare affinità di oggetti.
Una possibile applicazione è trovare abitudini di acquisto.

#### Rilevanza delle regole
Una regola X => Y è caratterizzta da:

* Supporto S: percentuale delle transazioni che contengono sia X che Y (rilevanza statistica)
* Confidenza C: percentuale delle transazioni che, tra quelle che contengono X, contengono anche Y (forza della regola)

Vi sono algoritmi che estreggono tutte le regole di associazione, con livelli di supporto e confidenza specificati

## Architetture per il warehousing
* Architetture a un 1 livello
  * dati operazionali
  * middleware
  * strumenti di reportistica e OLAP
* [Architetture a 2 livelli](#arch-2)
  * Dati operazionali e esterni integrati da strumenti ETL
  * Data warehouse
  * Data mart
  * reposrtistica, OLAP, data mining
* [Architetture a 3 livelli](#arch-3)
  * dati operazionali ed esterni
  * dati riconciliati
  * data warehouse
  * data mart
  * reportistica, OLAP, data mining

### <a name="arch-2"></a>Architetture a due livelli
I data mart alimentati dal DW primario sono detti dipendenti.
Sono utili, in aziende medio-grandi:

* per costruire incrementalmente il DW
* per ottimizzare le prestazioni

In alcuni contesti si adottano Data mart indipendenti alimentati direttamente dalle sorgenti, snellisce le fasi progettuali, ma rischia di generare inconsistenze.

Vantaggi:

* i dati sono disponibili anche se l'accesso alle sorgenti è precluso
* l'interrogazione analitica non interferisce con le operazioni transazionali ordinarie
* modello multidimensionale
* dati storici
* possibile applicare tecniche speciali per ottimizzare le prestazioni

### <a name"arch-3"></a>Architetture a tre livelli
Vantaggi:

* i dati riconciliati introducono un livello di dati comune per l'azienda

Svantaggi:

* i dati riconciliati sono ridondanti
