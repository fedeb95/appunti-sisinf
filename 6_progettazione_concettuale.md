# Progettazione concettuale
Introduce gli elementi dimenisonali nello schema globale riconciliato in seguito all'integrazione.

* Identificazione di fatti, misure e  dimenisoni
* Derivazione di un grafo dimenisonale
* Input per la progettazione logica

## Il Dimensional Fact Model DFM
Si tratta di un modello concettuale grafico per DW, pensato per:
* supportare il progetto concettuale
* creare una rappresentazione da cui partire per il progetto logico
* documentazione

### DMF: costrutti base
* **Fatto**: concetto di interesse per il processo decisionale, tipicamente un insieme di eventi. Deve essere dianmico, evolvere nel tempo
* **Dimensione**: proprietà con dominio finito di un fatto, ne descrive una coordinata di analisi
* **Misura**: proprietà numerica di un fatto, aspetto quantitativo di interesse

### Altri costrutti
* **Attributo dimensionale**: un ulteriore attributo, a valori discreti, che descrive una dimensione di analisi
* **Gerarchia**: albero direzionato i cui nodi sono attributi dimensionali, gli archi modellano associazioni molti a uno (dipendenze funzionali) tra attributi
* Attributo dscrittivo: contiene informazioni aggiuntive, ma non significativo per l'aggregazione. Sono sempre foglie della gerarchia ~~ovviamente~~.
* Archi opzionali: l'associazione non è definita per un sottoinsieme di eventi (e.g. l'attributo dieta assume valori solo per i prodotti alimentari, null negli altri casi). Indicato con un tratto sull'arco.

### Eventi
* **Evento primario**: particolare occorrenza di un fatto, ennupla con un valore per ogni dimensione
* **Evento secondatio**: insieme di eventi primari, ennupla di attributi dimensionali, aggrega gli eventi primari corrispondenti, con un opportuno operatore
* Pattern: combinazione di attributi dimensionali, denota una prospettiva di analisi

~~Un evento primario sta a un evento secondario come un evento sta a un gruppo di eventi secondo un certo pattern~~

### Aggregazione
L'aggregazione richiede di definire opportuni operatori per comporre i valori delle misure. Queste si suddividono, in base a quali operatori sono applicabili, in:

* Misure di flusso: sempre aggregabili con la somma
* Misure di livello: non ha senso sommarle sula gerarchia temporale, ma sulle altre gerarchie (e.g. numero di abitanti in città al ...)
* Misure unitarie: non si possono mai sommare, espresse in termini relativi (e.g. percentuale)

#### Additività
Una misura è detta additiva su una dimensione se i suoi valori possono essere sommati lungo la corrispondente gerarchia. Se una misura è di flusso non è specificato, altrimenti vengono indicati gli operatori utilizzabili, con un arco tratteggiato tra misura e attributo, etichettato col nome dell'operatore.

#### Convergenza
Rappresenta un vincolo d'integrità, due archi finiscono nello stesso attributo dimensionale. E.g, lo stato di un distretto è lo stesso di un negozio.

#### Gerarchia condivisa
Nodo in comune fra due gerarchie, i dati però sono diversi. Indicato con un cerchio all'interno del nodo e due o più frecce verso lo stesso.

#### Schemi di fatto vuoti
Uno schema di fatto è vuoto se non ci sono misure corrispondenti. In questo caso registra semplicemente il verificarsi di eventi. L'informazione di un evento secondario è il numero di eventi primari (COUNT).

## Progettazione concettuale di DW: come
Passi di progettazione:

* definizione dei fatti
* per ogni fatto:
  * [costruzione](#costruzione-albero) **albero degli attributi**
  * [**editing**](#editing-albero) dell'albero
  * definizione delle [**dimensioni**](#definizione-dimensioni)
  * definizione delle [**misure**](#definizione-misure)
  * creazione dello [**schema**](#creazione-schema) di fatto

### Definizione dei fatti
Tipicamente sono eventi che accadono dinamicamente. Dipende dai requisiti dell'analisi, può corrispondere ad un'entità o una relazione da reificare.

### Albero degli attributi
* La **radice** corrisponde all'identificatore del **fatto**
* Ogni **vertice** è un **attributo** dello schema sorgente
* Per ogni vertice *v*, il corrispondente attributo determina funzionalemnte i discendenti di *v*

#### <a name="costruzione-albero"></a>Costruzione dell'albero degli attributi
* Può essere fatta in modo automatico, navigando ricorsivamente le dipendenze funzionali espresse nello schema sorgente dalle associazioni 1:1
* Per ogni entità *E*, si crea nell'albero un vertice *v* corrispondente all'identificatore ~~alla chiave~~ di *E* e si aggiunge un figlio per ogni altro attributo di *E*
  * Per ogni relazione R con cardinalità massima pari a 1 e diretta verso un'entità *G*, si aggiungono a *v* tanti figli quanti sono gli attributi di *R*, poi ricorsione su *G*, rendendo l'identificatore di *G* figlio di *v*

Si parte dal fatto *F*.
#### <a name="editing-albero"></a>Editing
In genere non tutti gli attributi sono d'interesse per il DM, quindi l'albero viene modificato tramite:

* **Potatura**: si elimina il sottoalbero con radice in v
* **Innesto**: si collegano tutti i figli di v al padre v', eliminando v. Utile se v non interessa ma i suoi figli sì

L'editing porta ad un'alterazione delle granularità, rendendo necessaria una pre aggregazione.

#### <a name="definizione-dimensioni"></a> Definizione delle dimensioni
Le dimensioni vanno scelte tra i figli della radice. La loro scelta è cruciale perché definisce la granularità degli eventi primari. Il tempo corrisponde sempre ad una dimensione. Se non presente nelle sorgenti, viene aggiunto come timestamp del caricamento dei dati nel DW.

#### <a name="definizione-misure"></a>Definizione delle misure
Le misure sono i figli della radice che non sono dimensioni.
Altrimenti sono definite applicando funzioni di aggregazione ad attributi numerici dell'albero.

#### <a name="creazione-schema"></a>Creazione dello schema di fatto
L'albero degli attributi, una volta fatto l'editing, viene tradotto in uno schema di fatto:

* le gerarchie corrispondono ai sottoalberi dell'albero degli attributi, con le dimensioni come radice
* è possibile potare e innestare per eliminare dettagli inutili
* è possibile aggiungere attributi dimensionali (e.g. tempo)
* Gli attributi non utilizzati per l'aggregazione diventano descrittivi
* i figli della radice che non sono né misure né dimensioni
  * se la granularità conincide con quella dell'entità di F, attributi descrittivi
  * altrimenti devono essere potati
* identificazione di eventuali non additività
