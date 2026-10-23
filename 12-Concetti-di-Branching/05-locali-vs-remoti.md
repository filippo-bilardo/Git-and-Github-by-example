# 05 - Branch Locali vs Remoti

## 📖 Spiegazione Concettuale

Una delle distinzioni più importanti in Git è quella tra **branch locali** e **branch remoti**. Questa differenza è fondamentale per la collaborazione in team e per comprendere come Git gestisce la sincronizzazione tra repository diversi.

### Branch Locali
I **branch locali** esistono solo nel tuo repository locale. Sono dove lavori quotidianamente, dove fai commit e dove sviluppi le tue funzionalità.

### Branch Remoti
I **branch remoti** sono riferimenti ai branch che esistono in repository remoti (come GitHub, GitLab). Sono "istantanee" dello stato dei branch remoti al momento dell'ultimo fetch/pull.

### Visualizzazione Concettuale

```
Repository Locale                 Repository Remoto (GitHub)
├── main (branch locale)          ├── main
├── feature/login (locale)        ├── feature/login  
├── origin/main (riferimento)     ├── hotfix/bug123
└── origin/feature/login (rif.)   └── develop
```

## 🌐 Tipi di Branch

### 1. Branch Locali Puri
```bash
# Branch che esistono solo localmente
git branch feature/new-ui
git branch experiment/design
```

### 2. Branch di Tracking
```bash
# Branch locali che "seguono" branch remoti
git checkout -b main origin/main
git checkout -b feature origin/feature
```

### 3. Riferimenti Remoti
```bash
# Non sono branch veri, ma riferimenti
origin/main
origin/feature/login
upstream/develop
```

## ⚙️ Sintassi e Comandi

### Visualizzare Branch
```bash
# Solo branch locali
git branch

# Solo branch remoti
git branch -r

# Tutti i branch (locali e remoti)
git branch -a

# Branch con informazioni di tracking
git branch -vv
```

### Creare Branch Locali
```bash
# Nuovo branch locale
git branch feature/new-page

# Nuovo branch e switch
git checkout -b feature/new-page

# Da branch remoto specifico
git checkout -b feature/login origin/feature/login
```

### Gestire Branch Remoti
```bash
# Aggiornare riferimenti remoti
git fetch origin

# Scaricare tutti i branch remoti
git fetch --all

# Eliminare riferimenti a branch remoti cancellati
git remote prune origin
```

### Sincronizzazione
```bash
# Push branch locale su remoto
git push origin feature/login

# Pull da branch remoto
git pull origin main

# Impostare tracking per branch esistente
git branch --set-upstream-to=origin/main main
```

## 🔄 Scenari Pratici

### 1. Sviluppo Locale
```bash
# Scenario: Creare funzionalità localmente
git checkout -b feature/user-profile
echo "Profilo utente" > profile.html
git add profile.html
git commit -m "Add user profile page"

# Il branch esiste solo localmente
git branch
# * feature/user-profile
#   main
```

### 2. Condivisione con Team
```bash
# Scenario: Condividere il branch con il team
git push origin feature/user-profile

# Ora esiste anche remotamente
git branch -a
# * feature/user-profile
#   main
#   remotes/origin/feature/user-profile
#   remotes/origin/main
```

### 3. Collaborazione
```bash
# Scenario: Un collega ha pushato modifiche
git fetch origin
git branch -a
# Nuovo branch remoto visibile

# Creare branch locale per lavorarci
git checkout -b feature/api-integration origin/feature/api-integration
```

### 4. Sincronizzazione Modifiche
```bash
# Scenario: Aggiornare branch locale con modifiche remote
git checkout main
git pull origin main  # Aggiorna main locale

# Oppure separatamente
git fetch origin      # Scarica modifiche
git merge origin/main # Applica modifiche
```

## ⚠️ Errori Comuni e Soluzioni

### 1. Confusione tra Locale e Remoto
```bash
# ❌ ERRORE: Pensare che origin/main sia modificabile
git checkout origin/main
# Sei in detached HEAD!

# ✅ SOLUZIONE: Usa branch locali per lavorare
git checkout main
# oppure
git checkout -b fix-bug origin/main
```

### 2. Branch non Sincronizzati
```bash
# ❌ ERRORE: Lavorare su branch locale obsoleto
git checkout feature/old-work
# (branch non aggiornato da giorni)

# ✅ SOLUZIONE: Aggiorna prima di lavorare
git fetch origin
git merge origin/feature/old-work
# oppure
git pull origin feature/old-work
```

### 3. Push Senza Tracking
```bash
# ❌ ERRORE: Push confuso
git push
# fatal: No upstream branch

# ✅ SOLUZIONE: Specifica o imposta tracking
git push -u origin feature/new-work
# oppure
git push origin feature/new-work
git branch --set-upstream-to=origin/feature/new-work
```

### 4. Branch Remoti Fantasma
```bash
# ❌ ERRORE: Vedere branch remoti cancellati
git branch -r
# origin/old-feature (non esiste più su GitHub)

# ✅ SOLUZIONE: Pulisci riferimenti
git remote prune origin
git fetch --prune
```

## 💡 Best Practices

### 1. Nomenclatura Consistente
```bash
# ✅ BUONA PRATICA: Nomi descrittivi
git checkout -b feature/user-authentication
git checkout -b bugfix/header-alignment
git checkout -b hotfix/security-patch

# ❌ EVITA: Nomi generici
git checkout -b temp
git checkout -b fix
git checkout -b new-stuff
```

### 2. Tracking Automatico
```bash
# ✅ IMPOSTA: Tracking automatico per push
git config --global push.default simple
git config --global branch.autosetupmerge always
```

### 3. Pulizia Regolare
```bash
# ✅ ROUTINE: Pulizia settimanale
git fetch --prune
git branch --merged | grep -v "\*\|main\|develop" | xargs -n 1 git branch -d
```

### 4. Verifica Prima di Push
```bash
# ✅ CONTROLLO: Stato prima del push
git status
git log origin/main..HEAD  # Commit da pushare
git push origin feature/my-work
```

## 🔍 Differenze Chiave

| Aspetto | Branch Locali | Branch Remoti |
|---------|---------------|---------------|
| **Posizione** | Nel tuo repository | Su server remoto |
| **Modifiche** | Dirette (commit) | Solo tramite push |
| **Velocità** | Istantanea | Richiede rete |
| **Persistenza** | Finché non cancellati | Gestiti dal server |
| **Collaborazione** | Solo tua | Condivisi con team |

## 🧪 Quiz di Verifica

### Domanda 1
**Qual è la differenza principale tra `main` e `origin/main`?**

<details>
<summary>Risposta</summary>

`main` è il branch locale dove puoi fare commit direttamente. `origin/main` è un riferimento al branch main sul repository remoto - è una "istantanea" dello stato remoto e non può essere modificato direttamente.
</details>

### Domanda 2
**Cosa succede quando fai `git checkout origin/main`?**

<details>
<summary>Risposta</summary>

Entri in "detached HEAD" state perché `origin/main` è un riferimento remoto, non un branch locale. Per lavorare, dovresti fare `git checkout main` o `git checkout -b new-branch origin/main`.
</details>

### Domanda 3
**Come fai a vedere tutti i branch, locali e remoti?**

<details>
<summary>Risposta</summary>

Usa `git branch -a` per vedere tutti i branch. `-a` sta per "all" e mostra sia i branch locali che i riferimenti ai branch remoti.
</details>

### Domanda 4
**Perché è importante fare `git fetch` regolarmente?**

<details>
<summary>Risposta</summary>

`git fetch` aggiorna i riferimenti ai branch remoti nel tuo repository locale. Senza fetch, non vedrai le modifiche che altri hanno pushato sui branch remoti.
</details>

## 🛠️ Esercizio Pratico: Gestione Branch Locali/Remoti

### Parte 1: Esplorazione
```bash
# 1. Visualizza tutti i branch
git branch -a

# 2. Controlla le informazioni di tracking
git branch -vv

# 3. Aggiorna i riferimenti remoti
git fetch origin
```

### Parte 2: Creazione e Tracking
```bash
# 1. Crea un nuovo branch locale
git checkout -b feature/local-test

# 2. Fai alcune modifiche
echo "Test locale/remoto" > test.txt
git add test.txt
git commit -m "Test branch locale"

# 3. Push con tracking
git push -u origin feature/local-test

# 4. Verifica il tracking
git branch -vv
```

### Parte 3: Simulazione Collaborazione
```bash
# 1. Simula modifica da altro sviluppatore
# (in un'altra directory o con GitHub web interface)

# 2. Fetch aggiornamenti
git fetch origin

# 3. Confronta locale vs remoto
git log HEAD..origin/feature/local-test

# 4. Aggiorna branch locale
git pull origin feature/local-test
```

### Parte 4: Pulizia
```bash
# 1. Merge del branch in main
git checkout main
git merge feature/local-test

# 2. Push main aggiornato
git push origin main

# 3. Cancella branch locale e remoto
git branch -d feature/local-test
git push origin --delete feature/local-test

# 4. Pulisci riferimenti
git remote prune origin
```

## 🔗 Navigazione

**Precedente:** [04 - HEAD e Puntatori](./03-head-puntatori.md)  
**Successivo:** [06 - Strategie di Branching](./05-strategie-branching.md)  
**Torna all'Indice:** [README del Modulo](README.md)  
**Corso Principale:** [Git e GitHub by Example](../README.md)

## 📚 Risorse Aggiuntive

- [Git Documentation - Remote Branches](https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches)
- [Atlassian - Git Remote](https://www.atlassian.com/git/tutorials/syncing)
- [GitHub Docs - Managing Remote Repositories](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories)
