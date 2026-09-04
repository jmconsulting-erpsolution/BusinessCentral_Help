# JM Pick And Stock - Documentazione funzionale

**Nome applicazione:** JM Pick And Stock
**Publisher:** JM Consulting
**Versione:** 27.0.1.1
**ID applicazione:** 33a49749-ebb8-4b74-8585-4921b6a6c846
**Piattaforma di destinazione:** Business Central 27.0.0.0
**Distribuzione cloud:** Sì

---

## 1. Riepilogo esecutivo

**JM Pick And Stock** estende le funzionalità standard di Business Central per
supportare le operazioni di prelievo, stoccaggio e movimentazione di magazzino.
Centralizza le righe logistiche collegate ai documenti aziendali e consente agli
operatori di lavorare con quantità, ubicazioni e tracciabilità direttamente
dalle pagine operative.

Le capacità principali sono:

- gestione dei prelievi per vendite, trasferimenti, resi, assistenza e produzione;
- gestione dello stoccaggio e della ricezione delle merci;
- scansione di codici a barre per articoli, lotti, matricole, colli e ubicazioni;
- gestione di colli, pesi, dimensioni e numerazione delle spedizioni;
- tracciabilità di lotto, matricola e confezione durante ogni attività;
- controlli a più stati (Aperto, Verificato, Elaborato);
- collegamento diretto ai documenti standard e alle relative righe logistiche.

L'applicazione utilizza il modulo di magazzino standard di Business Central e
aggiunge controlli, pagine operative e azioni adatte agli addetti di magazzino.

## 2. Funzionalità principali

### 2.1 Sistema di gestione dei prelievi

Le righe di prelievo rappresentano le attività di uscita da eseguire. L'utente
può generarle dal documento sorgente, assegnare ubicazioni e tracciabilità,
registrare le quantità effettivamente prelevate e completare il ciclo solo dopo
i controlli previsti.

Funzioni disponibili:

- creazione e gestione delle righe da più documenti sorgente;
- gestione di lotto, matricola e numero confezione;
- controllo in tempo reale di quantità e ubicazioni;
- flusso **Aperto → Verificato → Elaborato**;
- selezione dell'ubicazione e dell'ubicazione di destinazione;
- inserimento manuale o tramite scansione barcode;
- conferma del prelievo prima della registrazione della spedizione;
- possibilità di riaprire una riga per correggere un'attività.

Documenti supportati:

- ordini di vendita e relative righe;
- archivi degli ordini di vendita;
- ordini di trasferimento;
- ordini di reso acquisto;
- ordini e righe di assistenza;
- componenti degli ordini di produzione;
- ordini di assemblaggio;
- spedizioni di magazzino e spedizioni registrate;
- righe di pianificazione commessa e relativi archivi;
- pagine principali degli ordini di vendita e di acquisto.

### 2.2 Sistema di gestione dello stoccaggio

Le righe di stoccaggio rappresentano le attività di ingresso, ricezione,
put-away e riclassificazione. L'operatore registra la quantità ricevuta,
l'ubicazione di destinazione e gli eventuali dati di tracciabilità prima della
registrazione del documento.

Funzioni disponibili:

- creazione e gestione delle attività di stoccaggio;
- assegnazione dell'ubicazione di magazzino;
- movimentazione tra ubicazioni e riclassificazione;
- controllo delle quantità ricevute, stoccate e riclassificate;
- flusso **Aperto → Verificato → Elaborato**;
- inserimento e verifica tramite barcode;
- conferma dello stoccaggio prima della registrazione.

Documenti supportati:

- ordini di acquisto e relative righe;
- righe degli ordini di reso acquisto;
- ordini di trasferimento;
- ricevute di magazzino e ricevute registrate;
- righe e componenti degli ordini di produzione;
- ordini di assemblaggio;
- giornali di riclassificazione articolo;
- ordini e righe di assistenza.

### 2.3 Gestione delle righe logistiche

La tabella **JM Logistic Lines** è il motore centrale delle attività Pick e
Stock. Ogni riga conserva il riferimento al documento sorgente e i dati
necessari per eseguire, verificare e registrare la movimentazione.

**Tipi di attività:**

- **Pick:** operazioni di uscita e prelievo;
- **Stock:** operazioni di ingresso, stoccaggio e riclassificazione.

**Attributi della riga:**

- numero articolo e codice variante;
- quantità per unità, quantità richiesta e quantità elaborata;
- codice ubicazione, codice collocazione e collocazione di destinazione;
- numero lotto, numero di matricola e numero confezione;
- tipo, numero e numero riga del documento di magazzino;
- stato dell'attività;
- utente assegnatario e date/ore di lavorazione.

Le pagine **JM Logistic Lines**, **JM Inbound Lines** e **JM Outbound Lines**
offrono rispettivamente la vista completa, quella delle attività in ingresso e
quella delle attività in uscita.

### 2.4 Gestione dei colli

La pagina **JM Parcels** consente di seguire i colli dalla preparazione del
prelievo alla spedizione. I colli possono essere creati automaticamente o
manualmente e possono contenere quantità provenienti da più righe.

- creazione e numerazione automatica dei colli;
- registrazione di peso e dimensioni;
- supporto a spedizioni suddivise in più colli;
- tracciamento del collo e collegamento alla spedizione;
- ricalcolo del peso dopo la registrazione delle quantità effettive.

In **JM Setup** sono configurabili la serie numerica dei colli e i controlli
per consentire la registrazione di spedizioni e ricevute di vendita, acquisto e
trasferimento.

### 2.5 Operazioni in ingresso

Da **JM Inbound Lines** l'utente può:

- usare **Pianifica** per creare le righe logistiche;
- usare **Aggiorna** per aggiornare descrizioni e metadati;
- aprire i dati logistici o il documento sorgente;
- completare o riaprire una riga;
- usare **Scansione barcode** per inserire rapidamente i dati.

### 2.6 Operazioni in uscita

Da **JM Outbound Lines** l'utente può:

- calcolare la disponibilità di inventario;
- creare le righe logistiche con **Pianifica**;
- verificare e completare le righe di prelievo;
- aprire il documento sorgente;
- riaprire una riga per correggerla;
- usare le interfacce di scansione barcode V1 o V2.

### 2.7 Integrazione barcode

La scansione riduce l'inserimento manuale e gli errori di digitazione. Sono
supportati:

- numeri articolo;
- numeri lotto;
- numeri matricola;
- numeri confezione o collo;
- codici collocazione;
- codici ubicazione.

Il tipo di riclassificazione barcode configurato determina se la scansione
avanza automaticamente all'articolo successivo, richiede dati aggiuntivi o
raggruppa articoli simili.

## 3. Oggetti principali e architettura

### 3.1 Codeunit principale

**JM Pick And Stock Mgt (ID 61940)** contiene la logica applicativa per:

- creare, controllare e confermare righe Pick e Stock;
- validare quantità e collocazioni;
- gestire la tracciabilità articolo;
- elaborare riclassificazioni;
- reagire alle modifiche dei documenti sorgente.

Tra le procedure principali figurano `CheckPick()`, `ConfirmPick()`,
`ReclassCheckPick()` e `ProcessPick()`, oltre alle procedure equivalenti per
le attività di stoccaggio.

### 3.2 Tabelle estese

L'estensione **User Setup** aggiunge le autorizzazioni operative per Pick e
Stock: abilitazione della gestione, verifica ed elaborazione, cancellazione
delle righe chiuse, parametri di riclassificazione e ruolo di superutente.

L'estensione **JM Setup** aggiunge la serie colli, i controlli di registrazione
per spedizioni/ricezioni e il tipo di riclassificazione barcode.

### 3.3 Enumerazioni

**JM Activity Type (Enum 61940)**:

- **Pick:** attività di prelievo in uscita;
- **Stock:** attività di stoccaggio in ingresso.

## 4. Componenti dell'interfaccia utente

### 4.1 Pagine principali

| Pagina | ID | Tipo | Utilizzo |
|---|---:|---|---|
| JM Inbound Lines | 61940 | Lista | Attività logistiche in ingresso |
| JM Logistic Lines | 61941 | Lista | Vista centrale di Pick e Stock |
| JM Outbound Lines | 61942 | Lista | Attività di prelievo in uscita |
| JM Parcels | 61943 | Lista | Colli e spedizioni |

Le pagine sono disponibili dal menu dell'applicazione e da **Cerca (Tell Me)**.

### 4.2 Estensioni pagina

L'applicazione aggiunge azioni e dati logistici alle pagine standard per:

- impostazioni utente e **JM Setup**;
- ordini di vendita, acquisto, reso e trasferimento;
- ordini e righe di assistenza;
- componenti, righe rilasciate e righe finite di produzione;
- ordini di assemblaggio;
- ricevute, spedizioni e righe di magazzino registrate;
- giornale di riclassificazione articolo;
- righe di pianificazione commessa;
- Business Manager, Order Processor, Warehouse Manager e Whse. Basic Role
  Center;
- scheda ubicazione e pagina di dialogo JM.

Le azioni principali sono **Logistic Line (Pick JM)**, **Logistic Line (Stock
JM)**, **Logistic Line (JM)** e **Barcode Scan**. Le pagine di dialogo mostrano
inoltre data attività, utente, quantità nuova e quantità massima.

## 5. Flussi operativi

### 5.1 Flusso tipico di un prelievo

1. Rilasciare l'ordine sorgente nel flusso standard di Business Central.
2. Aprire la riga del documento e scegliere **Logistic Line (Pick JM)**.
3. Verificare le righe create in **JM Logistic Lines (Pick)**.
4. Inserire o scansionare articolo, lotto, matricola e confezione.
5. Inserire quantità e collocazione di prelievo.
6. Eseguire **Check Pick** per validare dati e quantità.
7. Eseguire **Confirm Pick** per confermare l'attività.
8. Eseguire **Process Pick** per elaborare la riga.
9. Registrare la spedizione con il processo standard.
10. Verificare che le righe risultino completate.

### 5.2 Flusso tipico di uno stoccaggio

1. Creare la ricevuta o il documento di ingresso.
2. Creare le righe Stock dalle righe della ricevuta.
3. Aprire **JM Logistic Lines (Stock)**.
4. Scansionare l'articolo e indicare collocazione e tracciabilità.
5. Inserire la quantità da stoccare.
6. Eseguire **Check Stock** e correggere eventuali anomalie.
7. Eseguire **Confirm Stock**.
8. Eseguire **Process Stock**.
9. Registrare la ricevuta nel processo standard.
10. Verificare l'aggiornamento dell'inventario e delle collocazioni.

### 5.3 Flusso di riclassificazione

1. Aprire il giornale di riclassificazione articolo.
2. Usare **Barcode Scan** per inserire gli articoli.
3. Indicare ubicazione/collocazione di origine e destinazione.
4. Verificare le righe Stock generate per la riclassificazione.
5. Spostare gli articoli e confermare le attività.
6. Elaborare le righe e registrare il giornale.
7. Verificare i nuovi contenuti delle collocazioni.

## 6. Configurazione e impostazioni

### 6.1 Impostazioni utente

In **User Setup**, l'amministratore configura per ogni utente:

| Impostazione | Funzione |
|---|---|
| Enable Pick Mgt. | Creazione ed esecuzione dei prelievi |
| Enable Checked Pick | Verifica dei prelievi |
| Enable Processed Pick | Elaborazione dei prelievi |
| Enable Stock Mgt. | Creazione ed esecuzione dello stoccaggio |
| Enable Checked Stock | Verifica dello stoccaggio |
| Enable Processed Stock | Elaborazione dello stoccaggio |
| Delete Lines Process Closed | Cancellazione delle righe elaborate/chiuse |
| Template Riclass Item | Modello per riclassificazione articolo |
| Batch Riclass Item | Parametri di elaborazione batch |
| Enable AutoPost Riclass. | Registrazione automatica della riclassificazione |
| Pick & Stock SuperUser | Accesso completo alle funzioni Pick e Stock |

### 6.2 Impostazioni di sistema

In **JM Setup**, sezione Pick & Stock:

| Impostazione | Funzione |
|---|---|
| Parcel Nos. | Serie numerica per i colli |
| Allow Tran. Ship. Posting | Consente la registrazione della spedizione trasferimento |
| Allow Tran. Rcpt. Posting | Consente la registrazione della ricezione trasferimento |
| Allow Sales Ship. Posting | Consente la registrazione della spedizione vendita |
| Allow Purch. Rcpt. Posting | Consente la registrazione della ricezione acquisto |
| BarcodeScan Reclass. Type | Comportamento della riclassificazione da barcode |

Prima di usare i colli configurare **Parcel Nos.**. Impostare i controlli di
registrazione in base alla separazione dei compiti adottata dal magazzino.

## 7. Permessi e sicurezza

L'accesso è controllato dai permessi standard di Business Central e dai campi
di **User Setup**. Assegnare solo le capacità necessarie al ruolo:

- gli operatori possono creare e registrare attività abilitate;
- i verificatori possono eseguire i controlli Pick o Stock;
- i responsabili possono elaborare le righe e gestire le eccezioni;
- il superutente può operare su tutte le funzioni e correggere le righe chiuse.

Le righe conservano utente e data/ora delle operazioni. I controlli di
registrazione in **JM Setup** impediscono di registrare documenti non consentiti
dal processo aziendale. La tracciabilità di lotto e matricola continua a usare
le funzionalità standard di Business Central.

## 8. Integrazioni

### 8.1 Business Central

JM Pick And Stock è collegato a ordini, ricevute, spedizioni, documenti di
magazzino, righe di assistenza, commesse, produzione, assemblaggio e giornali
di riclassificazione. La registrazione aggiorna le registrazioni articolo, le
disponibilità, le prenotazioni, le collocazioni e i dati di tracciabilità
standard.

### 8.2 JM Utility Base

**JM Utility Base (27.0.0.0)** è la dipendenza richiesta. Fornisce dialoghi,
definizioni condivise, impostazioni comuni e funzioni di utilità usate
dall'applicazione.

## 9. Caratteristiche operative

- **Stati controllati:** Aperto, Verificato ed Elaborato.
- **Quantità flessibili:** conversioni per unità, quantità parziali e quantità
  elaborate residue.
- **Tracciabilità avanzata:** combinazione di lotto, matricola e confezione.
- **Gestione collocazioni:** assegnazione, validazione e movimentazione
  collocazione-collocazione.
- **Controllo qualità:** verifica obbligatoria, gestione discrepanze e
  riapertura prima della registrazione.
- **Ricalcolo inventario:** controllo della disponibilità prima dei prelievi.

## 10. Integrazione con i Role Center

Sono estesi i seguenti Role Center:

1. Business Manager;
2. Order Processor;
3. Warehouse Manager;
4. Whse. Basic.

Le estensioni aggiungono accesso rapido alle righe logistiche e alla gestione
delle attività in ingresso e in uscita.

## 11. Scansione dei codici a barre

### 11.1 Interfacce

- **V1:** interfaccia standard per l'inserimento dell'articolo;
- **V2:** interfaccia estesa con ulteriori conferme e validazioni.

### 11.2 Dati acquisibili

Articoli, lotti, matricole, confezioni, colli, collocazioni e ubicazioni.

### 11.3 Tipo di riclassificazione

Il tipo configurato può richiedere dati aggiuntivi, passare all'articolo
successivo o raggruppare articoli simili. Il comportamento deve essere scelto
in base al flusso operativo del magazzino.

## 12. Specifiche tecniche

### 12.1 Requisiti della piattaforma

- Business Central **27.0.0.0 o successivo**;
- distribuzione cloud supportata;
- runtime **16.0**;
- funzionalità `NoImplicitWith` e `TranslationFile`;
- debugging consentito;
- download del codice sorgente non consentito;
- simboli non inclusi.

### 12.2 Intervalli ID

| Intervallo | Utilizzo |
|---|---|
| 61940–61949 | Oggetti principali Pick e Stock |
| 61950–61959 | Estensioni di magazzino |
| 62020–62029 | Estensioni produzione e documenti |
| 62320–62329 | Estensioni avanzate di magazzino e documenti |

### 12.3 Dipendenze

È richiesta **JM Utility Base 27.0.0.0**. Non sono richieste altre dipendenze
esterne.

### 12.4 Localizzazione

Sono supportate le lingue inglese (en-US) e italiano (it-IT), incluse caption,
azioni, descrizioni dei campi e messaggi di errore.

## 13. Procedure consigliate

### 13.1 Prima della messa in esercizio

1. Configurare la serie numerica dei colli.
2. Definire i controlli di registrazione.
3. Configurare i permessi per ruolo e non solo per utente.
4. Impostare il tipo di riclassificazione barcode.
5. Verificare collocazioni, tracciabilità e unità di misura.

### 13.2 Durante le operazioni

1. Creare le righe logistiche dopo il rilascio del documento.
2. Non saltare lo stato **Verificato**.
3. Usare il barcode quando disponibile.
4. Mantenere il flusso Aperto → Verificato → Elaborato.
5. Confrontare sempre le quantità con il documento sorgente.
6. Controllare regolarmente le righe bloccate o non elaborate.

## 14. Scenari comuni

### 14.1 Prelievo di un ordine di vendita

Il responsabile rilascia l'ordine, crea le righe Pick dalla sottopagina
dell'ordine, l'operatore scansiona articolo e tracciabilità, inserisce quantità
e collocazione, quindi esegue verifica, conferma ed elaborazione. La spedizione
viene infine registrata nel processo standard.

### 14.2 Ricezione di un ordine di acquisto

Dalla ricevuta di magazzino si creano le righe Stock. L'operatore registra
articoli, quantità, lotti e collocazioni di destinazione, completa verifica,
conferma ed elaborazione, quindi registra la ricevuta e controlla l'inventario.

### 14.3 Spostamento tra collocazioni

Dal giornale di riclassificazione si avvia la scansione, si indicano origine e
destinazione, si elaborano le righe Stock e si registra il giornale. Il tipo
barcode configurato stabilisce il passaggio tra gli articoli.

## 15. Gestione degli errori e risoluzione dei problemi

### 15.1 Problemi comuni

**Non è possibile creare righe logistiche dall'ordine**

- verificare che il documento sia rilasciato;
- verificare che contenga almeno una riga;
- controllare `Enable Pick Mgt.` o `Enable Stock Mgt.` dell'utente.

**Le righe logistiche non sono visibili**

- rimuovere filtri di stato non appropriati;
- verificare il tipo attività Pick o Stock;
- controllare il riferimento al documento sorgente.

**Non è possibile verificare, confermare o elaborare**

- completare tutti i campi obbligatori;
- controllare che la quantità non superi quella del documento;
- verificare i permessi Checked e Processed del relativo tipo attività;
- riaprire la riga se è necessario correggere i dati.

**La scansione produce un risultato inatteso**

- verificare il formato del codice e il codice articolo;
- controllare lotto, matricola, collocazione e ubicazione;
- verificare il tipo di riclassificazione barcode in JM Setup.

**La registrazione è bloccata**

- controllare il relativo flag Allow Posting in JM Setup;
- verificare che l'attività sia stata elaborata;
- controllare disponibilità, tracciabilità e quantità residue.

### 15.2 Risorse di supporto

- documentazione: `docs/JM Pick And Stock/`;
- guida e pagine di configurazione: guida in-app di Business Central;
- supporto: [www.jmconsulting.it](http://www.jmconsulting.it/).

## 16. Informazioni sulla versione

| Versione | Data | Descrizione |
|---|---|---|
| 27.0.1.1 | Corrente | Release di produzione per Business Central 27 |
| 27.0.1.0 | Precedente | Versione di produzione precedente |

**Versione del documento:** 1.0
**Ultimo aggiornamento:** 2026-09-04
**Stato:** Corrente

## 17. Changefix

| Data | Modifica |
|---|---|
| 2026-09-04 | Creata la traduzione italiana della documentazione funzionale di JM Pick And Stock. |
