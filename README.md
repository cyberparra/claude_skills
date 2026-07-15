# 🤖 Claude Skills

Una raccolta di skill per [Claude](https://claude.ai) pronte da installare.

Le skill estendono le capacità di Claude permettendogli di eseguire task specifici in modo automatico — basta scrivere una frase in chat e Claude sa cosa fare.

---

## 📦 Skill disponibili

| Skill | Descrizione | Output |
|-------|-------------|--------|
| [🌌 Astronomy News Digest](./astronomy-news-digest/) | Raccoglie le ultime notizie di astronomia e spazio da 10 fonti autorevoli | Google Doc |
| [🔎 Five-Lens Text Analysis](./five-lens-text-analysis/) | Analizza un testo (link o documento) da 5 angolazioni indipendenti: contenuto evidente, non detto, interessi nascosti, controcampo, fake detector | File Markdown |

*Altre skill in arrivo…*

---

## ⚡ Come installare una skill

Il modo più semplice è chiedere direttamente a Claude. Apri una chat su [claude.ai](https://claude.ai) e scrivi:

```
Installa questa skill dal repository GitHub:
https://github.com/cyberparra/claude-skills/tree/main/[nome-skill]

Il file si chiama [nome-skill].skill
```

In alternativa, entra nella cartella della skill che ti interessa e segui le istruzioni nel suo `README.md`.

---

## 📋 Requisiti generali

- Un account **Claude.ai** (piano Free, Pro o Team)
- I connettori richiesti da ciascuna skill (indicati nel README di ogni skill)

---

## 🤝 Contributi

Hai creato una skill e vuoi condividerla? Apri una **Pull Request** con la tua cartella seguendo questa struttura:

```
nome-skill/
├── README.md           # Descrizione e istruzioni di installazione
├── nome-skill.skill    # File della skill da installare
└── SKILL.md            # Codice sorgente leggibile
```

---

## 📜 Licenza

MIT — libero di usare, modificare e condividere.
