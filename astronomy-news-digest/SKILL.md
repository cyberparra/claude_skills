---
name: astronomy-youtube-digest
description: >
  Usa questa skill quando l'utente vuole aggiornarsi sulle ultime notizie di astronomia
  e spazio, oppure chiede "cosa c'è di nuovo in astronomia", "aggiorna il mio Google Doc
  di astronomia", "digest astronomia", "ultime notizie spazio", o simili. La skill
  recupera le notizie recenti da una lista di siti autorevoli, crea un riassunto tematico
  con le URL e lo pubblica su un Google Doc tramite Google Drive. Triggera anche se
  l'utente chiede semplicemente "aggiornami" in contesto astronomia/spazio.
---

# Astronomy News Digest → Google Doc

Questa skill monitora una lista di siti web di astronomia e pubblica un digest tematico su Google Doc.

## Siti monitorati
- **ANSA Spazio**: https://www.ansa.it/canale_scienza_tecnica/notizie/spazio_astronomia/index.shtml
- **Sky at Night Magazine**: https://www.skyatnightmagazine.com/
- **BBC Science**: https://www.bbc.com/news/science_and_environment
- **The Guardian Science**: https://www.theguardian.com/science
- **Space.com**: https://www.space.com/
- **Universe Today**: https://www.universetoday.com/
- **NASA**: https://www.nasa.gov/
- **ESA**: https://www.esa.int/
- **ASI**: https://www.asi.it/
- **CNSA**: https://www.cnsa.gov.cn/english/n6465652/n6465653/index.html

---

## Workflow completo

### Step 1 — Recupera le notizie recenti

Usa `web_fetch` sui siti della lista per raccogliere i titoli delle notizie più recenti.
Dai priorità ai siti che rispondono più velocemente; se un sito restituisce errore, saltalo e continua.

Fetch paralleli consigliati (in ordine di priorità):
1. https://www.space.com/
2. https://www.universetoday.com/
3. https://www.nasa.gov/news-releases/
4. https://www.esa.int/Newsroom
5. https://www.ansa.it/canale_scienza_tecnica/notizie/spazio_astronomia/index.shtml
6. https://www.skyatnightmagazine.com/space-science
7. https://www.bbc.com/news/science_and_environment
8. https://www.theguardian.com/science
9. https://www.asi.it/
10. https://www.cnsa.gov.cn/english/n6465652/n6465653/index.html

Raccogli un massimo di **10 articoli in totale**, selezionando i più recenti tra tutte le fonti.
Se una fonte ha più articoli recenti, prendi solo il più nuovo. Dai priorità alla data di pubblicazione.

Per ogni notizia raccolta annota:
- Titolo
- URL completa dell'articolo
- Data di pubblicazione (se disponibile)
- Fonte (nome del sito)
- Breve tema/argomento

### Step 2 — Costruisci il riassunto tematico

Raggruppa le notizie per **tema**, non per fonte. Esempi di temi:
- 🚀 Missioni spaziali & lanci
- 🌌 Scoperte astronomiche
- 🔭 Telescopi & strumenti
- 🛸 Agenzie spaziali & politica
- 🌍 Terra, clima & sistema solare
- 🔬 Scienza & ricerca
- 🌙 Luna & esplorazione umana
- 🪐 Pianeti & esopianeti

Per ogni tema:
- Scrivi 2-4 frasi di sintesi delle notizie principali
- Elenca gli articoli con titolo, fonte e URL

### Step 3 — Crea il Google Doc via Google Drive MCP

Usa il tool **Google Drive MCP** (già connesso) con `create_file`.

#### Struttura del documento

```
🌌 DIGEST ASTRONOMIA & SPAZIO — DD/MM/YYYY
Fonti: ANSA · Sky at Night · BBC · Guardian · Space.com · Universe Today · NASA · ESA · ASI · CNSA
═══════════════════════════════════════════


🚀 MISSIONI SPAZIALI & LANCI
──────────────────────────────
[Riassunto 2-4 frasi]

▸ Titolo articolo (Fonte, data)
  URL

▸ Titolo articolo (Fonte, data)
  URL


🌌 SCOPERTE ASTRONOMICHE
─────────────────────────
[Riassunto 2-4 frasi]

▸ Titolo articolo (Fonte, data)
  URL

[... altri temi ...]


═══════════════════════════════════════════
📅 Aggiornato il DD/MM/YYYY
Fonti monitorate: ANSA · Sky at Night · BBC · Guardian · Space.com · Universe Today · NASA · ESA · ASI · CNSA
```

#### Parametri create_file
- **title**: `🌌 Digest Astronomia — DD/MM/YYYY`
- **contentMimeType**: `text/plain` (Drive lo converte automaticamente in Google Doc)
- **textContent**: il testo del digest formattato come sopra

### Step 4 — Output in chat

Dopo aver creato il Google Doc, mostra in chat:

```
✅ Digest pubblicato su Google Doc!

📰 Trovate X notizie da Y fonti
🗂️ Raggruppate in Z temi
🔗 Apri il documento: [link]

--- Anteprima ---
[Mostra i titoli principali per tema]
```

---

## Gestione errori

- **Sito non raggiungibile**: salta e continua con gli altri; segnala in fondo al digest quali fonti non erano disponibili
- **Nessuna notizia trovata**: prova con `web_search` usando query come `site:space.com astronomia 2026` o `NASA news [mese corrente]`
- **Google Drive MCP non disponibile**: avvisa l'utente che deve abilitare il connettore Google Drive nelle impostazioni di Claude
