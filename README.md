# LocalTypst

**LocalTypst** è un editor [Typst](https://typst.app) per il desktop, pensato per lavorare in locale: scrivi a sinistra, vedi il documento a destra, aggiornato mentre digiti. I tuoi file restano sul tuo computer. Quando vuoi, puoi **scrivere insieme ad altre persone in tempo reale** (collaborazione P2P cifrata) e **sincronizzare le cartelle con GitHub**.

**Piattaforme:** Windows 10/11 · Fedora (.rpm) · Ubuntu/Debian (.deb) · altre distribuzioni Linux (AppImage)
**Ultima versione:** vedi [Releases → Latest](https://github.com/caccapuzz-klipper/localtypst-releases/releases/latest)
**Lingua dell'interfaccia:** italiano

> Questo repository contiene **solo gli installer** di LocalTypst e il file usato per gli aggiornamenti automatici. Il codice sorgente è privato.

---

## Indice

1. [Download e installazione](#download-e-installazione)
2. [Aggiornamenti automatici](#aggiornamenti-automatici)
3. [Primi passi](#primi-passi)
4. [Editor e anteprima](#editor-e-anteprima)
5. [Funzioni di scrittura](#funzioni-di-scrittura)
6. [Esportazione PDF e avanzata](#esportazione-pdf-e-avanzata)
7. [Preambolo, file inclusi e importazione (Pandoc)](#preambolo-file-inclusi-e-importazione-pandoc)
8. [Collaborazione P2P](#collaborazione-p2p)
9. [GitHub: backup, sincronizzazione e cronologia](#github-backup-sincronizzazione-e-cronologia)
10. [Impostazioni](#impostazioni)
11. [Scorciatoie da tastiera](#scorciatoie-da-tastiera)
12. [Domande frequenti e risoluzione problemi](#domande-frequenti-e-risoluzione-problemi)
13. [Privacy](#privacy)

---

## Download e installazione

Scarica il file adatto al tuo sistema dalla pagina **[Releases → Latest](https://github.com/caccapuzz-klipper/localtypst-releases/releases/latest)**, sezione *Assets*.

| Sistema | File | Note |
| :-- | :-- | :-- |
| Windows 10/11 | `LocalTypst_Setup.exe` | **Consigliato.** Installa l'app e, se manca, anche il componente di sistema WebView2. |
| Windows 10/11 | `LocalTypst.exe` | Versione portatile: nessuna installazione. Richiede che WebView2 sia già presente (lo è su Windows 10/11 aggiornati). |
| Fedora e derivate | `LocalTypst-linux-x86_64.rpm` | Pacchetto `.rpm`. |
| Ubuntu / Debian e derivate | `LocalTypst-linux-amd64.deb` | Pacchetto `.deb`. |
| Altre distribuzioni Linux | AppImage | Non richiede installazione. |

### Windows

1. Scarica `LocalTypst_Setup.exe` ed eseguilo (oppure avvia direttamente `LocalTypst.exe` per la versione portatile).
2. **Avviso SmartScreen.** L'app non è firmata con un certificato a pagamento, quindi al primo avvio Windows può mostrare la schermata *"Windows ha protetto il PC"*. Non significa che il file sia pericoloso: clicca su **Ulteriori informazioni** e poi su **Esegui comunque**.

### Fedora

```bash
sudo dnf install ./LocalTypst-linux-x86_64.rpm
```

### Ubuntu / Debian

```bash
sudo apt install ./LocalTypst-linux-amd64.deb
```

### Altre distribuzioni (AppImage)

```bash
chmod +x LocalTypst*.AppImage
./LocalTypst*.AppImage
```

### Nota per Linux: interfaccia che si blocca o va in crash

Su alcune combinazioni di Wayland e driver grafici l'interfaccia può bloccarsi o chiudersi subito. In questo caso avvia l'app così:

```bash
WEBKIT_DISABLE_DMABUF_RENDERER=1 localtypst
```

Per l'AppImage usa lo stesso prefisso davanti al file (`WEBKIT_DISABLE_DMABUF_RENDERER=1 ./LocalTypst*.AppImage`).

---

## Aggiornamenti automatici

> **Dalla versione 0.5.0.** Chi ha una versione precedente deve installare la 0.5.0 a mano una volta (scaricandola da Releases); da lì in poi gli aggiornamenti arrivano da soli.

LocalTypst controlla da solo se esiste una nuova versione: il primo controllo avviene pochi secondi dopo l'apertura di un documento, poi ogni 6 ore circa.

Quando c'è un aggiornamento compare, sotto la barra in alto dell'editor, un banner **"Nuova versione disponibile!"** con i pulsanti:

- **Aggiorna ora**: scarica l'aggiornamento mostrando una barra di avanzamento. Il pacchetto viene **verificato con una firma crittografica**: se la firma non corrisponde, l'aggiornamento viene rifiutato.
- **Più tardi**: nasconde il banner per questa sessione.
- **Riavvia e Applica**: compare a download finito; chiude e riapre l'app sulla nuova versione.

Come si applica l'aggiornamento dipende dal sistema:

- **Windows:** l'aggiornamento viene installato e l'app si riavvia.
- **Linux AppImage:** il file AppImage si sostituisce da solo.
- **Linux `.rpm` / `.deb`:** viene richiesta la **password di sistema** (finestra di autenticazione `pkexec`) per installare il nuovo pacchetto.

**Quando il riavvio viene rimandato.** Per non rischiare di perdere lavoro, il riavvio per aggiornare è **bloccato mentre è attiva una stanza P2P** (esci prima dalla collaborazione) **o mentre è in corso un push Git**. L'app te lo segnala con un messaggio; riprova appena la condizione è finita. Prima del riavvio l'app salva su disco il file aperto.

Se un collaboratore usa una versione incompatibile con la tua, compare un avviso con il pulsante **Verifica aggiornamenti** per forzare il controllo.

> Se preferisci aggiornare a mano, scarica l'installer nuovo da Releases e installalo sopra quello esistente: documenti e impostazioni restano al loro posto.

---

## Primi passi

### La Dashboard

All'avvio vedi la **Dashboard**, la home con tutte le tue cartelle (progetti). In alto a sinistra c'è il tuo profilo (nome e icona, modificabili dalle Impostazioni), poi:

- **Spazio personale**: i tuoi progetti solo locali.
- **Ambienti condivisi**: gruppi di cartelle condivise con altre persone (vedi [Collaborazione P2P](#collaborazione-p2p)).
- Il pulsante **+** per creare o collegare un ambiente condiviso, il pulsante per collegare una singola cartella condivisa e l'ingranaggio per le **Impostazioni**.

Nell'area principale trovi le sezioni **I miei progetti** e **Condivisi con me**, con:

- **Cerca nelle cartelle…**: filtra per nome.
- **Vista Griglia / Vista Lista** (la lista mostra *Nome Progetto*, *Stato*, *Ultima Modifica*, *File*, *Azioni*).
- **Ordina per:** *Ultima modifica* oppure *Nome*.
- Pulsanti e cursore per **ridurre o ingrandire le miniature** (la grandezza si imposta anche nelle Impostazioni).
- **Riordina cartelle** (vedi sotto).

### Creare un documento o una cartella

Dalla Dashboard hai tre punti di partenza:

1. **Nuova cartella** (foglio bianco): scrivi il nome (per esempio `Relazione_Fisica`) e clicca **Crea Cartella**.
2. **Inizia da un file**: importa un documento esistente (.docx, .md, .tex) con la procedura di importazione. Dal menu a tendina accanto trovi anche **Apri cartella esistente da PC**, per aprire una cartella Typst che hai già altrove.
3. **Cartella Condivisa P2P**: collega una cartella che un'altra persona ha condiviso con te, con il suo codice di invito.

Ogni cartella è un progetto Typst con un file di avvio (di solito `main.typ`). Se usi un file di avvio diverso, sulla scheda compare un segnaposto 📌.

### Azioni su ogni cartella

Passando il mouse su una cartella (o dalla vista lista) hai:

- **Apri progetto**
- **Esporta PDF rapido**
- **Duplica progetto**
- **Configura progetto**: rinomina, cambia posizione (spazio personale o ambiente condiviso) ed **Elimina progetto** (con conferma; elimina i file dal computer).
- **Salva copia nelle cartelle solo locali**: crea una copia personale e scollegata dalla condivisione.

Un puntino azzurro sulla cartella indica che è condivisa in rete P2P. Puoi anche **trascinare** una cartella su uno spazio (personale o ambiente) per spostarla o per crearne una copia.

### Dove sono i file

Tutti i documenti stanno in `Documenti/LocalTypst/projects` (la cartella *Documenti* del tuo utente), organizzati così:

```
Documenti/LocalTypst/projects/
├── Personali/
│   └── <nome cartella>/
└── Ambienti/
    └── <nome ambiente>/
        └── <nome cartella>/
```

Sono normali file e cartelle: puoi aprirli con altri programmi o farne copie di sicurezza come per qualsiasi altro file. Le cartelle di servizio dell'app (per esempio `_recupero`, `_conflitti`) non compaiono come progetti.

**Riordina cartelle.** Se hai cartelle create con versioni precedenti dell'app (direttamente dentro `projects`), il pulsante **Riordina cartelle** mostra prima un'anteprima di cosa verrebbe spostato in `Personali` e `Ambienti\<ambiente>`; poi clicca **Sposta N cartelle** per confermare. I nomi non cambiano, quindi condivisione P2P, GitHub e cronologia continuano a funzionare, anche per gli altri PC che possono restare con l'ordine vecchio.

---

## Editor e anteprima

Aprendo un progetto ottieni l'editor: **codice a sinistra, anteprima a destra**, con un divisorio trascinabile. In alto ci sono i menu **File**, **Edit** e **View**, il percorso del file aperto, e a destra i pulsanti rapidi per **P2P**, **GitHub** ed **Esporta PDF**. In basso, la barra di stato.

### Anteprima live

- Il documento viene **compilato di continuo mentre scrivi**: l'anteprima si aggiorna da sola, senza premere nulla.
- All'apertura può comparire per un istante **"Anteprima salvata · compilazione in corso"**: sono le pagine dell'ultima sessione, mostrate subito mentre il documento viene ricompilato.
- **Errori e avvisi** compaiono nel pannello laterale **Warnings & Errors** (con il conteggio nella barra di stato); ogni voce indica il file e la riga del progetto, e un clic porta il cursore nel punto giusto, anche se l'errore è in un altro file.
- I pacchetti `@preview/...` vengono scaricati e messi in cache da soli quando servono (la prima volta serve la connessione a internet).

### Dall'anteprima al codice

| Cosa | Come |
| :-- | :-- |
| **Andare al punto nel codice** | **Doppio clic** su un elemento dell'anteprima: il cursore salta alla riga corrispondente (anche in un altro file del progetto). Si disattiva in *Impostazioni → P2P & Profilo → "Doppio click sull'anteprima salta al codice"*. |
| **Seguire un link interno o una voce di indice** | Doppio clic: l'anteprima scorre alla pagina collegata. |
| **Seleziona testo** | Pulsante nella barra dell'anteprima (o comando "Seleziona testo dall'anteprima (due clic)" della palette): clicca dove inizia e poi dove finisce il testo; la selezione compare nell'editor. Se i due punti sono in file diversi l'app lo segnala. **Esc** annulla. |
| **Copia codice dall'anteprima** | Pulsante **Copia codice**, oppure tieni premuto **Alt** e **trascina un rettangolo** sulle pagine: il codice sorgente di quella parte finisce negli appunti. **Esc** per uscire. |
| **Allinea anteprima al cursore** | Menu **Azioni** della barra dell'editor: porta l'anteprima nel punto in cui stai scrivendo. |

### Zoom, pagine e visualizzazione

- **Zoom**: pulsanti **−** e **+**, oppure **Ctrl + rotellina** sull'anteprima. Un clic sulla percentuale la reimposta (98%).
- **Adatta alla larghezza** e **Adatta alla pagina intera** (anche dal menu *View* → *Adatta Pagina (98%)* e dalla palette comandi).
- **Navigazione pagine**: frecce pagina precedente/successiva, campo per digitare il numero di pagina (Invio) e menu a tendina per scegliere una pagina o un capitolo.
- **Documento a tutto schermo** (**F11**; *Esci da Tutto Schermo* o **Esc** per tornare).
- **Inverti colori del foglio** (studio notturno): scurisce l'anteprima senza toccare il PDF esportato.
- **Modalità compatta**: se la finestra è stretta (meno di circa 1100 pixel) l'editor mostra **o il codice o l'anteprima** con due schede **Codice / Anteprima**; **Ctrl+Shift+E** passa dall'una all'altra.

### Pannello laterale e file

La barra laterale ha questi pannelli:

- **Files**: albero dei file del progetto. In alto: **Nuovo File (.typ)**, **Nuova Cartella**, menu **Altre opzioni**. Per ogni elemento: rinomina, elimina, e su una cartella **Importa documento con Pandoc**. Puoi selezionarne più d'uno ed eliminarli con **Canc**. La larghezza si regola trascinando il bordo.
- **Cerca nel progetto** (**Ctrl+Shift+F**): ricerca in tutti i file, con opzione *Maiuscole/Minuscole*.
- **Outline**: indice dei titoli del documento; un clic porta il cursore sul titolo.
- **Warnings & Errors**: diagnostica della compilazione.
- **Preambolo dei file inclusi**: compare solo nei file che usano `#include` (vedi [sotto](#preambolo-file-inclusi-e-importazione-pandoc)).

Si nasconde e si mostra con **Ctrl+Shift+B** (o dal menu *View* → *Nascondi/Mostra Pannello Laterale*).

### Barra degli strumenti dell'editor

Sopra il codice trovi i pulsanti per inserire al volo: **Impostazioni testo** (`#set text(...)`), **Grassetto**, **Corsivo**, **Sottolineato**, **Formatta** (formattazione automatica con Typstyle), **Titolo**, **Elenco puntato**, **Elenco numerato**, **Formula matematica**, **Blocco di codice**, **Riferimento** (`@label`).

Il menu **Azioni** raccoglie:

- **Inserisci Tabella (#table)…**: scegli righe e colonne passando su una griglia (con l'opzione *Intestazione*).
- **Trova e Sostituisci** (Ctrl+F).
- **Commenta / Decommenta (//)**.
- **Allinea anteprima al cursore**.
- **Trova definizione simbolo** (Ctrl+Alt+D).
- **Importa con Pandoc…**
- **Pulizia automatica immagini orfane**.

### Menu File, Edit, View

- **File**: Nuovo File, Nuova Cartella, Apri Cartella dal PC, Mostra in Esplora Risorse, **Salva File Corrente** (Ctrl+S), **Esporta PDF**, **Esporta Avanzato (PDF/SVG)**, **Pacchetti Typst Universe**, Pulizia Immagini Orfane, **Applica Template Typst**, **Auto-risolvi percorsi immagini**, **Importa Documento (Markdown / LaTeX)**, **Pulisci Duplicati P2P**.
- **Edit**: Trova e Sostituisci, **Tavolozza Simboli & Snippet** (Ctrl+K), Commenta/Decommenta riga, Grassetto, Corsivo, Formula Matematica.
- **View**: Documento a Tutto Schermo, pannello laterale, zoom anteprima.

### Altre funzioni dell'editor

- **Palette comandi** (**Ctrl+Shift+P**): scrivi nel campo *"Cerca un comando…"* e trovi le funzioni dell'editor, comprese quelle nascoste nelle barre (esporta PDF, cronologia versioni, GitHub, P2P, impostazioni, nuovo file o cartella, pannelli, trova e sostituisci, zoom, tutto schermo, inverti colori, seleziona testo, copia codice, modalità concentrazione, pulizia duplicazioni).
- **Modalità concentrazione** (**F9**, tasto modificabile): nasconde barre e pannelli e lascia solo editor e anteprima. Lo stesso tasto per uscire, oppure il pulsante **Esci dalla modalità concentrazione**.
- **Salvataggio**: le modifiche vengono scritte su disco poco dopo che smetti di scrivere; **Ctrl+S** forza il salvataggio immediato.
- **Autocompletamento**: suggerimenti mentre digiti funzioni Typst, etichette (`@...`) e altro; **Tab** o **Invio** accettano il suggerimento.
- **Slash snippet**: digita `/` per scegliere blocchi pronti (vedi [Funzioni di scrittura](#funzioni-di-scrittura)).
- **Tavolozza Simboli & Snippet** (**Ctrl+K**): cerca e inserisci simboli e lettere, oltre a frammenti per circuiti.
- **Formule "stile Obsidian"**: le formule `$ ... $` possono essere mostrate già renderizzate dentro il codice (scheda *Obsidian Preview* delle Impostazioni).
- **Quadratini colore**: i colori (`fill`, `stroke`) sono mostrati come quadratini; **clic** apre la tavolozza colori, **Ctrl+clic** mostra il codice.
- **Anteprima immagini**: passando il mouse sul nome di un'immagine nel codice se ne vede una miniatura, con nome e dimensione.
- **Ripiegamento**: puoi comprimere le sezioni (`=`, `==`, `===`) con le frecce nel margine.
- **Trova e Sostituisci** (**Ctrl+F** / **Ctrl+H**): *Maiuscole/Minuscole*, risultato precedente (Shift+Invio) e successivo (Invio), **Sostituisci** e **Sostituisci tutti**; **Esc** chiude.
- **Incolla immagini**: **Ctrl+V** con un'immagine negli appunti la salva nel progetto e inserisce il codice (comportamento scelto in *Impostazioni → Immagini & Paste*). Con *Chiedi sempre* si apre una finestra con cartella di destinazione, nome del file, formato (*#figure*, *Centrata*, *Griglia 2 Col*), larghezza e anteprima del codice; **Invio** inserisce, **Esc** annulla.
- **Pulizia immagini orfane**: analizza i `.typ` del progetto, trova le immagini non usate e ti lascia spostarle in una cartella.
- **Pulisci duplicazioni nel file**: strumento di riparazione per i (rari) casi in cui, in collaborazione, un testo risulti raddoppiato; mostra le differenze prima di applicare.
- **Cronologia versioni** (pulsante nella barra in alto): confronto e ripristino stile Overleaf (vedi [GitHub](#github-backup-sincronizzazione-e-cronologia)).
- **Pacchetti Typst Universe**: esplora i pacchetti ufficiali e inserisci l'`#import` con un clic; c'è anche il pre-caricamento per l'uso offline.

---

## Funzioni di scrittura

Si attivano o disattivano da **Impostazioni → Scrittura** ("Scrittura più facile"). Sono attive di default, salvo dove indicato.

| Funzione | Cosa fa | Come usarla |
| :-- | :-- | :-- |
| **Liste automatiche** | Su una riga che inizia con `- `, `+ ` o `1. ` premere **Invio** continua la lista (con il numero successivo); Invio su un elemento vuoto esce dalla lista. | Scrivi un elemento di lista e premi Invio. |
| **Racchiudi la selezione** | Con del testo selezionato, digitare `*`, `_`, `$`, `` ` `` o `"` racchiude il testo invece di sostituirlo. | Seleziona e premi il carattere. |
| **Scorciatoie di formattazione** | **Ctrl+B** grassetto, **Ctrl+I** corsivo, **Ctrl+M** formula `$…$`, **Ctrl+Shift+K** link. Premute di nuovo tolgono la formattazione. | Seleziona il testo (o posiziona il cursore) e premi la scorciatoia. Con queste attive, il pannello laterale si apre con **Ctrl+Shift+B** (modificabile). |
| **Incolla intelligente** | Un indirizzo web incollato su del testo selezionato diventa `#link("…")[testo]`; il percorso di un'immagine del progetto diventa `#image("…")`. | Seleziona del testo e incolla un URL; oppure incolla un percorso di immagine. |
| **Riga corrente al centro** (*spenta di default*) | Mentre scrivi, la riga del cursore resta a metà dell'editor, come una macchina da scrivere. | Attiva l'opzione. |
| **Titoli colorati per livello** | Le righe `=`, `==`, `===`… hanno colori diversi per livello. | Automatico. |
| **Parentesi abbinate** | Evidenzia la parentesi che chiude (o apre) quella vicina al cursore; in rosso se manca. | Automatico. |
| **Ctrl+Shift+V: tabelle e testo** | Con una **tabella copiata** (da Excel, Word, pagina web, o testo separato da tabulazioni) crea una `#table` con le celle al loro posto. Con del **testo selezionato** e **altro testo copiato** negli appunti crea una `#grid` a due colonne con i due testi affiancati. Con un'**immagine** negli appunti crea una griglia testo + immagine (vedi sotto). | Copia, posizionati nell'editor e premi **Ctrl+Shift+V** (la combinazione si cambia in *Immagini & Paste*). |
| **Prima riga come intestazione** | Nelle tabelle incollate con Ctrl+Shift+V la prima riga diventa intestazione in grassetto. | Attiva o disattiva l'opzione. |
| **Scorciatoia del pannello laterale** | Combinazione per aprire e chiudere il pannello (predefinita **Ctrl+Shift+B**). | Scrivila nel campo. |
| **Modalità concentrazione** | Tasto per nascondere barre e pannelli (predefinito **F9**). | Scrivilo nel campo. |

Se non c'è niente di adatto negli appunti, Ctrl+Shift+V ti ricorda cosa copiare: *un'immagine o una tabella, oppure seleziona del testo e copia l'altro testo da affiancare*.

### Griglia testo + immagine (Smart Grid)

Se negli appunti c'è un'**immagine** e premi **Ctrl+Shift+V**:

- con **testo selezionato** nell'editor, l'immagine viene salvata nel progetto e il testo diventa una `#grid` a due colonne, testo e immagine affiancati; per qualche secondo compare un pulsante per **invertire l'ordine delle colonne** (Testo / Immagine);
- **senza selezione** si apre la finestra di inserimento in modalità *Griglia 2 Col*.

L'ordine predefinito delle colonne e la larghezza della colonna immagine si regolano in *Impostazioni → Immagini & Paste*.

### Slash snippet e snippet personalizzati

Con **Impostazioni → Plugin Editor** attivi gli *Slash Snippets Rapidi*: digita `/` (carattere di innesco modificabile) e scegli dal menu:

| Comando | Inserisce |
| :-- | :-- |
| `/grid` | Griglia a 2 colonne (testo a sinistra, immagine a destra) |
| `/table` | Tabella con intestazione |
| `/fig` | Figura con didascalia (`#figure`) |
| `/mat` | Matrice 2×2 |
| `/cases` | Sistema di equazioni (`cases`) |
| `/nota`, `/risultato`, `/ipotesi` | Riquadri `#nota[...]`, `#risultato[...]`, `#ipotesi[...]` (funzionano se nel tuo documento sono definiti i riquadri con quei nomi) |
| `/circ` | Schema circuitale `#zap.circuit` (richiede il pacchetto circuitale usato dallo snippet) |

Nella stessa scheda c'è l'**Editor Codice Strutturato Snippet** (in formato JSON): ogni snippet ha `shortcut`, `title`, `description` e `code`, con segnaposto `$1`, `$2`, `$3` che si scorrono con **Tab**. Pulsanti: **Salva Modifiche Snippet**, **Aggiungi Template Vuoto**, **Ripristina Predefiniti**; un indicatore ti dice quanti snippet sono validi o dov'è l'errore.

### Navigazione strutturale

Da **Impostazioni → Navigazione & Tabout**:

- **Chiusura automatica delimitatori**: chiude da sola le coppie `()`, `[]`, `{}`, `""` e `$$`, con sovrascrittura e cancellazione con Backspace.
- **Tabout Intelligente con Tab / Shift+Tab**: premendo **Tab** prima o dentro un delimitatore di chiusura si salta all'esterno, senza inserire rientri inutili.
- **Navigazione celle tabelle, matrici e griglie**: **Tab** e **Shift+Tab** dentro `#table`, `#grid` e `mat(...)` spostano tra celle e argomenti.

---

## Esportazione PDF e avanzata

### Esporta PDF

Dal pulsante **Esporta PDF** in alto, dal menu *File* o dalla palette comandi si apre la finestra **Esporta PDF**:

- **Pagine da esportare**
  - **Tutto il documento** (con il numero di pagine);
  - **Pagina corrente** (quella che stai guardando nell'anteprima);
  - **Intervallo di pagine**: per esempio `1-3, 5` (la finestra conferma quante pagine sono selezionate o se l'intervallo non è valido).
- **Solo un file**: compila da solo uno dei file del progetto, con il suo preambolo. Utile per esportare un singolo capitolo.
- **Nome del file** del PDF.
- **Cartella di destinazione**: clicca sul percorso per sceglierne un'altra. La finestra propone l'ultima cartella usata; altrimenti la **Cartella di esportazione** impostata in *Impostazioni → Backup & Diagnostica*; altrimenti la cartella del progetto.

A esportazione conclusa vedi *"PDF salvato · N pagine"* con i pulsanti **Apri PDF** e **Mostra nella cartella**.

Dalla Dashboard, **Esporta PDF rapido** esporta direttamente il progetto.

### Esportazione avanzata (PDF / SVG)

Da *File → Esporta Avanzato (PDF/SVG)…* scegli il formato (**PDF** per stampa e pubblicazione, **SVG** a pagine singole per web e slide) e, facoltativamente, un intervallo di pagine (per esempio `1-3, 5`; vuoto = tutto il documento). La finestra offre anche l'opzione **Auto-PDF in background**, che esporta il PDF in automatico dopo 12 secondi di inattività.

---

## Preambolo, file inclusi e importazione (Pandoc)

### Preambolo dei file inclusi

Se il tuo documento è diviso in capitoli con `#include`, ogni capitolo di solito ripete lo stesso preambolo (`#import`, `#let`, `#set`, `#show`…). Aprendo un file che contiene `#include`, il pannello **Preambolo dei file inclusi** (icona nella barra laterale, o comando nella palette) ti permette di cambiarlo **in tutti i capitoli in una volta**:

1. L'app analizza i file inclusi e mostra, per ciascuno, il preambolo trovato. **Rianalizza** aggiorna l'elenco.
2. In **File inclusi** spunti i capitoli da modificare; **Parti dal preambolo di** ti fa scegliere il punto di partenza (indica quello *più usato*).
3. Modifica il **Nuovo preambolo**. L'app avvisa se contiene qualcosa di diverso da `#import`, `#let`, `#set`, `#show` e commenti: il resto dei file non viene mai toccato.
4. **Applica a N file**, poi conferma. Prima di scrivere, l'app salva una **copia di sicurezza di ogni file** nella cartella `_recupero` del progetto, controlla che il corpo resti identico e rilegge il risultato. Se qualcosa non torna, non modifica niente.

Funziona anche nelle cartelle condivise: le modifiche passano dall'editor e si propagano agli altri.

### Nuovo capitolo

Nello stesso pannello, **Nuovo capitolo** crea un nuovo file `.typ` accanto al file principale (per esempio `Cap6_Sistemi_trifase`), con il preambolo mostrato nel pannello e un titolo ricavato dal nome, e aggiunge l'`#include` nel file principale subito dopo gli altri. Se il file esiste già o è già incluso, l'app lo segnala senza sovrascrivere niente.

### Importazione di documenti (Pandoc)

- Dalla Dashboard (**Inizia da un file → Importa documento Pandoc**) o da un progetto (*File → Importa Documento*, oppure *Importa con Pandoc…* su una cartella) puoi importare **Word (.docx)**, **LaTeX (.tex)**, **Markdown (.md)**, **HTML**, **OpenDocument (.odt)**, testo e file **Typst**.
- Per `.md`, `.tex`, `.txt` e `.typ` la conversione è integrata nell'app. Per i file **`.docx`** è consigliato installare **[Pandoc](https://pandoc.org/installing.html)**; se non viene trovato, l'app lo segnala con *"Pandoc non trovato: conversione nativa Typst attiva"*.
- Puoi scegliere un **preambolo** da applicare al file convertito dalla **Libreria Preamboli Typst**: *Standard A4*, *Tesi / libro*, *Articolo scientifico* (2 colonne), *Sotto-file incluso* (senza `#set page`, adatto ai capitoli) o *Nessun preambolo*. Puoi creare i tuoi preset (**Nuovo**, **Salva**, elimina) e impostarne uno come predefinito.
- *File → Applica Template Typst* applica un modello al documento corrente.

---

## Collaborazione P2P

LocalTypst permette a più persone di **scrivere insieme sulla stessa cartella in tempo reale**, con cursori e nomi visibili, senza un servizio cloud che conservi i tuoi documenti.

- I collaboratori si collegano **direttamente tra loro** (peer-to-peer). I file vivono sul computer di ciascuno: lavorare da soli, anche offline, è sempre possibile; al rientro online le modifiche si riallineano. Se qualcuno ha cambiato qualcosa mentre eri assente, all'apertura compare l'avviso **"È cambiato qualcosa nella cartella condivisa!"** con i file aggiornati: un clic su un file lo apre e **mostra cosa è cambiato**.
- La comunicazione è **cifrata da un estremo all'altro**: la chiave della stanza viene ricavata dall'invito (il codice che inizia con `LTYP-`), quindi chi non ha l'invito non può leggere il contenuto.
- Immagini e altri file non testuali vengono sincronizzati a parte, a blocchi e verificati con un controllo d'integrità.
- Per evitare testi duplicati, solo chi ha creato la condivisione porta nella stanza i suoi file iniziali; gli altri li ricevono.

### Cartelle condivise e Ambienti condivisi

Hai due modi di condividere:

- **Cartella condivisa singola**: una sola cartella, con il suo codice.
- **Ambiente condiviso**: un gruppo di cartelle. Tutte le cartelle che metti o crei dentro l'ambiente vengono condivise automaticamente con un **unico codice**. Nella Dashboard l'ambiente ha una sua sezione, con:
  - **Nuova cartella nell'Ambiente** e **Includi** (aggiunge una cartella esistente);
  - **Copertina** (immagine PNG, JPG, WEBP o GIF, massimo 4 MB) e rimozione della copertina;
  - **Copia codice di invito negli appunti**;
  - **GitHub** (sincronizzazione dell'ambiente, vedi la sezione dedicata);
  - eliminazione dell'ambiente (le cartelle locali **non** vengono cancellate);
  - indicatori *Host attivo* / *Membro* e chi è online ora.

### Impostare il server di segnalazione (una volta, da chi condivide)

> **L'app non contiene un server di segnalazione predefinito. Chi crea la condivisione imposta una volta l'indirizzo del proprio server in Impostazioni → P2P; l'invito generato contiene già l'indirizzo, quindi chi lo riceve non deve configurare nulla.**

Il **server di segnalazione** serve soltanto a far "incontrare" i computer all'inizio (scambio dei messaggi necessari a stabilire il collegamento diretto): non vede i tuoi documenti e non li conserva. Per condividere hai bisogno dell'indirizzo di un server di segnalazione compatibile (per esempio uno che gestisci tu o che ti ha fornito il tuo gruppo di lavoro).

1. Apri **Impostazioni → P2P & Profilo**.
2. Nel campo del server di segnalazione WebRTC incolla l'indirizzo del tuo server.
3. Da quel momento ogni invito che generi lo contiene già.

Chi **riceve** un invito non deve fare nessuna impostazione.

### Come condividere (creare l'invito)

**Una cartella singola**

1. Apri il progetto e clicca il pulsante **P2P** in alto (*Collaborazione P2P Real-Time*), oppure usa il comando *Collaborazione P2P* della palette.
2. In *Rendi questa cartella una Cartella Condivisa P2P* clicca **Attiva Condivisione**.
3. Compare il **codice di invito** (inizia con `LTYP-` e contiene anche l'indirizzo del tuo server di segnalazione): clicca **Copia** e invialo alla persona (messaggio, email…). Invialo solo a chi vuoi che partecipi: chi ha il codice può modificare la cartella.
4. La cartella è salvata permanentemente su entrambi i computer e resta disponibile anche quando l'altro è spento. Il pulsante **Metti in pausa sincronizzazione live** interrompe la connessione senza cancellare nulla.

**Un ambiente condiviso**

1. Nella Dashboard clicca il pulsante **+** accanto al tuo profilo (*Crea o Collega un Ambiente Condiviso P2P*).
2. Nella scheda **Crea Ambiente** scrivi il nome e, se vuoi, spunta le cartelle esistenti da condividere subito; poi **Crea Ambiente Condiviso**.
3. Nell'intestazione dell'ambiente usa **Copia codice di invito negli appunti** e invia il codice.

### Come entrare (incollare l'invito)

**Una cartella singola** (dal pulsante *Cartella Condivisa P2P* della Dashboard):

1. Incolla il codice di invito (inizia con `LTYP-`).
2. Facoltativamente scegli il nome della cartella sul tuo PC.
3. Clicca **Crea e Sincronizza Cartella**. La cartella viene creata sul tuo computer e compare nella Dashboard.

**Un ambiente**

1. Clicca **+** e scegli la scheda **Entra in Ambiente**.
2. Incolla il codice dell'ambiente e, se vuoi, dai un nome all'ambiente sul tuo PC.
3. Se l'ambiente è sincronizzato anche con un repository GitHub, nei campi *Chiave 2: Sincronizzazione GitHub* puoi inserire il token e l'indirizzo del repository (il token si può lasciare vuoto se l'hai già salvato).
4. **Collega Ambiente Condiviso**: le cartelle dell'ambiente compariranno sul tuo computer.

### Durante la collaborazione

- Nell'editor il pulsante in alto diventa **Host** o **Ospite** con il numero di persone connesse. Nella barra di stato leggi **P2P Online (N peer)** oppure **P2P Offline**.
- Se un collaboratore usa una versione dell'app incompatibile, compare un avviso con il pulsante **Verifica aggiornamenti**: tutti devono avere versioni compatibili.
- Se compaiono testi raddoppiati, usa **Pulisci Duplicati P2P** (menu *File*) o **Pulisci duplicazioni nel file** (palette comandi).

### Indicatore di qualità e test di connessione

Nella barra di stato, accanto a P2P, c'è un indicatore della qualità del collegamento:

| Indicatore | Significato |
| :-- | :-- |
| **Locale** | Nessuna collaborazione attiva. |
| **P2P Diretto NN ms** | Collegamento diretto tra i computer (il migliore). |
| **P2P Relay NN ms** | Il traffico passa da un server di inoltro (relay), perché un collegamento diretto non è possibile (per esempio reti aziendali restrittive): funziona, con più latenza. |
| Verifica in corso | L'app sta misurando. |

Cliccando sull'indicatore si apre **Diagnostica di Rete & Connettività P2P**, con due schede:

- **Test 6-Fasi**: verifica in sequenza (1) la raggiungibilità del server di segnalazione, (2) la connessione WebSocket, (3) i server STUN, (4) le credenziali TURN temporanee, (5) la raccolta dei percorsi di rete (ICE) e (6) latenza e jitter. Ogni passo mostra l'esito (successo, avviso, errore) e i millisecondi. **Riesegui Tutti i Test** ripete la prova.
- **Log Redatti**: registro recente in memoria, con token, chiavi ed email già oscurati. **Esporta Report Completo (.txt)** salva un report da allegare a una richiesta di aiuto.

Per attraversare router e firewall l'app usa automaticamente server **STUN** pubblici e, se il server di segnalazione li fornisce, credenziali **TURN** temporanee (relay): non devi configurare nulla.

---

## GitHub: backup, sincronizzazione e cronologia

GitHub è facoltativo: serve per avere un **backup versionato** delle cartelle e per condividerle con altre persone tramite un repository. Si apre dal pulsante **GitHub** in alto nell'editor (mostra `@tuo-utente` quando sei collegato), dal ramo nella barra di stato o dalla palette (*GitHub: backup e sincronizzazione*).

### Collegare il tuo account

La finestra ha le schede **Backup & Sync**, **Repository** e **Accesso GitHub**.

**Opzione consigliata: Personal Access Token (PAT)**

1. Su GitHub crea un token personale (*Settings → Developer settings → Personal access tokens*; il link è nella finestra) con il permesso **`repo`**.
2. Incollalo nel campo *Incolla GitHub PAT* (inizia con `ghp_…` o `github_pat_…`) e salva.
3. Il token viene custodito nel **portachiavi del sistema** (Windows Credential Manager su Windows; il servizio dei segreti del desktop su Linux): non resta in chiaro in file dell'app.

**Alternativa: accesso con codice dal browser (OAuth Device Flow)**: clicca **Avvia Device Flow**, copia il codice mostrato e confermalo nel browser. Richiede il *Client ID* di una OAuth App creata su GitHub con *Enable Device Flow* attivo.

Puoi salvare il token anche in **Impostazioni → Backup & Diagnostica → Account GitHub** (*Salva* / *Rimuovi*): è utile prima di entrare in una cartella condivisa con un repository, perché l'app verifica che il tuo account abbia il permesso di scrittura. Lì compaiono anche gli **inviti ai repository** da accettare (**Accetta**). **Esci da GitHub** rimuove il token dal portachiavi.

### Collegare un repository

Nella scheda **Repository**:

- **Crea Nuovo Repository su GitHub (via API)**: scrivi il nome, scegli se *Privato* (predefinito) e clicca **Crea & Collega**.
- **Collega da uno dei tuoi repository GitHub**: cerca nell'elenco e scegli.
- Oppure inserisci a mano l'indirizzo (`https://github.com/utente/repository.git`) e clicca **Imposta Remote**.

Un ambiente condiviso già collegato a un repository non può essere ricollegato a un altro, per evitare frammentazioni.

### Salvare e sincronizzare

Nella scheda **Backup & Sync**:

- **Messaggio di Commit / Backup** e pulsanti **Salva Commit Locale** e **Commit & Push su GitHub**.
- **Pull**: scarica le novità dal repository (bloccato mentre una stanza P2P è attiva: durante la collaborazione la sincronizzazione avviene dal vivo).
- **Auto-Backup Periodico su GitHub**: *Disattivato*, ogni 5, 10, 15 (consigliato) o 30 minuti. Se un backup non riesce, in alto compare **Backup Sospeso**.
- **Cronologia dei commit** con **Ripristina** per tornare a una versione precedente.

In collaborazione, il backup su GitHub è affidato a un solo computer alla volta (l'**Host**): viene scelto automaticamente tra chi ha un token valido, e se esce dalla stanza il ruolo passa al successivo. Se i collaboratori usano lo stesso account GitHub (per esempio PC fisso e portatile) l'accesso al repository è già completo.

### Invitare collaboratori su GitHub

Nel pannello **Invita Collaboratore su GitHub** scrivi il nome utente GitHub della persona e clicca **Invita come Collaboratore**. L'invitato vede l'invito su GitHub e nell'app (finestra GitHub, oppure *Impostazioni → Backup & Diagnostica → Account GitHub*) e lo accetta con **Accetta Invito** / **Accetta**. Serve che tu abbia i permessi per aggiungere collaboratori al repository.

### Cronologia versioni (stile Overleaf)

Il pulsante **Cronologia versioni** (barra in alto) mostra le versioni del documento:

- confronto tra due versioni con le differenze evidenziate e ricerca nella versione (**Ctrl+F**);
- **Snapshot** crea un'istantanea manuale;
- **Restore this version** ripristina il file corrente a quella versione;
- **ZIP** scarica un archivio del progetto;
- **Back to editor** torna a scrivere.

---

## Impostazioni

Si aprono dall'ingranaggio della Dashboard o dell'editor (o dalla palette: *Impostazioni*). I cambiamenti si salvano subito. In fondo, **Ripristina predefiniti** riporta tutto ai valori iniziali.

### Aspetto & Tema

| Opzione | Descrizione |
| :-- | :-- |
| Tema dell'applicazione | **Light**, **Dark** o **System** (segue il sistema). |
| Grandezza Cartelle nella Dashboard | Cursore 150–360 px, con scelte rapide *Piccole*, *Normali*, *Grandi*, *Giganti*. |
| Zoom Interfaccia Globale | 85%–130% (con scelte rapide 85, 100, 115, 130). |

### Obsidian Preview

| Opzione | Descrizione |
| :-- | :-- |
| Modalità formule | **1. Sempre visibili**: le formule fuori dal cursore sono sostituite dal loro rendering. **2. Tenendo premuto**: codice normale; tenendo premuto il tasto scelto tutte le formule diventano renderizzate. **3. Hover / Tasto**: codice sempre visibile, con popup sopra la singola formula. **4. Disattivata**. |
| Tasto rapido di attivazione | Ctrl (predefinito), Alt, Shift, Ctrl+Spazio, F2, oppure **Registra tasto…**. |
| Dimensione formule | Cursore 70%–180%. |
| Quadratini colore interattivi | Mostra i colori (`fill`/`stroke`) come quadratini: clic = tavolozza, Ctrl+clic = codice. |

### Navigazione & Tabout

*Chiusura automatica delimitatori*, *Tabout Intelligente con Tab / Shift+Tab*, *Navigazione celle tabelle, matrici e griglie* (vedi [Navigazione strutturale](#navigazione-strutturale)).

### Scrittura

*Liste automatiche*, *Racchiudi la selezione*, *Scorciatoie di formattazione*, *Incolla intelligente*, *Riga corrente al centro*, *Titoli colorati per livello*, *Parentesi abbinate*, *Ctrl+Shift+V: tabelle e testo*, *Prima riga come intestazione*, *Scorciatoia del pannello laterale*, *Modalità concentrazione* (vedi [Funzioni di scrittura](#funzioni-di-scrittura)).

### Plugin Editor

| Opzione | Descrizione |
| :-- | :-- |
| Slash Snippets Rapidi | Abilita il menu di snippet digitando `/`. |
| Carattere di Innesco | Il carattere che apre la lista (predefinito `/`). |
| Formatta codice Typst su salvataggio (Typstyle) | Allinea sintassi e indentazione a ogni salvataggio. |
| Editor Codice Strutturato Snippet | Modifica gli snippet in JSON (salva, aggiungi, ripristina). |

### Immagini & Paste

| Opzione | Descrizione |
| :-- | :-- |
| Cartella di destinazione immagini | Dove salvare le immagini incollate (predefinita `images`). |
| Comportamento standard Ctrl+V (con immagine negli appunti) | **Solo #image(...)** (inserimento immediato), **Centrata #align(...)**, **Figura con didascalia** (`#figure` con caption e label), **Chiedi sempre** (finestra di scelta a ogni incolla). |
| Scorciatoia Smart Grid | Predefinita **Ctrl+Shift+V**; alternative **Alt+V**, **Ctrl+Alt+G**, **Ctrl+G** o **Registra combinazione…**. |
| Disposizione colonne (#grid) | *Testo a sinistra + immagine a destra* oppure *Immagine a sinistra + testo a destra*. |
| Larghezza predefinita colonna immagine | 35%, 45% o 50%. |

### P2P & Profilo

| Opzione | Descrizione |
| :-- | :-- |
| Il tuo Nome Utente | Mostrato nei progetti e accanto al cursore in collaborazione. |
| Icona Profilo | Iniziale del nome, **icona rapida** (emoji), colore a scelta o **Carica foto**. |
| Avviso "Cosa è cambiato" al rientro | Mostra l'avviso quando un collaboratore ha cambiato file mentre eri assente. |
| Doppio click sull'anteprima salta al codice | Attiva o disattiva il salto dal doppio clic sull'anteprima. |
| Server di segnalazione WebRTC | L'indirizzo del tuo server di segnalazione, da impostare **una volta** se crei condivisioni (vedi [sopra](#impostare-il-server-di-segnalazione-una-volta-da-chi-condivide)). |

### Backup & Diagnostica

| Opzione | Descrizione |
| :-- | :-- |
| Typst Data Takeout | **Esporta Data Takeout (.zip)** salva un archivio dei tuoi progetti; **Importa Typst Takeout (.zip)…** importa l'archivio scaricato dal tuo account su typst.app (con *Applica preferenze e nome da User.json* importa anche nome e preferenze). |
| Account GitHub | Token (salva/rimuovi), account collegato e inviti da accettare. |
| Cartella di esportazione | Dove salvare i PDF (*Scegli…*; *Progetto* torna alla cartella del progetto). |
| Diagnostica prestazioni (Anti-freeze) | Rileva i blocchi dell'interfaccia e misura i tempi di Git, compilazione e comunicazione interna; utile per segnalare problemi di lentezza. Spenta di default. |

---

## Scorciatoie da tastiera

| Scorciatoia | Azione |
| :-- | :-- |
| **Ctrl+S** | Salva il file corrente |
| **Ctrl+F** / **Ctrl+H** | Trova e sostituisci nel file |
| **Invio** / **Shift+Invio** | Risultato successivo / precedente (nella barra di ricerca) |
| **Ctrl+Shift+F** | Cerca in tutto il progetto |
| **Ctrl+Shift+P** | Palette comandi |
| **Ctrl+K** | Tavolozza simboli e snippet |
| **Ctrl+Alt+D** | Trova definizione del simbolo |
| **Ctrl+B** / **Ctrl+I** | Grassetto / corsivo (con *Scorciatoie di formattazione* attive) |
| **Ctrl+M** | Formula `$…$` |
| **Ctrl+Shift+K** | Link |
| **Ctrl+Shift+B** | Mostra/nascondi il pannello laterale (modificabile; con le scorciatoie di formattazione disattivate è **Ctrl+B**) |
| **Ctrl+Shift+V** | Incolla come tabella, griglia di testi o griglia testo + immagine (modificabile) |
| **Ctrl+V** | Incolla (con un'immagine negli appunti: la salva nel progetto) |
| **Tab** / **Shift+Tab** | Esci da un delimitatore / vai alla cella o argomento successivo-precedente; **Tab** accetta anche il suggerimento nell'autocompletamento |
| **Esc** | Chiude la barra di ricerca, il tutto schermo, le modalità selezione/copia dall'anteprima |
| **F9** | Modalità concentrazione (modificabile) |
| **F11** | Documento a tutto schermo |
| **Ctrl+Shift+E** | In modalità compatta: passa da Codice ad Anteprima |
| **Ctrl + rotellina** (sull'anteprima) | Zoom dell'anteprima |
| **Alt + trascina** (sull'anteprima) | Copia il codice della zona selezionata |
| **Doppio clic** (sull'anteprima) | Salta al punto corrispondente nel codice |
| **Tasto formule** (Ctrl predefinito) | Mostra le formule renderizzate (modalità *Tenendo premuto* e *Hover / Tasto*) |
| **Canc** | Elimina gli elementi selezionati nell'albero dei file |

---

## Domande frequenti e risoluzione problemi

**Windows mostra "Windows ha protetto il PC".**
L'app non è firmata con un certificato a pagamento. Clicca **Ulteriori informazioni → Esegui comunque**.

**L'app non parte (versione portatile) o la finestra resta vuota.**
La versione portatile richiede il componente WebView2 di Microsoft. Installa `LocalTypst_Setup.exe`, che lo installa se manca, oppure scarica il *WebView2 Runtime* dal sito Microsoft.

**Su Linux l'interfaccia si blocca o si chiude all'avvio.**
Avvia con `WEBKIT_DISABLE_DMABUF_RENDERER=1 localtypst` (vedi la [nota per Linux](#nota-per-linux-interfaccia-che-si-blocca-o-va-in-crash)).

**L'AppImage non si avvia.**
Verifica di averla resa eseguibile (`chmod +x`). Su alcune distribuzioni può servire il supporto FUSE.

**L'aggiornamento non parte / "esci dalla stanza prima di riavviare".**
Gli aggiornamenti sono bloccati mentre è attiva una stanza P2P o è in corso un push Git: chiudi la collaborazione (**Metti in pausa sincronizzazione live**), attendi il termine del salvataggio e riprova.

**Su Linux l'aggiornamento chiede una password.**
È normale per le installazioni `.rpm` / `.deb`: serve l'autorizzazione di sistema per installare il pacchetto.

**L'anteprima non si aggiorna o mostra un errore.**
Apri il pannello **Warnings & Errors**: indica file e riga. L'`#import` di un pacchetto `@preview/...` richiede la connessione la prima volta (poi resta in cache).

**Il doppio clic sull'anteprima non mi porta al codice.**
Controlla che l'opzione *Doppio click sull'anteprima salta al codice* (P2P & Profilo) sia attiva. Per alcuni disegni generati da pacchetti grafici il salto porta alla chiamata che li produce.

**Ctrl+B non apre il pannello laterale.**
Con le *Scorciatoie di formattazione* attive Ctrl+B è il grassetto: il pannello si apre con **Ctrl+Shift+B** (modificabile in *Impostazioni → Scrittura*).

**Non riesco a collegarmi a un collaboratore.**
1. Controlla che l'invito sia stato copiato per intero: è un codice lungo che inizia con `LTYP-` e contiene una `@`. Se è corto (senza `@`) è un invito di una versione vecchia: chi condivide deve aggiornare l'app, impostare il server in *Impostazioni → P2P & Profilo* e copiarlo di nuovo.
2. Clicca sull'indicatore di qualità nella barra di stato e lancia il **Test 6-Fasi**: ti dice quale passo fallisce.
3. Verifica che anche l'altra persona usi una versione compatibile (altrimenti compare un avviso).
4. Se sei tu a creare la condivisione, controlla in *Impostazioni → P2P & Profilo* di aver impostato il tuo server di segnalazione.
5. Su reti molto restrittive il collegamento può passare da un relay (indicatore **P2P Relay**) o non essere possibile.

**Vedo testo raddoppiato in un file condiviso.**
Usa *File → Pulisci Duplicati P2P* (o la palette): mostra le differenze e ti lascia confermare.

**Ho perso una modifica.**
Controlla la **Cronologia versioni**; se hai applicato il preambolo a più file, le copie originali sono nella cartella `_recupero` del progetto.

**GitHub rifiuta il token.**
Verifica che il token abbia il permesso `repo` e che non sia scaduto; in *Impostazioni → Backup & Diagnostica → Account GitHub* puoi sostituirlo.

**Come disinstallo?**
Windows: *Impostazioni → App*. Linux: rimuovi il pacchetto con il gestore della tua distribuzione (`dnf` o `apt`), oppure elimina il file AppImage. I tuoi documenti in `Documenti/LocalTypst` non vengono toccati.

**Come segnalo un problema?**
Scrivi a chi ti ha dato l'app, indicando la versione (la trovi nelle note della release installata) e, per i problemi di collaborazione, allegando il report esportato dalla **Diagnostica di Rete**.

---

## Privacy

- **I tuoi documenti restano sul tuo computer**, in `Documenti/LocalTypst/projects`. LocalTypst non li carica su alcun servizio proprio.
- **Collaborazione P2P:** i contenuti viaggiano direttamente tra i computer dei partecipanti e sono **cifrati end-to-end** con una chiave derivata dal codice di invito. Il **server di segnalazione** vede solo i messaggi necessari a mettere in contatto i computer (identificativo della stanza e dati di connessione): **non riceve né conserva i contenuti dei documenti**, che per lui sono illeggibili.
- **GitHub:** se usi la sincronizzazione, i file vanno al repository che scegli tu, con le regole di privacy di GitHub (usa repository *privati* per i documenti riservati).
- **Token e credenziali:** il token GitHub è salvato nel **portachiavi di sistema** (Windows Credential Manager; su Linux il servizio dei segreti del desktop), non in chiaro. Nei log di diagnostica token, chiavi ed email vengono oscurati prima di essere mostrati o esportati.
- **Aggiornamenti:** l'app legge il file `latest.json` dell'ultima release di questo repository per sapere se esiste una nuova versione, e verifica la firma del pacchetto prima di installarlo.
- **Pacchetti Typst:** quando usi un `@preview/...`, l'app scarica il pacchetto dal registro pubblico di Typst.
- **Diagnostica prestazioni:** disattivata di default; misura i tempi in locale.
