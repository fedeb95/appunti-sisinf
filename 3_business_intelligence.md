# Architettura dei SI
I sistemi informativi [operativi](./1_introduzione.html#si-operativi) o [istituzionali](./1_introduzione.html#si-istituzionali) si dividono in:

* ERP: Enterprise Resource Planner
* CRM: Customer Relationship Management (distribuzione, vendita e post-vendita)

I processi si dividono in:

* operativi: [decisioni strutturate](./2_business_process.html#teoria-simon), con regole precise
* direzionali: [decisioni non strutturate](./2_business_process.html#teoria-simon),dati fortemente aggregati

Di conseguenza i sistemi informativi possono essere:

* **T**ransaction **P**rocessing **S**ystem: per processi operativi, elaborano le transazioni e i relativi dati
  * enfasi sull'automazione
  * molti utenti
  * ambito limitato, per le singole funzioni
* **D**ecision **S**upport **S**ystem: per i processi direzionali
  * enfasi sulla generazione di informazione
  * pochi utenti
  * ambito globale, a livello di impresa

## Dai dati alle informazioni

I dati aggregati sono elaborati a partire dai dati dei sistemi operativi, attraverso un processo di selezione e sintesi progressiva.

Le informazioni aggregate sono:

* Preventive: esprimono obiettivi e traguardi, estratte da piani e budget
* Consuntive: riguardano risultati effettivi, dai SI operativi (e.g. vendite)

## Business Intelligence come DSS
Essere in grado di prendere decisioni rapide e migliori sulla base di dati aggregati (indici)

Si parla più propriamente di *sistema* di BI, in quanto sono necessari:

* Hardware dedicato
* Infrastrutture di rete
* DBMS
* Software di back-end
* Software di front-end

Il ruolo chiave di una piattaforma di BI è la trasformazione di dati aziendali in informazioni fruibili a diversi livelli di dettaglio.

## Data Warehousing
Collezione di metodi, tecnologie e strumenti di ausilio al *knowledge worker* per condurre analisi dei dati.

Requisiti:

* **Accessibilità** a utenti con conoscenze limitate di informatica
* **Integrazione** dei dati da database diversi, strutturati in modi diversi
* **Flessibilità** di integrazione
* **Sintesi** per analisi mirate ed efficaci
* Rappresentazione **multidimensionale**, intuitiva ed efficacemente manipolabile, soprattutto in tempo e area geografica
* **Correttezza e completezza** dei dati integrati

## Data Warehouse
Cuore del data warehousing, collezione di dati di supporto al processo decisionale che richiede una modellazione specifica, finalizzata all'analisi dei dati.

Quindi un DW dev'essere:

* orientato ai **soggetti**: tiene conto di chi lo utilizza
* **integrato** e consistente: vi confluiscono dati da diversi sistemi operazionali
  * come inserirli?
  * come renderli consistenti fra loro?
* **tempo** fondamentale: tiene conto di tutte le transazioni
* **non volatile**

### <a name="modalita-utilizzo"></a> Modalità di utilizzo
Le modalità di utilizzo di una base dati sono:

* **O**n**L**ine **T**ransaction **P**rocessing:
  tradizionale modalità, dati di dettaglio aggiornati, proprietà ACIDE
* **O**n**L**ine **A**nalytical **P**rocessing:
  operazioni complesse ed estemporanee, dati storici, operazioni di sola lettura
