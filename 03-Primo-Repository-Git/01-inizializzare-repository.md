# 🎯 Inizializzare un Repository Git

## 📋 Introduzione

Inizializzare un repository Git è il primo passo per tracciare le modifiche del tuo progetto. È come dire a Git: "Da questo momento in poi, tieni traccia di tutto quello che succede in questa cartella".

---

## 🚀 Il Comando `git init`

### Sintassi Base

```bash
git init [nome-cartella]
```

### Esempi Pratici

#### Inizializzare nella cartella corrente
```bash
# Inizializza repository nella cartella attuale
$ git init
Initialized empty Git repository in /home/user/mio-progetto/.git/
```

#### Creare una nuova cartella con repository
```bash
# Crea cartella e inizializza repository
$ git init mio-nuovo-progetto
Initialized empty Git repository in /home/user/mio-nuovo-progetto/.git/

$ cd mio-nuovo-progetto
$ ls -la
drwxr-xr-x  3 user user  96 Dec 10 10:30 .
drwxr-xr-x  8 user user 256 Dec 10 10:30 ..
drwxr-xr-x  7 user user 224 Dec 10 10:30 .git
```

---

## 🔍 Cosa Succede Durante l'Inizializzazione

Quando esegui `git init`, Git:

1. **🗂️ Crea la cartella `.git`** nella directory corrente
2. **🏗️ Imposta la struttura interna** del repository
3. **📋 Inizializza il database degli oggetti** Git
4. **🔧 Configura le impostazioni di base** del repository

### Struttura della Cartella `.git`

```
.git/
├── HEAD                 # Punta al branch corrente
├── config               # Configurazioni locali del repository
├── description          # Descrizione del repository
├── hooks/               # Script automatici per eventi Git
├── info/                # File di configurazione globali
├── objects/             # Database degli oggetti Git (commit, blob, tree)
├── refs/                # Reference a branch, tag, etc.
└── index                # Area di staging (creata al primo add)
```

---

## 🎯 Workflow Post-Inizializzazione

### 1. Verifica dello Stato
```bash
$ git status
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

### 2. Configurazione Locale (Opzionale)
```bash
# Impostare identità per questo specifico repository
$ git config user.name "Mario Rossi"
$ git config user.email "mario@example.com"

# Verificare la configurazione
$ git config --list --local
```

### 3. Primo File e Commit
```bash
# Creare un file
$ echo "# Mio Primo Progetto" > README.md

# Aggiungerlo al tracking
$ git add README.md

# Fare il primo commit
$ git commit -m "Initial commit: aggiunto README"
```

---

## 🎨 Branch di Default

### Impostare il Branch Principale

**Metodo Moderno (Git 2.28+):**
```bash
# Configurazione globale
$ git config --global init.defaultBranch main

# Inizializzazione con branch main
$ git init
$ git status
On branch main
```

**Metodo Tradizionale:**
```bash
# Inizializzazione (branch master di default)
$ git init

# Rinominare a main
$ git branch -m master main
```

---

## 🛠️ Opzioni Avanzate

### Repository Bare
```bash
# Repository senza working directory (per server)
$ git init --bare mio-repository.git
```

### Template Personalizzato
```bash
# Utilizzare template personalizzato
$ git init --template=/path/to/template
```

### Quiet Mode
```bash
# Inizializzazione silenziosa
$ git init --quiet
```

---

## 📊 Best Practices

### ✅ Do's
- **📁 Una cartella = un repository** per progetti separati
- **📝 README.md** come primo file del progetto
- **🔧 Configura identità** prima del primo commit
- **📋 .gitignore** fin dall'inizio per file non necessari

### ❌ Don'ts  
- **🚫 Non inizializzare** repository annidati
- **🚫 Non inizializzare** nella home directory
- **🚫 Non ignorare** la configurazione dell'identità
- **🚫 Non eliminare** la cartella `.git` per sbaglio

---

## 🔍 Troubleshooting

### Problema: "fatal: not a git repository"
```bash
# Soluzione: verificare di essere nella cartella corretta
$ pwd
$ ls -la | grep .git

# Se necessario, ri-inizializzare
$ git init
```

### Problema: Repository già esistente
```bash
$ git init
Reinitialized existing Git repository in /path/to/repo/.git/

# Non è un errore - Git reinizializza senza perdere dati
```

### Problema: Permessi insufficienti
```bash
# Verificare permessi della cartella
$ ls -la
$ chmod 755 .

# Riprovare l'inizializzazione
$ git init
```

---

## 🎯 Esercizio Pratico

**Crea tre repository diversi:**

1. **Repository per progetto web**
```bash
mkdir website-project
cd website-project
git init
echo "# My Website" > README.md
git add README.md
git commit -m "Initial commit: progetto website"
```

2. **Repository per documentazione**
```bash
git init documentation --bare
# Repository bare per condivisione
```

3. **Repository con configurazione personalizzata**
```bash
mkdir special-project
cd special-project
git init
git config user.name "Development Team"
git config user.email "dev@company.com"
```

---

## 🔗 Collegamenti Utili

- **📚 Prossima guida**: [02 - Anatomia Directory Git](./02-anatomia-directory-git.md)
- **🎯 Esempi pratici**: [01 - Progetto Sito Web](esempi/01-progetto-sito-web.md)
- **📖 Documentazione ufficiale**: [git-init](https://git-scm.com/docs/git-init)
