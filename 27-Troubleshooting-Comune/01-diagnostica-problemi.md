# 01 - Diagnostica Problemi

## 📖 Spiegazione Concettuale

La **diagnostica Git** è l'arte di identificare rapidamente la causa di problemi, errori e comportamenti inaspettati. Una diagnosi corretta è fondamentale per applicare la soluzione appropriata senza peggiorare la situazione.

### Principi di Diagnostica

#### 1. **Non Panico** 🧘‍♂️
- Git ha meccanismi di recovery molto robusti
- Raramente si perde lavoro definitivamente
- La maggior parte degli errori è reversibile

#### 2. **Raccolta Informazioni** 🔍
- Comprendi cosa stavi facendo
- Raccogli tutti i messaggi di errore
- Verifica lo stato corrente del repository

#### 3. **Approccio Metodico** 📋
- Un problema alla volta
- Testa le soluzioni in ambiente sicuro
- Documenta cosa funziona

## 🔍 Strumenti di Diagnostica

### 1. **git status** - Lo Stato del Repository

```bash
# Il comando più importante per la diagnostica
git status

# Output tipico e interpretazione:
On branch feature/new-login
Your branch is ahead of 'origin/feature/new-login' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   src/auth.js
        new file:   src/login.html

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        temp.log
```

**Interpretazione:**
- ✅ Repository in stato normale, modifiche in corso
- ℹ️ 2 commit avanti rispetto al remote
- ⚠️ Ci sono sia staged che unstaged changes

### 2. **git log** - Storia e Cronologia

```bash
# Cronologia base
git log --oneline -10

# Con grafico dei branch
git log --oneline --graph --all -20

# Per vedere cosa è successo recentemente
git log --since="2 days ago" --oneline

# Chi ha modificato cosa
git log --author="nome-utente" --oneline
```

### 3. **git reflog** - Il Salvavita

```bash
# Mostra TUTTE le operazioni recenti
git reflog

# Output esempio:
a1b2c3d HEAD@{0}: commit: Add login functionality
d4e5f6g HEAD@{1}: checkout: moving from main to feature/login
h7i8j9k HEAD@{2}: merge: fast-forward
l0m1n2o HEAD@{3}: reset: moving to HEAD~1
```

**Uso cruciale:**
- Recupera commit "persi"
- Annulla reset disastrosi
- Trova stato precedente del repository

### 4. **git diff** - Analisi delle Differenze

```bash
# Differenze working directory vs staging
git diff

# Differenze staging vs ultimo commit
git diff --staged

# Differenze tra branch
git diff main feature/new-feature

# Differenze specifiche per file
git diff HEAD~1 HEAD -- src/auth.js
```

### 5. **git remote -v** - Configurazione Remoti

```bash
git remote -v

# Output atteso:
origin    https://github.com/user/repo.git (fetch)
origin    https://github.com/user/repo.git (push)
upstream  https://github.com/original/repo.git (fetch)
upstream  https://github.com/original/repo.git (push)
```

## 🚨 Categorizzazione Problemi Comuni

### Categoria 1: **Problemi di Stato**

#### Sintomo: "Working directory not clean"
```bash
# Diagnosi
git status

# Possibili cause:
# 1. File modificati non committati
# 2. File in staging area
# 3. Merge conflict irrisolti
# 4. File untracked importanti
```

#### Sintomo: "HEAD detached"
```bash
# Diagnosi
git status
# HEAD detached at a1b2c3d

git log --oneline -5
# Vedi dove sei nella storia
```

### Categoria 2: **Problemi di Sincronizzazione**

#### Sintomo: "Repository ahead/behind"
```bash
git status
# Your branch is ahead of 'origin/main' by 3 commits.
# Your branch is behind 'origin/main' by 2 commits.

# Diagnosi dettagliata
git log origin/main..HEAD     # Commit locali non pushati
git log HEAD..origin/main     # Commit remoti non pullati
```

#### Sintomo: "Merge conflicts"
```bash
git status
# both modified:   src/config.js
# both added:      new-feature.html

# Visualizza conflitti
git diff
```

### Categoria 3: **Problemi di Performance**

#### Sintomo: Git lento
```bash
# Diagnosi dimensioni repository
git count-objects -vH

# Output esempio:
count 1500
size 12.5 MiB
in-pack 1200
packs 3
size-pack 10.2 MiB
```

#### Sintomo: Clone/fetch lento
```bash
# Testa connettività
git ls-remote origin

# Verifica dimensioni
du -sh .git/
```

## 🔬 Processo di Diagnostica Step-by-Step

### Step 1: **Situational Awareness**

```bash
# Dove sono?
pwd
git status
git branch

# Cosa stavo facendo?
git reflog -10
git log --oneline -5

# Configurazione corrente
git config --list --local | grep -E "(user|remote)"
```

### Step 2: **Error Analysis**

```bash
# Riproduci l'errore (se possibile)
git <comando-che-ha-fallito>

# Salva messaggio errore completo
git <comando> 2>&1 | tee error.log

# Verifica verbose
git <comando> --verbose
```

### Step 3: **Environment Check**

```bash
# Versione Git
git --version

# Spazio disco
df -h .

# Permessi
ls -la .git/

# Network (per problemi remote)
ping github.com
```

### Step 4: **Backup Before Fix**

```bash
# Backup branch corrente
git branch backup-$(date +%Y%m%d-%H%M%S)

# O backup completo
cp -r .git ../backup-repo-git

# Reflog backup
git reflog > ../reflog-backup.txt
```

## 📊 Diagnostic Checklists

### 🔍 **General Problem Checklist**

```markdown
□ Raccolto messaggio errore completo
□ Verificato git status
□ Controllato git reflog
□ Identificato ultimo comando funzionante
□ Creato backup se necessario
□ Testato in repository separato se possibile
```

### 🌐 **Remote Problems Checklist**

```markdown
□ Verificato connessione internet
□ Testato git remote -v
□ Controllato autenticazione (SSH/HTTPS)
□ Verificato permessi repository
□ Testato con git ls-remote
```

### 🔀 **Merge/Rebase Problems Checklist**

```markdown
□ Identificato tipo di merge/rebase in corso
□ Verificato file in conflitto
□ Controllato stato con git status
□ Valutato abort vs risoluzione manuale
```

### ⚡ **Performance Problems Checklist**

```markdown
□ Misurato dimensioni repository
□ Verificato spazio disco disponibile
□ Controllato configurazione Git
□ Testato su repository diverso
□ Verificato network per problemi remoti
```

## 🧰 Diagnostic Tools Avanzati

### 1. **git fsck** - File System Check

```bash
# Verifica integrità repository
git fsck --full

# Mostra oggetti non raggiungibili
git fsck --unreachable

# Fix automatico (use with caution)
git fsck --full --strict
```

### 2. **git gc** - Garbage Collection

```bash
# Cleanup manuale
git gc

# Garbage collection aggressiva
git gc --aggressive --prune=now

# Verifica prima di cleanup
git gc --dry-run
```

### 3. **git show** - Analisi Commit Specifici

```bash
# Dettagli commit specifico
git show a1b2c3d

# Solo le modifiche
git show a1b2c3d --stat

# Specifico file in commit
git show a1b2c3d:path/to/file.js
```

### 4. **git blame** - Analisi Cambiamenti

```bash
# Chi ha modificato ogni riga
git blame src/auth.js

# In un range specifico
git blame -L 10,20 src/auth.js

# Ignora whitespace changes
git blame -w src/auth.js
```

## 🎯 Diagnostic Scenarios Comuni

### Scenario 1: "Git non risponde"

**Sintomi:**
- Comandi Git si bloccano
- Nessun output dopo molto tempo

**Diagnostica:**
```bash
# Check processi
ps aux | grep git

# Verifica .git/locks
ls -la .git/*.lock
ls -la .git/refs/heads/*.lock

# Spazio disco
df -h .
```

### Scenario 2: "Repository corrotto"

**Sintomi:**
- Errori "object file is empty"
- "Unable to read" messages

**Diagnostica:**
```bash
# File system check
git fsck --full

# Verifica oggetti
find .git/objects/ -size 0

# Check backup
ls .git/refs/
```

### Scenario 3: "Merge impossibile"

**Sintomi:**
- "Would be overwritten by merge"
- Conflitti irrisolvibili

**Diagnostica:**
```bash
# Stato corrente
git status

# Analizza differenze
git diff HEAD origin/main

# Check file che causano problemi
git clean -n -d  # Dry run
```

## 📚 Diagnostic Resources

### Log Files Utili

```bash
# Git logs di sistema (se disponibili)
tail -f /var/log/git.log

# SSH debug (per problemi autenticazione)
ssh -vT git@github.com

# Network tracing
git config --global http.postBuffer 524288000
```

### Configuration Debug

```bash
# Configurazione completa
git config --list --show-origin

# Solo configurazioni problematiche
git config --list | grep -E "(http|ssh|user|remote)"

# Verifica configurazione specifica
git config --get-regexp "remote.*"
```

## 🧭 Navigazione del Corso

- [📑 Indice](README.md)
- [➡️ Recovery Strategies](02-recovery-strategies.md)
