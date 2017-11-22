# Processo gestionale

Un BP (Business process) definisce il modo di operare dell'azienda. L'architettura funzionale di un SI d'impresa rispecchia l'architettura funzionale dei processi gestionali. Quindi il modello più diffuso è quello dei BP.

La modellazione dei BP avviene a diversi livelli di astrazione:

* [Architettura aziendale](#architettura-aziendale): visione complessiva
* [Architettura dei processi](#architettura-processi): dettaglio intermedio
* [Architettura dell'attività](#architettura-attivita): singole attività

Un processo gestionale è un insieme di attività (o task) interconnesse per il raggiungimento di un obiettivo. Un BP è sempre connesso a un cliente che riceve i risultati in risposta a una richiesta.

Il cuore di un BP sono le *attività*: ad esse associate ci sono le organizzazioni che le eseguono, anche esterne all'azienda (e.g. Amazon gestisce venditori esterni).

### <a name="diagramma-craso"></a>Diagramma CRASO

* **C**liente
* **R**ichiesta
* **A**ttività
* **S**ystems (Organizzazioni)
* **O**utput

Due rombi contengono richiesta e output. Le attività sono nodi interconnessi, divise in rettangoli, le organizzazioni. Il cliente fa la richiesta e ottiene l'output.


## <a name="architettura-aziendale"></a>Architettura aziendale
Descrive i processi di un'azienda.
Una rappresentazione è un albero così formato:

1. La **radice** è l'**azienda**
2. I **nodi** sono **classi di processi**
3. Le **foglie** sono i **processi**

Fondamentale per capire quali aree sono informatizzabili e quindi per la realizzazione dei sistemi informativi.

## <a name="architettura-processi"></a> Architettura dei processi
Individua le attività di un processo. Rappresentazione:

* [Diagramma di gerarchia](#diagramma-gerarchia)
  1. La **radice** è il **processo**
  2. Le **foglie** sono le singole **attività**
* [Diagramma di flusso](#diagramma-flusso): relazioni di sequenza fra le attività

Definisce quali attività sono svolte, da chi e con quale output.

### <a name="diagramma-gerarchia"></a>Diagramma di gerarchia
La radice è il processo, mentre suoi figli sono le attività che lo compongono. I filgi di ogni attività possono essere:

* sotto-attività, corrispondenti a *PART_OF*
* specializzazioni, corrispondenti a *IS_A*

Si distinguono con colori diversi attività dell'impresa, attività esterne e specializzazioni.

### <a name="diagramma-flusso"></a>Diagramma di flusso
Descrive i comportamenti dinamici, è una versione più ricca del [diagramma CRASO](#diagramma-craso). Comprende:

* attività
* sequenza
* scelta
* input/output
* organizzazioni (in UML pools)

Le attività sono in ordine temporale o di scelta, ognuna posizionata nel pool che se ne occupa. Input e output sono in rombi.

## <a name="architettura-attivita"></a>Architettura delle attività
Individua i contenuti della signola attività elementare.
Un'attività può essere composta da:

* azioni compiute da persone
* azioni sul sistema

Singola **attività** descritta da:

* Diagrammi dei **casi d'uso** e diagrammi di **flusso**
* Descrizioni **testuali**

Architettura che definisce il comportamento operativo del processo.

## Struttura organizzativa
* [Macrostruttura](#macrostruttura): organigramma gerarchico dell'azienda
* [Microstruttura](#microstruttura): esplode le strutture elementari della macrostruttura
* Mansioni: compito di ciascun addetto

Sussiste una relazione molti a molti fra strutture e processi:
una struttura può partecipare a molteplici processi e un processo può coinvolgere più strutture (o addirittura organizzazioni).

La **griglia processi/strutture** indica se:
* P: la struttura partecipa attivamente al processo
* C: la struttura è cliente del processo

Sono indicati anche gli attori esterni.

### <a name="macrostruttura"></a>Macrostruttura
* Strutture dirette: svolgono attività direttamente collegate alla produzione
* Strutture indirette: svolgono attività di supporto alle strutture dirette

### <a name="microstruttura"></a>Microstruttura
~~Nella rappresentazione sono indicate anche le mansioni~~

## Tipologie di processi gestionali
I processi gestionali, in relazione alla struttura, si suddividono in:

* **Processi funzionali**: attività svolte da una sola struttura
* **Processi interfunzionali**: attori appartengono a reparti diversi della stessa organizzazione
* **Processi interaziendali**: attori appartengono a organizzazioni diverse

## Architettura aziendale dei BP
* [Processi manageriali e di analisi](#processi-manageriali): pianificazione e governo, business intelligence
* [Processi di supporto](#processi-supporto): richiesti dai primari
* [Processi primari](#processi-primari): erogazione di prodotti o servizi

T: parte sinistra manageriali, centrale primari, destra di supporto

### <a name="processi-manageriali"></a>Processi manageriali
#### Piramide di Anthony (1965)
Primo formalismo per i processi gestionali. La piramide è così formata:

* Pianificazione strategica: quali mercati entrare, quali prodotti, fissa gli obiettivi complessivi dell'impresa
* Controllo direzionale: definisce gli obiettivi economici e verifica i risultati ottenuti
* Controllo operativo: agisce in tempo reale sulle singole attività produttive, assicura che procedano nei modi prefissati

Il controllo operativo è l'unica area completamente automatizzabile.

#### <a name="teoria-simon"></a>Teoria di Simon
Rispetto ai processi decisionali, si distinguono:

* Decisioni strutturate, quando dato un input si ottiene lo stesso output (e.g. decisioni operative), può essere ricondotta ad una regola algebrica
* Decisioni non strutturate, su base soggettiva

#### Sintesi (Gorry e Scott-Morton)
Griglia attività/decisioni, per ogni livello della piramide di Anthony si definisce la classificazione di Simon.

Introducono la decisione semi-strutturata, con dati oggettivi di supporto alla decisione, ma processo decisionale non riducibile ad una regola unica.

Da qui si può ricavare la griglia di infomatizzazione per i processi manageriali:

**Strutturazione** | Strutturazione| decisione |
--------|-------------------------:||
**informazione** |**Bassa**|**Alta**
**Alta** |Informatizzazione parziale|Informatizzazione completa
**Bassa**|Memorizzazione documenti|Memorizzazione documenti

### <a name="processi-supporto"></a>Processi di supporto
Mappa, *Processi di supporto* radice, processi figli e per ognuno i vari altri processi.

### <a name="processi-primari"></a>Processi primari
Ci sono diverse teorie e modelli con obiettivi diversi:
* [Schema di Blumenthal](#schema-blumenthal)
* [Value Chain di Porter](#value-chain)
* [Schemi di settore](#schemi-settore)
* [Best Practice](#best-practice)

#### <a name="schema-blumenthal"></a>Schema di Blumenthal
Divide il *Controllo operativo* in:

* Controllo flussi fisici
* Controllo flussi amministrativi

Ognuno suddiviso nei vari processi.

#### <a name="value-chain"></a>Value Chain di Porter
Lo schema della value chain rappresenta le fasi in cui si crea il valore. Sono classificate come attività secondatie quelle che non creano direttamente valore. Ben classificate le attività primarie per l'industria manufatturiera: oggi ci sono [schemi](#schemi-settore) specifici per ogni settore.

Tra le attività primarie:

* Logistica in ingresso: recupero materie prime
* Marketing e vendite
* Logistica in uscita: consegna del prodotto finito
* Post vendita: assistenza al cliente e manutenzione

#### <a name="schemi-settore"></a>Schemi di settore (Framework)
Oggi esistono schemi specifici per ogni settore, che descrivono l'architettura dei processi gestionali in un dato settore.

#### <a name="best-practice"></a>Best practice e business map
Knowledge base di riferimento, solitamente proprietaria di un'azienda di consulenza.
