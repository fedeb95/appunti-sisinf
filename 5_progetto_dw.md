# Progetto DW
Nel progettare un DW, sono possibili due approcci:

* [Top-down](#top-down)
* [Bottom-up](#bottom-up)

### <a name="top-down"></a>Approccio top-down
Vantaggi:

  * promette ottimi risultati perché si basa su una visione globale

Svantaggi:

  * il preventivo di costi onerosi e i lunghi tempi di attesa scoraggiano dall'intraprendere il progetto
  * affrontare contemporaneamente analisi e riconciliazione di tutte le sorgenti è estremamente complesso
  * impossibile prevedere le necessità di tutte le aree, l'analisi rischia una paralisi
  * non consegnare un prototipo in poco tempo porta disinteresse

### <a name="bottom-up"></a>Approccio bottom-up
Vantaggi:

* risultati concreti in tempi brevi
* ridotti investimenti finanziari
* permette di studiare solo le problematiche del data mart in oggetto
* fornisce un riscontro immediato sull'utilità del sistema
* mantiene elevata l'attenzione sul progetto

Svantaggi:
* visione parziale del dominio di interesse

## Ciclo di sviluppo
* Definizione obiettivi e pianificazione
* Progettazione infrastruttura
* Iterativamente, progettazione e sviluppo dei data mart

Il primo data mart da prototipare deve essere quello più importante per l'azienda, appoggiandosi su fonti di dati già disponibili e consistenti.

La progettazione di un DM/DW è diversa da una normale base di dati:

* i dati hanno caratteristiche diverse
* vincolata dalle basi di dati esistenti
* guidata da criteri differenti

## Progettazione
Attività principali:

* [Analisi](#analisi)
* [Integrazione](#integrazione)
* Progettazione
  * concettuale
  * logica
  * fisica

### <a name="analisi"></a>Analisi
I dati in ingresso sono:
* requisiti: le esigenze aziendali
* descrizione delle basi di dati aziendali
* descrizione di altre sorgenti informative

Analisi delle sorgenti operazionali:
* Selezione delle sorgenti informative
* Traduzione in un modello concettuale di riferimento
* Analisi delle sorgenti informative

## <a name="integrazione"></a>Integrazione
Fusione dei dati in un'unica base di dati globale. Scopo dell'integrazione è identificare tutte le porzioni di diverse sorgenti che si riferiscono a uno stesso aspetto della realtà, per riconciliarle. Vanno identificati, analizzati e risolti i conflitti.

Il risultato è uno schema riconciliato, in seguito è necessario completare la rappresentazione dei concetti dimensionali, implementare un modello logico e creare indici per ottimizzare le prestazioni.

### Reverse Engineering
Per ragionare su schemi eterogenei è necessario un formalismo comune, cioè un modello concettuale. Questo va derivato dagli schemi logici delle basi di dati. Il reverse engineering è svolto in modo semiautomatico.

### Analisi delle sorgenti operazionali
Il progettista acquisisce una conoscenza delle sorgenti attraverso:

* ricognizione: esame approfondito degli schemi
* normalizzazione: correggere gli schemi locali per modellare meglio il sistema applicativo (e.g. dipendenze funzionali implicite)

### Integrazione di schemi
L'integrazione è orientata all'identificazione, analisi e risoluzione di conflitti, tramite:
* individuazione delle **corrispondenze** tra i concetti in **schemi diversi**
* definizione di un'**unica rappresentazione** globale
* creazione di un **unico schema**

### Strategie di integrazione
* **Strategia Binaria**: si parte da due sorgenti, riconciliate in uno schema intermedio, poi riconciliato con un'altra, fino allo schema finale
* **Strategia N-aria**: si deriva lo schema finale direttamente da tutte le sorgenti
* **Strategia mista**: n sorgenti formano schemi intermedi, riconciliati in vari passi a quello finale

Tramite Schema matching vengono trovati i matching concept tra due schemi e **proprietà interschema** (vincoli tra concetti di schemi differenti e.g. subset), poi unificati tramite allineamento e fusione.

#### Conflitti
* Terminologici:
  * Omonimi: stesso nome, ma significati diversi
  * Sinonimi: nomi diversi, ma stesso significato
* Strutturali: stesso concetto, ma costrutti diversi
  * di chiave: identificatori diversi per lo stesso nome
  * di dipendenza: correlazione con vincoli diversi (1,N invece che 1,1 etc)
* Semantici: stessa porzione di mondo reale, ma a diversi livelli di astrazione

#### Matching concept
* Identità: usato lo stesso costrutto
* Equivalenza: costrutti diversi, ma equivalenti
* Compatibilità: i costrutti e i punti di vista dei progettisti non sono in contrasto fra loro
* Incompatibilità: gli schemi sono in contrasto a causa di incoerenza nelle specifiche

#### Unificazione
Scopo di questa fase è la risoluzione dei conflitti per giungere ad una rappresentazione unificata.
Non sempre i conflitti possono essere risolti, viene chiesto all'utente.
In caso di incertezza si preferiscono le trasformazioni che avvantaggiano gli schemi più importanti per il DM.

Esempio: Entità PRODOTTO(Prezzo) del database di produzione, entità PRODOTTO(Prezzo) del database delle vendite -> entità PRODOTTO(Prezzo-prod,Prezzo-vendita).

Per fondere gli schemi si utilizzano le proprietà inter-schema, esempio: in un db IMPIEGATO, nell'altro MANAGER, relazione di inclusione manager -> impiegato.
