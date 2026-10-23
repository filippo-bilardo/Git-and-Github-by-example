# 01 - Installazione Git su Diversi Sistemi Operativi

## 🎯 Obiettivo

Imparare a installare Git sui principali sistemi operativi (Windows, macOS, Linux) e comprendere le differenze tra i metodi di installazione.

## 📚 Contenuti

### 1. Panoramica dei Metodi di Installazione

Git può essere installato in diversi modi:

#### 📦 **Metodi Principali**
- **Installer ufficiali** - Più semplici per principianti
- **Package manager** - Più flessibili per utenti avanzati
- **Compilazione da sorgente** - Massimo controllo

#### 🎯 **Scelta del Metodo**
- **Principianti**: Installer grafici ufficiali
- **Sviluppatori**: Package manager
- **Esperti**: Compilazione da sorgente

---

## 🪟 Installazione su Windows

### Percorso per utente non amministratore

Puoi installare Git nel tuo profilo personale, usare Git Bash e configurare il PATH utente senza modificare quello di sistema. Segui l'[esempio Windows senza amministratore](./esempi/05-setup-windows-senza-amministratore.md), che include PortableGit come alternativa e la configurazione di VS Code. Poi completa l'[esercizio con utente standard](./esercizi/05-installazione-windows-utente-standard.md).

### Metodo 1: Git for Windows (Raccomandato)

1. **Download**: Vai su [git-scm.com](https://git-scm.com)
2. **Esegui installer**: `Git-2.xx.x-64-bit.exe`

#### 🔧 **Opzioni Importanti durante l'Installazione**

```bash
✅ Selezioni Consigliate:
• Editor: "Use Visual Studio Code as Git's default editor"
• PATH: "Git from the command line and also from 3rd-party software"
• HTTPS: "Use the OpenSSL library"
• Line endings: "Checkout Windows-style, commit Unix-style line endings"
• Terminal: "Use MinTTY (the default terminal of MSYS2)"
• Credential helper: "Git Credential Manager"
```

#### 📦 **Cosa Include**
- **Git Bash** - Terminale Unix-like per Windows
- **Git GUI** - Interfaccia grafica
- **Git from Command Prompt** - Uso da CMD/PowerShell

### Metodo 2: Windows Package Manager (winget)

```powershell
# Da PowerShell (come amministratore)
winget install --id Git.Git -e --source winget
```

### Metodo 3: Chocolatey

```powershell
# Installa Chocolatey (se non presente)
# Poi installa Git
choco install git
```

---

## 🍎 Installazione su macOS

### Metodo 1: Homebrew (Raccomandato)

```bash
# Installa Homebrew (se non presente)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Installa Git
brew install git
```

### Metodo 2: Git Installer ufficiale

1. **Download**: [git-scm.com/download/mac](https://git-scm.com/download/mac)
2. **Esegui**: `git-2.xx.x-intel.dmg`

### Metodo 3: Xcode Command Line Tools

```bash
# Installa Xcode Command Line Tools (include Git)
xcode-select --install
```

#### ⚠️ **Nota per macOS**
- La versione da Xcode potrebbe essere datata
- Homebrew offre sempre l'ultima versione

---

## 🐧 Installazione su Linux

### Ubuntu/Debian

```bash
# Aggiorna repository
sudo apt update

# Installa Git
sudo apt install git-all

# Versione più recente (PPA)
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git
```

### CentOS/RHEL/Fedora

```bash
# CentOS/RHEL 7
sudo yum install git-all

# CentOS/RHEL 8+ / Fedora
sudo dnf install git-all
```

### Arch Linux

```bash
# Pacman
sudo pacman -S git

# AUR per versione sviluppo
yay -S git-git
```

### openSUSE

```bash
# Zypper
sudo zypper install git
```

---

## 🔧 Verifica Installazione

Dopo l'installazione, verifica che Git sia disponibile:

```bash
# Controlla versione
git --version

# Output atteso (esempio)
git version 2.40.0

# Controlla percorso installazione
which git    # Linux/macOS
where.exe git    # Windows, anche da PowerShell
```

### 🎯 **Versioni Consigliate**
- **Minima**: Git 2.25+ (supporto per tutte le funzionalità moderne)
- **Consigliata**: Git 2.35+ (miglioramenti performance e sicurezza)

---

## 🚨 Problemi Comuni e Soluzioni

### Windows

**Problema**: Git non riconosciuto nel prompt
```powershell
# Soluzione: Aggiungi al PATH
# Vai in: Sistema > Proprietà > Variabili d'ambiente
# Nel PATH utente aggiungi la sottocartella cmd dell'installazione effettiva.
# Esempio per installazione personale:
# C:\Users\Mario\AppData\Local\Programs\Git\cmd
# Per installazione di sistema: C:\Program Files\Git\cmd
# Riapri terminali e VS Code dopo la modifica.
```

**Problema**: Conflitti line endings
```bash
# Soluzione: Configura line endings
git config --global core.autocrlf true
```

### macOS

**Problema**: Versione datata da Xcode
```bash
# Soluzione: Usa Homebrew e forza il PATH
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

### Linux

**Problema**: Versione vecchia nei repository
```bash
# Ubuntu: Usa PPA ufficiale
sudo add-apt-repository ppa:git-core/ppa

# CentOS: Compila da sorgente o usa repository esterni
sudo yum groupinstall "Development Tools"
```

---

## 📋 Checklist Post-Installazione

- [ ] Git versione 2.25 o superiore installata
- [ ] Comando `git --version` funziona correttamente
- [ ] Git disponibile dal terminale/prompt
- [ ] (Windows) Git Bash disponibile
- [ ] PATH configurato correttamente

---

## 🔗 Prossimi Passi

✅ **Completato**: Installazione Git
🎯 **Prossimo**: [Configurazione Identità](./02-configurazione-identita.md)

---

## 📚 Risorse Aggiuntive

- [Documentazione Ufficiale Git](https://git-scm.com/doc)
- [Pro Git Book - Installazione](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Troubleshooting Git Installation](https://docs.github.com/en/get-started/quickstart/set-up-git)
