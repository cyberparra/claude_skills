# 🔎 Five-Lens Text Analysis

Analizza un testo (da link web o da documento allegato) attraverso **cinque angolazioni indipendenti**, producendo un report Markdown finale con una sintesi integrata.

## Cosa fa

Data un URL, un documento allegato (PDF, DOCX, TXT, MD...) o un testo incollato in chat, Claude applica cinque letture distinte e indipendenti tra loro:

1. **Contenuto evidente** — tesi esplicita e struttura argomentativa
2. **Il non detto** — assunzioni date per scontate, buchi logici, domande non affrontate
3. **Interessi e concetti nascosti** — chi trae vantaggio dalla tesi, posizionamento dell'autore
4. **Controcampo** — le migliori controargomentazioni possibili
5. **Verifica fattuale / Fake detector** — controllo con ricerca web di citazioni, statistiche e affermazioni verificabili, classificate come confermate / non verificabili / imprecise / false / citazione errata

Le quattro lenti "interpretative" (1-4) vengono scritte come compartimenti stagni, per non farsi influenzare a vicenda; la Lente 5 è l'unica che usa attivamente la ricerca web. Al termine, una sintesi mette in dialogo i risultati delle cinque analisi.

## Output

Un file Markdown scaricabile con 6 sezioni (le 5 lenti + sintesi finale).

## Come usarla

Basta chiedere a Claude di analizzare un testo, ad esempio:

```
Analizza a fondo questo articolo: https://esempio.com/articolo
Analizza questo documento e dimmi cosa non dice / chi ci guadagna / se contiene fake news
```

## Requisiti

- Nessun connettore richiesto
- Serve accesso a ricerca web (`web_search`/`web_fetch`) per la Lente 5

## Installazione

```
Installa questa skill dal repository GitHub:
https://github.com/cyberparra/claude-skills/tree/main/five-lens-text-analysis

Il file si chiama five-lens-text-analysis.skill
```
