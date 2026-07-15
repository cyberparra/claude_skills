# 🌌 Astronomy News Digest — Claude Skill

Una skill per [Claude](https://claude.ai) che raccoglie automaticamente le ultime notizie di astronomia e spazio da 10 fonti autorevoli e le pubblica in un **Google Doc** tematico, pronto da leggere.

## ✨ Cosa fa

Quando scrivi ad esempio **"aggiornami sull'astronomia"** o **"digest astronomia"**, Claude:

1. **Recupera** i 10 articoli più recenti da una lista di siti selezionati
2. **Raggruppa** le notizie per tema (missioni, scoperte, agenzie, pianeti…)
3. **Scrive un riassunto** tematico con link agli articoli originali
4. **Pubblica tutto su Google Doc** e ti manda il link direttamente in chat

### Fonti monitorate

| Fonte | URL |
|-------|-----|
| ANSA Spazio | https://www.ansa.it/canale_scienza_tecnica/notizie/spazio_astronomia/ |
| Sky at Night Magazine | https://www.skyatnightmagazine.com/ |
| BBC Science | https://www.bbc.com/news/science_and_environment |
| The Guardian Science | https://www.theguardian.com/science |
| Space.com | https://www.space.com/ |
| Universe Today | https://www.universetoday.com/ |
| NASA | https://www.nasa.gov/ |
| ESA | https://www.esa.int/ |
| ASI | https://www.asi.it/ |
| CNSA | https://www.cnsa.gov.cn/english/n6465652/n6465653/index.html |

---

## 📋 Requisiti

- Un account **Claude.ai** (piano Free, Pro o Team)
- Il connettore **Google Drive** abilitato in Claude (gratuito, basta collegare il proprio account Google)

---

## 🚀 Installazione

### ⚡ Metodo 1 — Chiedi direttamente a Claude (più semplice)

Apri una chat su [claude.ai](https://claude.ai) e incolla questo messaggio:

```
Installa questa skill dal repository GitHub:
https://github.com/cyberparra/claude-skills/blob/main/astronomy-news-digest/astronomy-news-digest.skill

Il file si chiama astronomy-news-digest.skill
```

Claude scaricherà e installerà la skill al posto tuo. Poi segui solo il passo **Collega Google Drive** qui sotto.

---

### 🗂️ Metodo 2 — Installazione manuale

Se preferisci farlo a mano:

**1. Scarica il file della skill**

Scarica il file `astronomy-news-digest.skill` da questo repository (clicca sul file → **Download raw file**).

**2. Apri le impostazioni di Claude**

Vai su [claude.ai](https://claude.ai) → clicca sulla tua foto profilo in alto a destra → **Settings**.

**3. Installa la skill**

Nella sezione **Skills**, clicca su **Add skill** e carica il file `.skill` scaricato.

> Se non vedi la sezione Skills, assicurati di avere un piano Pro o Team attivo.

---

### 🔗 Collega Google Drive (obbligatorio per entrambi i metodi)

Vai su **Settings → Connectors** e collega il tuo account Google Drive. Serve solo la prima volta.

### ✅ Prova!

Apri una nuova chat con Claude e scrivi:

```
aggiornami sull'astronomia
```

Claude recupererà le notizie più recenti e creerà un Google Doc nel tuo Drive. 🎉

---

## 💬 Frasi che attivano la skill

La skill si attiva automaticamente quando scrivi qualcosa come:

- `aggiornami sull'astronomia`
- `cosa c'è di nuovo nello spazio?`
- `digest astronomia`
- `ultime notizie spazio`
- `crea il digest di astronomia`

---

## 🛠️ Personalizzazione

Puoi modificare la skill aprendo il file `SKILL.md` con un editor di testo. Le cose più comuni da cambiare:

- **Aggiungere o rimuovere fonti** — modifica la sezione "Siti monitorati"
- **Cambiare il numero di articoli** — cerca "10 articoli" e modifica il numero
- **Cambiare la lingua del digest** — aggiungi un'istruzione nella sezione Step 2

Dopo aver modificato il file, ricaricalo nelle impostazioni di Claude seguendo gli stessi passi dell'installazione.

---

## 📄 Struttura del repository

```
astronomy-news-digest/
├── README.md                      # Questo file
├── astronomy-news-digest.skill    # File della skill da installare
└── SKILL.md                       # Codice sorgente della skill (leggibile)
```

---

## 🤝 Contributi

Se vuoi aggiungere nuove fonti, migliorare il formato del digest o tradurre la skill in altre lingue, apri una **Pull Request** o una **Issue** — ogni contributo è benvenuto!

---

## 📜 Licenza

MIT — libero di usare, modificare e condividere.
