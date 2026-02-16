# 🚀 Quick Start - Team Tasks

Guida rapida per iniziare con il workflow issues di 80/20 Solutions.

---

## 🎯 Per Davide (Project Manager)

### **Aprire una Issue**

1. Vai su https://github.com/80-20Solutions/team-tasks/issues
2. Clicca **"New Issue"**
3. Scegli template:
   - **🚀 Feature / Task** - Nuova funzionalità o task
   - **🐛 Bug Report** - Problema da fixare
   - **❓ Question / Decision** - Discussione o decisione

4. Compila form (titolo, descrizione, labels)
5. Clicca **"Submit new issue"**

### **Notifica Automatica**

Ricevi notifica su Telegram (gruppo 8020dev):
```
✨ Nuova Issue Aperta

#42 - [maestro] Export dati energia CSV
...
```

### **Monitorare Progresso**

- Issue page su GitHub: vedi commenti team
- Telegram: ricevi update automatici
- Dashboard Projects (opzionale): Kanban board

### **Chiudere Issue**

- Automatico: Se PR contiene `Closes #N`
- Manuale: Clicca "Close issue" su GitHub
- Via commento: Scrivi "Close #N" in commento

---

## 💻 Per Claudio (Developer)

**Leggi guida completa**: [`WORKFLOW_CLAUDIO.md`](./WORKFLOW_CLAUDIO.md)

### **TL;DR Workflow**

```
1. Ricevi notifica → Leggi issue
2. Commenta "Preso in carico"
3. git checkout -b feature/nome
4. Sviluppa + test
5. git commit -m "feat: ... Refs #N"
6. git push + Crea PR con "Closes #N"
7. Merge → Done!
```

### **Commit Format**

```
feat: descrizione breve

- Dettaglio 1
- Dettaglio 2

Refs #42
```

### **PR Description**

```markdown
Closes #42

## Descrizione
Cosa hai fatto

## Checklist
- [x] Codice testato
- [x] Documentazione aggiornata
```

---

## 🔧 Per Ciccio (DevOps)

**Leggi guida completa**: [`WORKFLOW_CICCIO.md`](./WORKFLOW_CICCIO.md)

### **TL;DR Workflow**

**Task VPS** (script, config, cron):
```
1. Leggi issue
2. Commenta "In corso"
3. Lavora su VPS + testa
4. Commenta con output/log
5. Davide chiude o tu con "Close #N"
```

**Task Git** (codice repo):
```
1-2. (come sopra)
3. git checkout -b infra/nome
4. Modifica + test + commit "Refs #N"
5. Push + PR "Closes #N"
6. Merge → Done!
```

### **Check Issue via CLI**

```bash
gh issue list --repo 80-20Solutions/team-tasks -l "🔧 infra"
```

---

## 📋 Convenzioni Team

### **Branch Naming**

```
feature/nome-feature    # Nuova funzionalità (Claudio)
fix/nome-bug           # Bug fix (Claudio)
infra/cosa             # Infra/DevOps (Ciccio)
refactor/cosa          # Refactoring codice
docs/cosa              # Solo documentazione
```

### **Commit Messages**

Format: `type: description`

**Types**:
- `feat:` - Nuova feature
- `fix:` - Bug fix
- `infra:` - Infrastructure/DevOps
- `refactor:` - Refactoring (no feature/fix)
- `docs:` - Documentazione
- `test:` - Test
- `chore:` - Maintenance

**Sempre includere**: `Refs #N` (issue number)

**Esempi**:
```
feat: add CSV export button
fix: resolve crash on empty data
infra: setup daily database backup
docs: update API documentation
```

### **PR Title Format**

Same as commit: `type: description`

```
feat: CSV export feature
fix: crash on empty export
infra: PostgreSQL connection pooling
```

### **PR Description**

```markdown
Closes #N   ← Importante! Chiude issue automaticamente

## 📝 Descrizione
Cosa hai fatto

## ✅ Checklist
- [x] Testato localmente
- [x] Nessun warning
- [x] Documentazione aggiornata

## 🔗 Related
Issue #N, docs: https://...
```

---

## 🏷️ Labels Guida

### **Per Tipo**
- `🔧 infra` → DevOps, VPS, DB (Ciccio)
- `💻 coding` → Sviluppo app (Claudio)
- `🎨 design` → UI/UX
- `🐛 bug` → Fix urgenti
- `📝 docs` → Documentazione
- `🚀 deploy` → Release
- `❓ question` → Discussioni
- `✨ enhancement` → Miglioramenti

### **Per Priorità**
- `priority:high` → Urgente
- `priority:medium` → Importante
- `priority:low` → Backlog

### **Per Progetto**
- `project:maestro`
- `project:beachref`
- `project:finn`
- `project:stageconnect`
- `project:arbitri-dash`
- `project:8020site`

---

## 🔗 Keywords Magiche GitHub

Usa in commit messages o PR descriptions:

### **Auto-Close Issue**
```
Closes #42
Fixes #42
Resolves #42
```

Quando PR viene mergiata → Issue chiusa automaticamente!

### **Link Issue (no close)**
```
Refs #42
See #42
Related to #42
```

Collega commit/PR a issue senza chiuderla.

### **Multiple Issues**
```
Closes #42, #43, #44
Fixes #42 and resolves #43
```

---

## 📞 Comunicazione

### **Telegram (8020dev)**
- Notifiche automatiche issue
- Chat veloce team
- Update informali

### **GitHub Comments**
- Update formali su issue
- Discussioni tecniche
- Storico decisioni

### **Quando Usare Cosa**

**Telegram**: "Hey @ClaudioDev hai visto issue #42? Serve urgente!"

**GitHub**: Commento su #42 con dettagli tecnici, log, screenshot

**Regola**: Telegram per coordination, GitHub per documentation.

---

## 🔍 Find & Filter Issues

### **Su GitHub Web**

1. https://github.com/80-20Solutions/team-tasks/issues
2. Filter bar:
   - `is:open` - Solo aperte
   - `label:"💻 coding"` - Solo coding
   - `label:"priority:high"` - Solo urgenti
   - `assignee:@me` - Assegnate a te
3. Sort: Priority, Created date, Comments

### **Via GitHub CLI**

```bash
# Tutte aperte
gh issue list --repo 80-20Solutions/team-tasks

# Solo coding
gh issue list --repo 80-20Solutions/team-tasks -l "💻 coding"

# Solo urgenti
gh issue list --repo 80-20Solutions/team-tasks -l "priority:high"

# Per progetto
gh issue list --repo 80-20Solutions/team-tasks -l "project:maestro"

# Assegnate a me
gh issue list --repo 80-20Solutions/team-tasks --assignee @me
```

---

## 🎯 Daily Workflow Ideale

### **Mattina (09:00)**

**Davide**:
- Check issue aperte su GitHub
- Prioritize per la giornata
- Apri nuove issue se serve

**Claudio**:
- Check notifiche Telegram
- Leggi issue assegnate
- Commenta "In corso" su quella che inizi

**Ciccio**:
- Check system health (VPS, DB)
- Heartbeat: `gh issue list` per nuove infra tasks
- Commenta "In corso" su issue

### **Durante Giorno**

**Tutti**:
- Commenta progresso su issue ogni 2-3h
- Taglia in Github quando completi task
- Chiedi aiuto via commenti se bloccato

### **Sera (18:00)**

**Tutti**:
- Aggiorna issue con stato finale giorno
- Push codice (anche WIP se non finito)
- Commenta se task sposta a domani

**Davide**:
- Review PR pronte
- Check progresso generale
- Prioritize per domani

---

## ✅ Checklist Prima di Chiudere Issue

### **Per Developer (Claudio)**
- [ ] Codice testato localmente
- [ ] Nessun warning/error
- [ ] PR creata con `Closes #N`
- [ ] Review richiesta a Davide
- [ ] Branch pushata su GitHub

### **Per DevOps (Ciccio)**
- [ ] Comando/script testato
- [ ] Output documentato in commento
- [ ] Rollback plan presente (se rilevante)
- [ ] Monitoring setup (se rilevante)
- [ ] README/docs aggiornati

### **Per Davide**
- [ ] Funzionalità testata end-to-end
- [ ] Soddisfa requisiti originali
- [ ] Nessun breaking change inatteso
- [ ] OK per merge/close

---

## 🆘 Troubleshooting

### **"Non riesco a pushare branch"**
```bash
git pull origin main --rebase
git push origin feature/nome
```

### **"PR non chiude issue automaticamente"**
- Check: PR description contiene `Closes #N`?
- Check: PR già mergiata?
- Chiudi manualmente se serve

### **"Issue non riceve notifica Telegram"**
- Verifica workflow GitHub Actions: `.github/workflows/telegram-notify.yml`
- Check secrets: `TELEGRAM_BOT_TOKEN` e `TELEGRAM_CHAT_ID`
- Controlla log Actions su GitHub

### **"Non trovo issue giusta per me"**
- Filtra per label: `💻 coding` (Claudio) o `🔧 infra` (Ciccio)
- Ordina per `priority:high`
- Chiedi a Davide in chat Telegram

---

## 📚 Risorse

- **Repository Issues**: https://github.com/80-20Solutions/team-tasks/issues
- **Workflow Claudio**: [`WORKFLOW_CLAUDIO.md`](./WORKFLOW_CLAUDIO.md)
- **Workflow Ciccio**: [`WORKFLOW_CICCIO.md`](./WORKFLOW_CICCIO.md)
- **GitHub CLI Docs**: https://cli.github.com/manual/
- **Git Docs**: https://git-scm.com/doc
- **Telegram Chat**: Gruppo 8020dev

---

## 🎉 Welcome!

Il workflow è semplice:

1. **Issue** = Task da fare
2. **Comment** = Comunicazione
3. **Branch** = Lavoro isolato
4. **Commit** = Snapshot con `Refs #N`
5. **PR** = Richiesta merge con `Closes #N`
6. **Merge** = Issue chiusa automaticamente!

**Domande?** Scrivi nel gruppo 8020dev o apri issue con label `❓ question`.

— Team 80/20 Solutions 🚀
