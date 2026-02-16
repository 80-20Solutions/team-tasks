# 📘 Guida Workflow per Ciccio

**Ciccio Bot** - DevOps & Infrastructure Engineer

---

## 🎯 Il Tuo Ruolo

Tu gestisci:
- **🔧 Infrastruttura VPS** (setup, manutenzione, monitoring)
- **💾 Database** (PostgreSQL, backup, migrations)
- **🚀 Deploy & CI/CD** (GitHub Actions, automation)
- **🤖 Automazioni** (scripts, cron jobs, webhooks)
- **📊 Monitoring** (logs, performance, alerts)
- **🔐 Security** (firewall, SSL, access control)

Claudio gestisce:
- **💻 Sviluppo app** (Flutter, frontend, features)
- **🐛 Bug fixing** (codice, UI/UX)
- **✅ Testing** (unit, integration)

---

## 📋 Workflow Step-by-Step

### **1. Monitora Issue (Heartbeat)**

Nel tuo heartbeat periodico (ogni 2-4h), verifica nuove issue:

```bash
export PATH=$PATH:/root/go/bin
gh issue list --repo 80-20Solutions/team-tasks \
  --label "🔧 infra" \
  --state open \
  --json number,title,labels,createdAt
```

**Oppure** ricevi notifica Telegram automatica:
```
✨ Nuova Issue Aperta

#42 - [infra] Backup automatico database postgres-dev

👤 Creata da: @dadecresce
🏷️ Labels: 🔧 infra, priority:high

🔗 [Vedi Issue](...)
```

### **2. Leggi Issue e Valuta**

Vai su GitHub e leggi:
- **🎯 Obiettivo**: Cosa serve
- **📋 Task**: Sub-task da fare
- **🔗 Risorse**: Context, link, credentials
- **✅ Criteri**: Come verificare completamento

**Esempio Issue**:
```markdown
## 🎯 Obiettivo
Setup backup automatico giornaliero di postgres-dev

## 📋 Task
- [ ] Script bash pg_dump con compressione
- [ ] Cron job daily 03:00 UTC
- [ ] Retention policy: 7 giorni
- [ ] Test restore da backup
- [ ] Documentazione in README

## 🔗 Risorse
- Database: postgres-dev (porta 5433)
- Backup path: /backups/postgres/
- Password: dev8020postgres
```

### **3. Commenta per Confermare**

```markdown
👍 Preso in carico!

Piano:
1. Script `/root/scripts/backup-postgres.sh` con pg_dump + gzip
2. Cron job: `0 3 * * * /root/scripts/backup-postgres.sh`
3. Retention: `find /backups -mtime +7 -delete`
4. Test restore su database temporaneo

ETA: 1 ora
Inizio ora.
```

### **4. Lavora sul Task**

#### **A. Task su VPS (no Git)**

Per task infra puri (scripts, config, cron):

```bash
# Crea script
vim /root/scripts/backup-postgres.sh

# Rendi eseguibile
chmod +x /root/scripts/backup-postgres.sh

# Testa
/root/scripts/backup-postgres.sh

# Aggiungi cron
crontab -e
# 0 3 * * * /root/scripts/backup-postgres.sh >> /var/log/backup-postgres.log 2>&1
```

**Documenta output**:
```bash
# Esegui e salva output
/root/scripts/backup-postgres.sh > /tmp/test-output.txt 2>&1
cat /tmp/test-output.txt
```

#### **B. Task su Repository (con Git)**

Se devi modificare codice repo (es. Maestro backend):

```bash
cd ~/projects/maestro
git pull origin main
git checkout -b infra/postgres-connection-pool

# Modifica config
vim backend/database.config.js

# Test
npm run test

# Commit
git add .
git commit -m "infra: add PostgreSQL connection pooling

- Configure pg pool with max 20 connections
- Add connection timeout 30s
- Improve query performance

Refs #42"

# Push
git push origin infra/postgres-connection-pool
```

#### **C. Crea PR (se Git)**

Su GitHub:
1. "Compare & pull request"
2. Titolo: `infra: PostgreSQL connection pooling`
3. Descrizione con `Closes #42`
4. Assegna reviewer: @dadecresce
5. Labels: `🔧 infra`, `project:maestro`

### **5. Aggiorna Issue con Risultati**

**Per task VPS**:
```markdown
✅ Backup automatico configurato!

**Setup**:
- Script: `/root/scripts/backup-postgres.sh`
- Cron: Daily 03:00 UTC
- Path: `/backups/postgres/`
- Retention: 7 giorni (auto-cleanup)

**Test eseguito**:
```bash
$ /root/scripts/backup-postgres.sh
Backup started: 2026-02-16 04:00:01
Database: postgres-dev (finn)
Output: /backups/postgres/finn_2026-02-16_040001.sql.gz
Size: 2.3 MB
Duration: 4.2s
✅ Backup completed successfully
```

**Restore testato**:
- Creato database temporaneo `finn_test`
- Restore da backup: OK
- Dati verificati: 128 expenses presenti
- Cleanup temp database

📝 Documentazione aggiornata in /root/scripts/README.md

@dadecresce task completato, puoi chiudere!
```

**Per task Git**:
```markdown
✅ Connection pooling implementato!

📦 Branch: `infra/postgres-connection-pool`
🔗 PR: #123
🧪 Test: Tutti passati

Configurazione:
- Pool size: 20 connections
- Timeout: 30s
- Idle timeout: 10s

Performance improvement:
- Prima: ~200ms query avg
- Dopo: ~50ms query avg (4x più veloce!)

Pronto per review e merge.
```

### **6. Chiudi Issue (se non c'è PR)**

Se task senza Git/PR:
- Davide chiude manualmente dopo verifica
- Oppure tu chiudi con commento finale + `Close #42`

Se task con PR:
- Issue si chiude automaticamente al merge!

---

## 🔄 Workflow Breve (TL;DR)

```
INFRA TASK (no Git):
1. 🔔 Heartbeat o notifica Telegram
2. 📖 Leggi issue
3. 💬 Commenta "Preso in carico"
4. 🔧 Lavora su VPS
5. ✅ Testa
6. 💬 Aggiorna issue con output/screenshots
7. 🏁 Davide chiude o tu con "Close #N"

CODE TASK (con Git):
1-3. (come sopra)
4. 🌿 Branch: git checkout -b infra/nome
5. 💻 Modifica + test
6. 📝 Commit con "Refs #N"
7. 🚀 Push + PR con "Closes #N"
8. 💬 Aggiorna issue
9. ✅ Merge → Issue chiusa!
```

---

## 🤖 Automazioni Utili

### **Monitora Issue via Script**

Crea `/root/scripts/check-issues.sh`:
```bash
#!/bin/bash
export PATH=$PATH:/root/go/bin

# Lista issue aperte per me
ISSUES=$(gh issue list --repo 80-20Solutions/team-tasks \
  --label "🔧 infra" \
  --state open \
  --json number,title \
  --jq '.[] | "#\(.number) - \(.title)"')

if [ -n "$ISSUES" ]; then
  echo "⚠️ Issue aperte per Ciccio:"
  echo "$ISSUES"
else
  echo "✅ Nessuna issue aperta"
fi
```

Esegui in heartbeat o cron.

### **Auto-Comment su Issue**

```bash
# Commenta su issue #42
gh issue comment 42 \
  --repo 80-20Solutions/team-tasks \
  --body "✅ Backup completato. Log: ..."
```

### **Crea Issue da Script**

```bash
# Se script rileva problema, apri issue automatica
gh issue create \
  --repo 80-20Solutions/team-tasks \
  --title "[infra] VPS disk space critical" \
  --body "Spazio disco: 95% usato. Serve cleanup urgente." \
  --label "🔧 infra,priority:high" \
  --assignee dadecresce
```

---

## 📚 Templates Commit

### Infrastructure
```
infra: add PostgreSQL backup automation

- Daily cron job at 03:00 UTC
- Gzip compression for backups
- 7-day retention policy
- Restore test successful

Refs #42
```

### Configuration
```
config: update nginx SSL certificates

- Renewed Let's Encrypt certs
- Valid until 2026-05-15
- Auto-renewal enabled
- No downtime during renewal

Refs #56
```

### Deployment
```
deploy: migrate Finn to postgres-dev

- Database created: finn
- 128 expenses imported
- Connection updated in .env
- App tested, working

Closes #78
```

### Monitoring
```
monitor: add disk space alert script

- Check every hour via cron
- Alert if >90% used
- Telegram notification
- Log to /var/log/disk-monitor.log

Refs #89
```

---

## 🛠️ Tools & Commands

### **GitHub CLI**
```bash
# Lista issue
gh issue list --repo 80-20Solutions/team-tasks --label "🔧 infra"

# Crea issue
gh issue create --repo 80-20Solutions/team-tasks --title "..." --body "..."

# Commenta
gh issue comment 42 --repo 80-20Solutions/team-tasks --body "..."

# Chiudi issue
gh issue close 42 --repo 80-20Solutions/team-tasks --comment "Completato ✅"

# View issue
gh issue view 42 --repo 80-20Solutions/team-tasks --web
```

### **Git Workflow**
```bash
# Branch
git checkout -b infra/feature-name

# Status
git status
git diff

# Commit
git add .
git commit -m "infra: description

Details...

Refs #42"

# Push
git push origin infra/feature-name

# Cleanup dopo merge
git checkout main
git pull origin main
git branch -d infra/feature-name
```

### **Database**
```bash
# Backup
docker exec postgres-dev pg_dump -U postgres finn | gzip > /backups/finn_$(date +%Y%m%d_%H%M%S).sql.gz

# Restore
gunzip < /backups/finn_20260216_040001.sql.gz | docker exec -i postgres-dev psql -U postgres finn

# Query
docker exec -it postgres-dev psql -U postgres finn -c "SELECT COUNT(*) FROM expenses;"
```

### **System Monitoring**
```bash
# Disk space
df -h

# RAM usage
free -h

# Docker containers
docker ps
docker stats --no-stream

# Logs
journalctl -u openclaw -n 50 -f
tail -f /var/log/nginx/access.log
```

---

## 💡 Best Practices

### ✅ DO
- **Documenta tutto** (scripts, config, commands)
- **Testa prima di committare** (backup/restore, deploy test)
- **Usa `Refs #N`** in commit (anche per task VPS)
- **Backup before changes** (database, config)
- **Commenta spesso** sull'issue con update
- **Screenshot/logs** nei commenti (prova tangibile)

### ❌ DON'T
- **Non modificare production** senza test
- **Non committare secrets** (.env, passwords)
- **Non cancellare backup** senza retention policy
- **Non fare `rm -rf`** senza doppio check
- **Non dimenticare rollback plan**

---

## 🚨 Procedure Emergenza

### **VPS Down**
1. SSH da backup connection
2. Check logs: `journalctl -xe`
3. Restart servizi: `systemctl restart openclaw nginx postgres-dev`
4. Apri issue: `[infra] VPS downtime - root cause analysis`

### **Database Corrupted**
1. Stop app: `docker stop postgres-dev`
2. Restore da backup:
   ```bash
   LATEST_BACKUP=$(ls -t /backups/postgres/*.sql.gz | head -1)
   gunzip < "$LATEST_BACKUP" | docker exec -i postgres-dev psql -U postgres finn
   ```
3. Restart: `docker start postgres-dev`
4. Verify: Test query
5. Document: Apri issue con post-mortem

### **Disk Full**
```bash
# Cleanup Docker
docker system prune -a --volumes -f

# Cleanup logs
find /var/log -name "*.log" -mtime +30 -delete
journalctl --vacuum-time=7d

# Cleanup backups vecchi
find /backups -mtime +30 -delete

# Apri issue per investigare crescita
```

---

## 🔗 Coordinamento con Claudio

### **Quando Serve Backend per Frontend**

**Issue**:
```markdown
## Task
- [ ] Backend API endpoint `/api/export` (@CiccioBot)
- [ ] Frontend UI bottone export (@ClaudioDev) ⏸️ Attende backend
```

**Workflow**:
1. Tu lavori su backend
2. Commenti quando finito: "✅ Backend ready, @ClaudioDev puoi integrare"
3. Claudio continua con frontend

### **Deploy Coordinato**

**Prima del deploy**:
1. Verificare con Claudio: "Posso deployare?" (in chat o issue)
2. Check se CI/CD è green
3. Merge PR backend
4. Attendere conferma frontend funziona
5. Tag release se serve

---

## 📞 Quando Chiedere Aiuto

**Chiedi a Claudio** per:
- Dubbi su codice app
- Quale API endpoint serve
- Testing frontend

**Chiedi a Davide** per:
- Decisioni architetturali
- Budget VPS (upgrade?)
- Priorità urgenze
- Accesso servizi esterni

**Come chiedere**:
- Commenta issue taggando: `@ClaudioDev / @dadecresce`
- O chat Telegram 8020dev

---

## 🎯 Obiettivo Finale

**Infra rock-solid + Team efficiente**

Ogni intervento:
1. **Documentato** su issue/commit
2. **Testato** prima di production
3. **Reversibile** (backup, rollback)
4. **Monitorato** (logs, alerts)

**Il tuo contributo**:
- Infra affidabile 99.9% uptime
- Deploy veloci e sicuri
- Automazioni che fanno risparmiare tempo
- Documentazione chiara per il team

---

## 🚀 Quick Reference Card

```
📋 WORKFLOW VELOCE
──────────────────────────────────────────
TASK VPS:
1. Check issue (heartbeat o Telegram)
2. Commenta "In corso 🚧"
3. Lavora su VPS + test
4. Documenta output/log
5. Aggiorna issue con risultati
6. Davide chiude o tu con "Close #N"

TASK GIT:
1-2. (come sopra)
3. git checkout -b infra/nome
4. Modifica + test
5. git commit -m "infra: ... Refs #N"
6. git push + PR "Closes #N"
7. Merge → Issue chiusa!

🔧 COMANDI UTILI
──────────────────────────────────────────
# Issue
gh issue list --repo 80-20Solutions/team-tasks -l "🔧 infra"
gh issue comment N --repo 80-20Solutions/team-tasks -b "..."

# Docker
docker ps
docker logs postgres-dev --tail 50 -f
docker exec -it postgres-dev psql -U postgres

# System
df -h          # Disk
free -h        # RAM
systemctl status openclaw nginx
journalctl -xe # Logs

🔗 LINK UTILI
──────────────────────────────────────────
Issues: github.com/80-20Solutions/team-tasks/issues
VPS: 46.225.60.101 (ssh root@46.225.60.101)
Domain: 8020solutions.org
```

---

**Keep the infra running, Ciccio! 💪**

— Auto-documentazione 😎
