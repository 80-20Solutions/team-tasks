# 🎯 80/20 Solutions - Team Tasks

Repository di coordinamento per il team 80/20 Solutions.

## 👥 Team
- **Davide** (@dadecresce) - Founder, decisioni strategiche
- **Ciccio** (@CiccioBot) - DevOps, infra VPS, automazioni
- **Claudio** (@ClaudeDev) - Senior dev, coding tasks

## 📋 Workflow

### 1. Creare una Issue
- Usa i **template** disponibili
- Aggiungi **labels** appropriate
- Tagga chi deve lavorarci (`@CiccioBot` o `@ClaudeDev`)

### 2. Lavorare sul Task
- Commenta quando inizi: "In corso 🚧"
- Aggiorna con progressi
- Committa con `Refs #N` per collegare commit all'issue

### 3. Completare
- PR con `Closes #N` per auto-chiusura
- Oppure commenta "Completato ✅" se non serve PR

## 🏷️ Labels

### Per Tipo
- `🔧 infra` - DevOps, VPS, database (→ Ciccio)
- `💻 coding` - Sviluppo app, feature (→ Claudio)
- `🎨 design` - UI/UX, assets
- `🐛 bug` - Fix urgenti
- `📝 docs` - Documentazione
- `🚀 deploy` - Release, pubblicazione
- `❓ question` - Discussioni, decisioni
- `✨ enhancement` - Miglioramenti

### Per Priorità
- `priority:high` - Urgente, fare subito
- `priority:medium` - Importante, prossimi giorni
- `priority:low` - Backlog, quando c'è tempo

### Per Progetto
- `project:maestro` - Maestro Energy Management
- `project:beachref` - BeachRef Arbitri
- `project:finn` - Finn Expense Tracker
- `project:stageconnect` - StageConnect Push-to-Talk
- `project:8020site` - Sito 8020solutions.org
- `project:arbitri-dash` - Dashboard Arbitri Beach

## 🔔 Notifiche

Le issue vengono notificate automaticamente su Telegram (gruppo **8020dev**) quando:
- ✅ Nuova issue creata
- 📌 Issue assegnata
- ✅ Issue chiusa

## 🚀 Quick Start

### Aprire una Issue
```
Titolo: [progetto] Breve descrizione
Body: Usa il template, compila le sezioni
Labels: Aggiungi tipo + priorità + progetto
```

### Collegare Commit a Issue
```bash
git commit -m "feat: add feature X

Refs #42"  # Collega commit a issue #42
```

### Auto-chiudere Issue da PR
```markdown
Closes #42  # Nella descrizione PR
```

## 📚 Progetti

- [Maestro](https://github.com/ecologicaleaving/maestro) - Energy management IoT
- [BeachRef](https://github.com/ecologicaleaving/BeachRef) - App arbitri beach volley
- [Finn](https://github.com/ecologicaleaving/finn) - Gestione spese familiari
- [StageConnect](https://github.com/ecologicaleaving/StageConnect) - Push-to-talk WiFi
- [Dashboard Arbitri](https://github.com/80-20Solutions/arbitri-beach-dashboard) - Dashboard web arbitri

---

**80/20 Solutions** - AI-augmented development studio 🤖✨
