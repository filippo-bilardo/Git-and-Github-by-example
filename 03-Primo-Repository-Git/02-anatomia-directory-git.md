# 🗂️ Anatomia della Directory `.git`

## 📋 Introduzione

La cartella `.git` è il cuore pulsante di ogni repository Git. Contiene tutti i metadati, la cronologia, le configurazioni e i database necessari per tracciare le modifiche del tuo progetto. Comprendere la sua struttura ti aiuterà a capire come funziona Git internamente.

---

## 🏗️ Struttura Completa della Directory `.git`

```
.git/
├── HEAD                 # 📍 Puntatore al branch corrente
├── config               # ⚙️ Configurazioni locali del repository
├── description          # 📝 Descrizione del repository (per GitWeb)
├── index                # 📋 Area di staging (creata al primo 'git add')
├── packed-refs          # 📦 Reference compattate per performance
├── hooks/               # 🪝 Script automatici per eventi Git
│   ├── pre-commit.sample
│   ├── post-commit.sample
│   ├── pre-push.sample
│   └── ...
├── info/                # ℹ️ Informazioni e configurazioni globali
│   ├── exclude          # File da ignorare (alternativa a .gitignore)
│   └── refs
├── logs/                # 📊 Cronologia delle operazioni
│   ├── HEAD
│   └── refs/
├── objects/             # 🗄️ Database degli oggetti Git
│   ├── info/
│   ├── pack/
│   ├── 00/
│   ├── 01/
│   └── ... (256 directory per hash SHA-1)
└── refs/                # 🔗 Reference a branch, tag e remote
    ├── heads/           # Branch locali
    ├── remotes/         # Branch remoti
    └── tags/            # Tag
```

---

## 📁 Componenti Principali

### 1. **HEAD** - Il Puntatore Corrente

```bash
$ cat .git/HEAD
ref: refs/heads/main

# Durante un checkout su commit specifico
$ cat .git/HEAD
a1b2c3d4e5f6789012345678901234567890abcd
```

**Funzione:**
- 📍 Indica su quale branch o commit ti trovi attualmente
- 🔄 Viene aggiornato automaticamente con `git checkout` e `git switch`

### 2. **config** - Configurazioni Locali

```bash
$ cat .git/config
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true

[user]
    name = Mario Rossi
    email = mario@example.com

[remote "origin"]
    url = https://github.com/user/repo.git
    fetch = +refs/heads/*:refs/remotes/origin/*

[branch "main"]
    remote = origin
    merge = refs/heads/main
```

### 3. **index** - Area di Staging

```bash
# Visualizzare il contenuto dell'index
$ git ls-files --stage
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0   README.md
100644 83baae61804e65cc73a7201a7252750c76066a30 0   index.html
```

**Caratteristiche:**
- 📋 Contiene snapshot dei file in staging
- 🔄 Viene aggiornato con `git add`
- 🗑️ Pulito dopo ogni commit

### 4. **objects/** - Database degli Oggetti

Git memorizza tutti i dati come oggetti:

#### 🎯 Tipi di Oggetti

**Blob (Binary Large Object):**
```bash
# Contenuto di un file
$ git cat-file -p a1b2c3d
Contenuto del file README.md
```

**Tree (Directory):**
```bash
# Struttura di una directory
$ git cat-file -p d4e5f6g
100644 blob a1b2c3d4    README.md
100644 blob e7f8g9h0    index.html
040000 tree i1j2k3l4    src/
```

**Commit:**
```bash
# Metadati del commit
$ git cat-file -p m5n6o7p
tree d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3
parent x4y5z6a7b8c9d0e1f2g3h4i5j6k7l8m9n0o1p2q3
author Mario Rossi <mario@example.com> 1609459200 +0100
committer Mario Rossi <mario@example.com> 1609459200 +0100

Initial commit: progetto website
```

### 5. **refs/** - Reference

```
refs/
├── heads/               # Branch locali
│   ├── main            # SHA-1 dell'ultimo commit su main
│   └── develop         # SHA-1 dell'ultimo commit su develop
├── remotes/            # Branch remoti
│   └── origin/
│       ├── main
│       └── develop
└── tags/               # Tag
    ├── v1.0.0
    └── v1.1.0
```

---

## 🔍 Esplorazione Pratica

### Analizzare un Repository Esistente

```bash
# Dimensione della cartella .git
$ du -sh .git
2.1M    .git

# Numero di oggetti
$ find .git/objects -type f | wc -l
156

# Branch disponibili
$ ls .git/refs/heads/
main  develop  feature-auth

# Ultimo commit di ogni branch
$ cat .git/refs/heads/main
a1b2c3d4e5f6789012345678901234567890abcd

$ cat .git/refs/heads/develop  
x7y8z9a0b1c2d3e4f5g6h7i8j9k0l1m2n3o4p5q6
```

### Ispezionare gli Hooks

```bash
$ ls .git/hooks/
applypatch-msg.sample     pre-applypatch.sample
commit-msg.sample         pre-commit.sample
post-update.sample        pre-push.sample
pre-rebase.sample         prepare-commit-msg.sample
update.sample

# Rendere eseguibile un hook
$ cp .git/hooks/pre-commit.sample .git/hooks/pre-commit
$ chmod +x .git/hooks/pre-commit
```

---

## 🛠️ Operazioni Avanzate

### Pulizia e Manutenzione

```bash
# Verificare integrità del repository
$ git fsck --full
Checking object directories: 100% done.
Checking objects: 100% done.

# Compattare oggetti per risparmiare spazio
$ git gc --aggressive
Counting objects: 2007, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (1978/1978), done.

# Verificare dimensioni prima e dopo
$ du -sh .git
1.8M    .git  # Prima
1.2M    .git  # Dopo gc
```

### Backup della Configurazione

```bash
# Backup della configurazione locale
$ cp .git/config .git/config.backup

# Backup completo del repository
$ tar -czf repository-backup.tar.gz .git/
```

---

## ⚠️ Cosa NON Toccare

### 🚫 File da NON Modificare Manualmente

- **objects/*** - Database degli oggetti (corrompe il repository)
- **index** - Area di staging (usa `git add/reset`)
- **HEAD** - Puntatore corrente (usa `git checkout/switch`)
- **packed-refs** - Reference compattate (usa comandi Git)

### ✅ File Sicuri da Modificare

- **config** - Configurazioni (meglio con `git config`)
- **description** - Descrizione del repository
- **hooks/*** - Script personalizzati
- **info/exclude** - File da ignorare

---

## 🔧 Troubleshooting

### Repository Corrotto

```bash
# Verificare problemi
$ git status
fatal: unable to read tree 89abcdef...

# Tentare riparazione
$ git fsck --full
$ git reflog expire --expire=now --all
$ git gc --prune=now --aggressive
```

### Recupero da Backup

```bash
# Se hai un backup
$ rm -rf .git
$ tar -xzf repository-backup.tar.gz

# Verificare integrità
$ git status
$ git log --oneline
```

---

## 🎯 Best Practices

### ✅ Raccomandazioni

- **🔍 Esplora senza modificare** per imparare
- **🔄 Fai backup** prima di operazioni rischiose
- **📊 Monitora dimensioni** con `git gc` periodico
- **🪝 Usa hooks** per automazione

### ❌ Evita

- **🚫 Modifica diretta** di files interni
- **🗑️ Eliminazione manuale** di oggetti
- **📝 Edit manuale** dell'index
- **🔧 Hack della configurazione** senza capire

---

## 🎯 Esercizio Pratico

**Esplora la struttura del tuo repository:**

```bash
# 1. Crea un repository di test
mkdir git-anatomy-test
cd git-anatomy-test
git init

# 2. Esplora la struttura iniziale
ls -la .git/
tree .git/ 2>/dev/null || find .git -type f

# 3. Aggiungi contenuto e osserva i cambiamenti
echo "Test file" > test.txt
git add test.txt

# 4. Verifica l'index
git ls-files --stage

# 5. Fai commit e osserva gli oggetti
git commit -m "Test commit"
find .git/objects -type f

# 6. Analizza gli oggetti creati
git cat-file -t $(find .git/objects -type f | head -1 | sed 's|.git/objects/||' | sed 's|/||')
```

---

## 🔗 Collegamenti Utili

- **📚 Prossima guida**: [03 - Stati dei File](./03-stati-file.md)
- **📖 Guida precedente**: [01 - Inizializzare Repository](./01-inizializzare-repository.md)
- **🎯 Esempi pratici**: [02 - Repository Documentazione](esempi/02-repository-documentazione.md)
