# 📘 Guida Workflow per Claudio

**Claudio Dev** - Senior Developer, Coding Tasks

---

## 🎯 Il Tuo Ruolo

Tu gestisci:
- **💻 Sviluppo app** (Flutter, React, TypeScript)
- **🔧 Feature implementation**
- **🐛 Bug fixing**
- **✅ Testing codice**
- **📝 Code review**

Ciccio gestisce:
- **🔧 DevOps/Infra** (VPS, database, deploy)
- **🤖 Automazioni**
- **📊 Monitoring**

---

## 📋 Workflow Step-by-Step

### **1. Ricevi Notifica su Telegram**

Quando Davide apre una issue su `team-tasks`, ricevi notifica nel gruppo **8020dev**:

```
✨ Nuova Issue Aperta

#42 - [maestro] Export dati energia in CSV

👤 Creata da: @dadecresce
🏷️ Labels: 💻 coding, project:maestro, priority:high

🔗 [Vedi Issue](https://github.com/80-20Solutions/team-tasks/issues/42)
```

### **2. Leggi la Issue su GitHub**

Vai sul link e leggi:
- **🎯 Obiettivo**: Cosa fare
- **📋 Task Checklist**: Lista sub-task
- **🔗 Risorse**: Link repo, docs, API
- **✅ Criteri Completamento**: Come sapere che è finito

**Esempio Issue**:
```markdown
## 🎯 Obiettivo
Aggiungere export CSV dei dati energia in Maestro

## 📋 Task
- [ ] Backend: endpoint API `/api/energy/export` (@CiccioBot)
- [ ] Frontend: bottone "Export CSV" nella dashboard (@ClaudioDev)
- [ ] Integrazione chiamata API
- [ ] Test con dati reali
- [ ] Documentazione

## 🔗 Risorse
- Repo: https://github.com/ecologicaleaving/maestro
- Design Figma: https://...
```

### **3. Commenta per Confermare**

Vai su GitHub e **scrivi un commento** sull'issue:

```markdown
👍 Preso in carico!

Piano:
- Aggiungo bottone "Export CSV" in energy_dashboard.dart
- DateRangePicker per selezionare periodo
- Download CSV via dio package

Inizio ora, finisco stasera.
```

**Perché commentare?**
- Davide sa che stai lavorando
- Ciccio vede il tuo progresso (se deve coordinare)
- Storico completo del lavoro

### **4. Lavora sul Codice**

#### **A. Crea Branch**

**Sul tuo PC** (Windows):

```powershell
cd C:\Projects\maestro
git pull origin main
git checkout -b feature/csv-export
```

**Convenzione nomi branch**:
- `feature/nome-feature` - Nuove funzionalità
- `fix/nome-bug` - Bug fix
- `refactor/cosa` - Refactoring
- `docs/cosa` - Solo documentazione

#### **B. Sviluppa**

Scrivi il codice normalmente con:
- Hot reload
- Debugging
- Testing locale

#### **C. Committa con Riferimento Issue**

**IMPORTANTE**: Nei commit includi `Refs #N` dove N è il numero issue:

```powershell
git add .
git commit -m "feat: add CSV export button in energy dashboard

- Add Export button in EnergyDashboardWidget
- Integrate DateRangePicker for date selection
- Download CSV via API call using dio package
- Add loading indicator during export

Refs #42"
```

**Perché `Refs #42`?**
- Collega automaticamente il commit all'issue su GitHub
- Puoi vedere tutti i commit relativi all'issue
- Traceability completa

#### **D. Push Branch**

```powershell
git push origin feature/csv-export
```

### **5. Aggiorna la Issue**

Torna su GitHub e **commenta** con il progresso:

```markdown
✅ Frontend completato!

- Bottone "Export CSV" aggiunto in dashboard
- DateRangePicker per range date
- Chiamata API `/api/energy/export` integrata
- Download automatico file CSV
- Loading indicator durante export

📦 Branch: `feature/csv-export`
🔗 Commit: abc123f

Pronto per test. @dadecresce puoi provare?
```

### **6. Crea Pull Request**

**Su GitHub** (vai sul repo del progetto, es. `maestro`):

1. Clicca **"Compare & pull request"** (appare dopo il push)
2. Compila:
   - **Titolo**: `feat: CSV export feature`
   - **Descrizione**:
   ```markdown
   ## 📝 Descrizione
   Implementa export CSV dei dati energia con filtro date
   
   ## ✅ Checklist
   - [x] Bottone UI aggiunto
   - [x] API integration
   - [x] Loading states
   - [x] Error handling
   - [x] Test manuale completato
   
   ## 🔗 Related
   Closes #42
   ```
   
3. **IMPORTANTE**: Scrivi `Closes #42` nella descrizione
   - Quando la PR viene mergiata, **issue si chiude automaticamente**!

4. Assegna reviewer: **@dadecresce**
5. Labels: `💻 coding`, `project:maestro`
6. Clicca **"Create pull request"**

### **7. Review e Merge**

Davide:
- Testa la feature
- Lascia commenti se serve modifiche
- Approva la PR

Tu:
- Risolvi eventuali richieste di modifica
- Pushare altri commit nello stesso branch

Quando approvata:
- **Davide mergia** (o tu se hai i permessi)
- Issue si chiude automaticamente ✅
- Branch può essere eliminato

---

## 🔄 Workflow Breve (TL;DR)

```
1. 🔔 Ricevi notifica Telegram
2. 📖 Leggi issue su GitHub
3. 💬 Commenta "Preso in carico"
4. 🌿 Crea branch: git checkout -b feature/nome
5. 💻 Sviluppa
6. 📝 Commit con "Refs #N"
7. 🚀 Push branch
8. 💬 Aggiorna issue con progresso
9. 📬 Crea PR con "Closes #N"
10. ✅ Merge → Issue chiusa!
```

---

## 📚 Templates Commit

### Feature
```
feat: add CSV export functionality

- Implement export button in dashboard
- Add date range selector
- Integrate API call

Refs #42
```

### Bug Fix
```
fix: resolve crash on empty data export

- Add null check before accessing data
- Show error message if no data available
- Add unit test for edge case

Fixes #56
```

### Refactor
```
refactor: extract CSV generation to separate service

- Move logic from UI to service layer
- Add unit tests for service
- Improve code maintainability

Refs #78
```

### Documentation
```
docs: add CSV export usage guide

- Document export feature in README
- Add screenshots
- Include API endpoint details

Refs #42
```

---

## 🏷️ Keywords Magiche

Usa nei commit o PR description per azioni automatiche:

- **`Closes #N`** - Chiude issue N quando mergiata
- **`Fixes #N`** - Chiude issue N (per bug)
- **`Resolves #N`** - Chiude issue N
- **`Refs #N`** - Collega a issue N (senza chiuderla)

**Esempi**:
```markdown
Closes #42
Closes #42, #43, #44
Fixes #56
Refs #78
```

---

## 🔍 Come Trovare Issue da Fare

### **Su GitHub**
1. Vai su https://github.com/80-20Solutions/team-tasks/issues
2. Filtra per label: `💻 coding`
3. Ordina per: `priority:high` → `medium` → `low`

### **Via GitHub CLI** (sul tuo PC)
```powershell
# Lista issue per te
gh issue list --repo 80-20Solutions/team-tasks --label "💻 coding" --state open

# Issue urgenti
gh issue list --repo 80-20Solutions/team-tasks --label "priority:high" --state open
```

### **Su Telegram**
Ricevi notifiche automatiche quando:
- Davide apre issue con label `💻 coding`
- Vieni taggato in un commento: `@ClaudioDev`
- Issue viene assegnata a te

---

## 💡 Best Practices

### ✅ DO
- **Commenta spesso** sull'issue per aggiornare
- **Usa branch per ogni feature** (non lavorare su `main`)
- **Includi `Refs #N`** in tutti i commit
- **Testa prima di pushare**
- **Scrivi commit messages descrittivi**
- **Chiedi se non sei sicuro** (commenta sull'issue)

### ❌ DON'T
- **Non pushare su `main`** direttamente
- **Non usare commit generici** tipo "fix" o "update"
- **Non dimenticare `Refs #N`** nei commit
- **Non aprire PR senza testare**
- **Non modificare `.gitignore` o config** senza chiedere

---

## 🚨 Casi Speciali

### **Issue Bloccata da Ciccio**

Se l'issue dice:
```markdown
## Task
- [ ] Backend API (@CiccioBot) ⏳
- [ ] Frontend UI (@ClaudioDev) ⏸️ Attende backend
```

**Cosa fare**:
1. Commenta: "In attesa di backend. Lavoro su UI intanto?"
2. Prepara UI con mock data
3. Integra API quando Ciccio finisce

### **Bug Urgente**

Se ricevi notifica:
```
🔥 URGENT - Bug Critico
#89 - [maestro] App crasha all'avvio
```

**Workflow veloce**:
1. Branch: `fix/crash-on-startup`
2. Fix rapido
3. Test su device
4. Push + PR con `Fixes #89`
5. Chiedi merge immediato a Davide

### **Conflitti Git**

Se al push vedi conflitti:

```powershell
git pull origin main
# Risolvi conflitti manualmente
git add .
git commit -m "merge: resolve conflicts from main"
git push origin feature/nome
```

Chiedi aiuto a Ciccio se serve!

---

## 📞 Quando Chiedere Aiuto

**Chiedi a Ciccio** (@CiccioBot) per:
- Problemi VPS, database, deploy
- Configurazioni environment
- API endpoint non funzionanti
- Accesso a servizi

**Chiedi a Davide** (@dadecresce) per:
- Decisioni di design/UX
- Priorità task
- Requisiti non chiari
- Approvazioni architetturali

**Come chiedere**:
- Commenta sull'issue taggando: `@CiccioBot ho bisogno di...`
- O scrivi nel gruppo Telegram 8020dev

---

## 🎯 Obiettivo Finale

**Workflow pulito = Team efficiente**

Ogni issue diventa:
1. **Tracciabile**: Chi ha fatto cosa, quando
2. **Documentata**: Storico decisioni e cambiamenti
3. **Collegata**: Commit → PR → Issue = tutto connesso
4. **Automatica**: PR mergiata = Issue chiusa

**Il tuo contributo**:
- Code di qualità
- Comunicazione costante
- Commit ben documentati
- PR pronte per review

---

## 🚀 Quick Reference Card

```
📋 WORKFLOW VELOCE
──────────────────────────────────────────
1. Leggi issue su GitHub
2. Commenta "In corso 🚧"
3. git checkout -b feature/nome
4. Sviluppa + test
5. git commit -m "feat: ... Refs #N"
6. git push origin feature/nome
7. Crea PR con "Closes #N"
8. Commenta progresso sull'issue
9. Richiedi review a @dadecresce
10. ✅ Merge → Done!

🔗 LINK UTILI
──────────────────────────────────────────
Issues: github.com/80-20Solutions/team-tasks/issues
Maestro: github.com/ecologicaleaving/maestro
BeachRef: github.com/ecologicaleaving/BeachRef
Finn: github.com/ecologicaleaving/finn

💬 COMUNICAZIONE
──────────────────────────────────────────
Telegram: gruppo 8020dev
Tag Ciccio: @CiccioBot (infra/backend)
Tag Davide: @dadecresce (decisioni)
```

---

**Benvenuto nel team, Claudio! 🎉**

Per domande su questa guida: scrivi nel gruppo 8020dev o apri issue con label `❓ question`.

— Ciccio 😎
