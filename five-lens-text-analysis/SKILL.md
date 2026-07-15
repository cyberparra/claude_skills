---
name: five-lens-text-analysis
description: Analizza un testo (da link web o da documento allegato) attraverso cinque angolazioni indipendenti - contenuto evidente, non detto/assunzioni nascoste, interessi/concetti nascosti dietro la tesi, controcampo/controargomentazioni, e verifica fattuale/fake detector - producendo un report Markdown finale con una sintesi integrata. Usa SEMPRE questa skill quando l'utente chiede di "analizzare a fondo" un articolo, post, saggio o documento, o menziona esplicitamente cose come "il non detto", "cosa c'è dietro", "gli interessi nascosti", "il controcampo", "leggere tra le righe", "cosa non dice l'autore", "verifica se è vero/falso", "fact-check", "contiene fake news", o chiede un'analisi critica/multi-prospettica di un testo. Triggera anche per richieste generiche tipo "analizza questo testo/link/pdf/doc con più punti di vista" o "fammi un'analisi critica di questo articolo" o "verifica se questo testo dice il vero".
---

# Five-Lens Text Analysis

Skill per produrre un'analisi critica multi-prospettica di un testo, applicando cinque
angolazioni di lettura distinte e indipendenti, seguite da una sintesi che le mette in dialogo.

## Workflow

### 1. Ottenere il testo

- **Se l'utente fornisce un link**: usa `web_fetch` per recuperare il contenuto della pagina.
  Se il link punta a un PDF o altro formato non testuale, gestiscilo di conseguenza.
- **Se l'utente allega un documento** (docx, pdf, txt, md...): leggi il file dal percorso in
  `/mnt/user-data/uploads/`. Consulta la skill `file-reading` o `pdf-reading` se il contenuto
  non è già visibile in contesto.
- **Se l'utente incolla il testo direttamente in chat**: usa quello, senza fetch.

Non procedere all'analisi finché non hai il testo completo davanti. Se il testo è molto lungo
(es. un intero libro), chiedi all'utente se vuole l'analisi sull'intero testo o su una sezione
specifica, invece di troncare silenziosamente.

### 2. Le cinque analisi indipendenti

Esegui le cinque analisi **in questo ordine, ma trattandole come compartimenti stagni**: quando
scrivi l'analisi N, non lasciarti influenzare da quello che hai già scritto per le analisi
precedenti. Ogni lente deve restare "pulita" e non anticipare le conclusioni delle altre — le
sovrapposizioni verranno gestite solo nella sintesi finale (punto 3).

Per ciascuna lente, produci un testo di 150-350 parole circa (più lungo se il testo sorgente è
corposo e complesso, più corto se è breve). Scrivi in prosa scorrevole, non elenchi puntati
generici — è ammesso l'uso di punti elenco solo per raccogliere esempi concreti a supporto di
un'affermazione.

**Lente 1 — Contenuto evidente**
Cosa dice esplicitamente il testo. Qual è la tesi centrale, come è strutturata l'argomentazione,
quali sono i passaggi logici dichiarati dall'autore. Questa è una lettura "alla lettera": niente
interpretazione, solo ricostruzione fedele di ciò che è scritto e di come è organizzato.

**Lente 2 — Il non detto**
Cosa il testo dà per scontato senza argomentarlo. Quali domande ovvie un lettore critico si
aspetterebbe fossero affrontate e non lo sono. Dove ci sono salti logici, generalizzazioni non
supportate, premesse implicite che se rese esplicite indebolirebbero l'argomentazione. Non
inventare intenzioni malevole: distingui tra "omissione probabilmente innocente" e "omissione che
sembra funzionale alla tesi".

**Lente 3 — Interessi e concetti nascosti**
Chi trae vantaggio se il lettore accetta questa tesi? Qual è la posizione (professionale,
economica, ideologica) dell'autore rispetto all'argomento, per quanto è verificabile o inferibile
dal testo stesso o da informazioni pubblicamente note su chi scrive? Ci sono concetti che vengono
usati in modo strategico (framing, terminologia che orienta il giudizio) più che descrittivo?
Qui è importante restare basati sui fatti: se non ci sono elementi per inferire un interesse
specifico, dillo esplicitamente invece di forzare un'interpretazione.

**Lente 4 — Controcampo**
Qual è la migliore versione possibile della tesi opposta, o delle principali obiezioni? Non un
"avvocato del diavolo" pretestuoso, ma le controargomentazioni più solide che un interlocutore
informato e in buona fede solleverebbe. Questa lente è puramente argomentativa/di ragionamento:
non fare verifiche fattuali qui, quelle sono nella Lente 5.

**Lente 5 — Verifica fattuale / Fake detector**
Questa è l'unica lente che usa attivamente `web_search` (e `web_fetch` se serve controllare una
fonte citata). Obiettivo: verificare se il testo contiene affermazioni false, fuorvianti,
statistiche inventate o distorte, citazioni attribuite scorrettamente, o fatti che risultano
smentiti da fonti affidabili.

Procedi così:
1. Elenca le affermazioni fattuali verificabili presenti nel testo (numeri, statistiche, eventi,
   citazioni attribuite a persone reali, nomi/date/fatti storici, claim scientifici).
2. Per ciascuna affermazione rilevante (non serve verificare ogni singolo dettaglio, concentrati
   su quelle che sono centrali per l'argomentazione o che sembrano sospette/troppo nette), fai una
   ricerca web mirata per controllarne l'accuratezza.
3. Classifica ogni affermazione verificata in una di queste categorie: **Confermata** (riscontro
   in fonti affidabili), **Non verificabile** (nessuna fonte la conferma né la smentisce, es.
   opinioni o previsioni), **Impreciso/fuorviante** (contiene un nucleo di verità ma è presentato
   in modo distorto o senza contesto), **Falso** (contraddetto da fonti affidabili), **Citazione
   errata/inventata** (la frase attribuita a una persona non risulta essere sua, o è alterata).
4. Se il testo è opinione/analisi personale (come nel caso di un saggio argomentativo) più che
   un pezzo di cronaca, dillo esplicitamente: in questi casi il fake-detection si concentra sui
   dati e le citazioni puntuali usate a supporto della tesi, non sulla tesi stessa (le opinioni
   non sono "vere o false").
5. Riporta i risultati in una tabella o elenco chiaro, con una riga per ogni affermazione
   controllata, l'esito, e la fonte usata per la verifica.

Se il testo non contiene alcuna affermazione fattuale verificabile (es. è puramente
argomentativo/valutativo), scrivilo esplicitamente in questa sezione invece di forzare una
verifica dove non c'è nulla da verificare.

### 3. Sintesi finale

Dopo le quattro lenti, scrivi una sintesi (200-400 parole) che:
- individua le connessioni tra le quattro analisi (es. "il non detto della lente 2 rafforza
  l'interesse individuato nella lente 3");
- offre una valutazione equilibrata di quanto la tesi regga nel complesso;
- NON impone un verdetto definitivo se il tema è genuinamente controverso — presenta invece cosa
  serve per decidere (dati mancanti, verifiche possibili, punti su cui ragionevolmente si può
  dissentire).

### 4. Output

Genera un file Markdown con questa struttura, e salvalo in `/mnt/user-data/outputs/`:

```markdown
# Analisi a Quattro Lenti: [Titolo del testo]

**Fonte:** [link o nome file]
**Data analisi:** [data odierna]

## 1. Contenuto evidente
[...]

## 2. Il non detto
[...]

## 3. Interessi e concetti nascosti
[...]

## 4. Controcampo
[...]

## 5. Verifica fattuale / Fake detector
[...]

## Sintesi
[...]
```

Usa `present_files` per condividere il file con l'utente al termine. Non limitarti a mostrare il
contenuto solo in chat: il valore di questa skill è nel documento consultabile e salvabile.

## Note

- Se il testo è dichiaratamente satirico, narrativo o poetico (non argomentativo), avverti
  l'utente che le lenti 2-4 avranno meno presa e adattale di conseguenza (es. "non detto" diventa
  più utile come "sottotesto", "interessi nascosti" come "posizionamento dell'autore/narratore").
  La Lente 5 in questi casi si limita a controllare eventuali riferimenti a fatti reali inseriti
  nella narrazione (es. eventi storici citati), se presenti.
- Non etichettare mai un intero testo come "fake" o "disinformazione" sulla sola base della Lente
  5: riporta i risultati affermazione per affermazione, lasciando che sia il lettore a farsi un
  giudizio complessivo. Evita toni sensazionalistici nel presentare eventuali falsità trovate.
- Mantieni un tono analitico e onesto, non cinico: l'obiettivo è illuminare, non screditare
  sistematicamente ogni testo che viene analizzato.
- Rispetta sempre i vincoli di copyright: nessuna citazione diretta oltre le 15 parole, parafrasi
  del contenuto sorgente, non riprodurre l'articolo per intero.
