# 06 - Git Submodules: Gestione Repository Inclusi

I **Git Submodules** permettono di includere un repository Git all'interno di un altro repository Git, mantenendo i due progetti separati ma collegati. È particolarmente utile per gestire dipendenze, librerie condivise, o componenti modulari.

### Cosa sono i Submodules

Un **submodule** è un repository Git completo che viene "montato" come una sottocartella in un altro repository (chiamato "superproject"). Ogni submodule mantiene la sua cronologia indipendente e può essere sviluppato separatamente.

```
Repository Principale (Superproject)
├── .git/
├── .gitmodules                    ← Configurazione submodules
├── src/
│   └── main.c
├── docs/
├── lib/                           ← Submodule 1
│   └── .git                       ← Repository separato
└── ui-components/                 ← Submodule 2
    └── .git                       ← Repository separato
```

### Vantaggi dei Submodules

- **Versioning Preciso**: Ogni submodule punta a un commit specifico
- **Sviluppo Separato**: Team diversi possono lavorare su moduli diversi
- **Riutilizzo**: Stessa libreria in progetti multipli
- **Controllo Dependencies**: Aggiornamenti controllati delle dipendenze

### Svantaggi e Limitazioni

- **Complessità**: Workflow più complesso
- **Sincronizzazione**: Richiede attenzione per mantenere tutto allineato
- **Learning Curve**: Curva di apprendimento più ripida
- **Tool Support**: Non tutti gli strumenti gestiscono bene i submodules

## 🏗️ Struttura e Funzionamento

### File .gitmodules

Il file `.gitmodules` contiene la configurazione di tutti i submodules:

```ini
[submodule "lib/auth"]
    path = lib/auth
    url = https://github.com/company/auth-library.git
    branch = main

[submodule "ui-components"]
    path = ui-components
    url = git@github.com:company/ui-components.git
    branch = develop
```

### Stato dei Submodules

I submodules possono essere in diversi stati:

- **Initialized**: Configurato ma non scaricato
- **Updated**: Sincronizzato con il commit specificato
- **Modified**: Ha modifiche locali non committate
- **Out of sync**: Punta a un commit diverso da quello nel superproject

## ⚙️ Comandi Fondamentali

### Aggiungere un Submodule

```bash
# Sintassi base
git submodule add <repository-url> <path>

# Esempi pratici
git submodule add https://github.com/company/auth-lib.git lib/auth
git submodule add git@github.com:company/ui-components.git components/ui

# Con branch specifico
git submodule add -b develop https://github.com/company/utils.git lib/utils

# Verifica aggiunta
git status
# new file:   .gitmodules
# new file:   lib/auth
```

### Clonare Repository con Submodules

```bash
# Metodo 1: Clone con submodules automatici
git clone --recursive https://github.com/company/main-project.git

# Metodo 2: Clone prima, poi inizializza submodules
git clone https://github.com/company/main-project.git
cd main-project
git submodule init
git submodule update

# Metodo 3: Command combinato
git clone https://github.com/company/main-project.git
cd main-project
git submodule update --init --recursive
```

### Aggiornare Submodules

```bash
# Aggiorna tutti i submodules al commit specificato nel superproject
git submodule update

# Aggiorna alle ultime versioni dei branch configurati
git submodule update --remote

# Aggiorna recursivamente (submodules di submodules)
git submodule update --remote --recursive

# Aggiorna un submodule specifico
git submodule update --remote lib/auth
```

### Lavorare all'interno dei Submodules

```bash
# Entra nel submodule
cd lib/auth

# Lavora normalmente con Git
git checkout main
git pull origin main
echo "fix bug" >> auth.c
git add auth.c
git commit -m "Fix authentication bug"
git push origin main

# Torna al superproject
cd ../..

# Il superproject vede il submodule come "modified"
git status
# modified:   lib/auth (new commits)

# Commit la nuova versione del submodule
git add lib/auth
git commit -m "Update auth library to latest version"
```

## 🔄 Workflow Completi

### Workflow 1: Sviluppo Coordinato

```bash
# 1. Setup iniziale del superproject
mkdir main-app && cd main-app
git init
echo "# Main Application" > README.md
git add README.md
git commit -m "Initial commit"

# 2. Aggiungi submodules per componenti
git submodule add https://github.com/company/auth-module.git modules/auth
git submodule add https://github.com/company/database-layer.git modules/db
git submodule add https://github.com/company/ui-framework.git modules/ui

# 3. Commit la configurazione
git add .gitmodules modules/
git commit -m "Add core application modules"

# 4. Push superproject
git remote add origin https://github.com/company/main-app.git
git push -u origin main
```

### Workflow 2: Team Collaboration

```bash
# Developer A: Lavora sul modulo auth
cd modules/auth
git checkout -b feature/two-factor-auth
# ... sviluppo ...
git push origin feature/two-factor-auth

# Developer B: Prende i cambiamenti
git submodule update --remote
cd modules/auth
git checkout feature/two-factor-auth
git pull origin feature/two-factor-auth
cd ../..

# Dopo merge della feature nel submodule
git submodule update --remote modules/auth
git add modules/auth
git commit -m "Update auth module with 2FA support"
```

### Workflow 3: Release Management

```bash
# 1. Prepara release dei submodules
cd modules/auth
git checkout main
git tag v2.1.0
git push origin v2.1.0
cd ../..

cd modules/ui
git checkout main  
git tag v1.5.0
git push origin v1.5.0
cd ../..

# 2. Aggiorna superproject alle versioni taggate
git submodule foreach 'git checkout main && git pull'
git add modules/
git commit -m "Update all modules to latest stable versions"
git tag v1.0.0
git push origin v1.0.0
```

## 🔧 Comandi Avanzati

### Operazioni su Tutti i Submodules

```bash
# Esegui comando in tutti i submodules
git submodule foreach 'git status'
git submodule foreach 'git checkout main'
git submodule foreach 'git pull origin main'

# Con condizioni
git submodule foreach 'git checkout main && git pull'

# Mostra informazioni sui submodules
git submodule status
git submodule summary
```

### Configurazione Avanzata

```bash
# Configura aggiornamento automatico
git config submodule.recurse true

# Configura strategia di merge per submodules
git config submodule.lib/auth.update merge

# Ignora modifiche in submodules specifici
git config submodule.lib/auth.ignore dirty

# Push automatico dei submodules
git config push.recurseSubmodules check  # Controlla se submodules sono pushati
git config push.recurseSubmodules on-demand  # Push automatico
```

### Rimozione Submodules

```bash
# 1. Rimuovi dal .gitmodules
git config --remove-section submodule.lib/auth

# 2. Rimuovi dalla configurazione Git
git config --remove-section submodule.lib/auth

# 3. Rimuovi dalla staging area
git rm --cached lib/auth

# 4. Rimuovi directory fisica
rm -rf lib/auth

# 5. Commit le modifiche
git add .gitmodules
git commit -m "Remove auth submodule"

# 6. Pulisci riferimenti residui
rm -rf .git/modules/lib/auth
```

## 🎯 Casi d'Uso Pratici

### Caso 1: Microservices Architecture

```bash
# Setup architettura microservices
mkdir ecommerce-platform && cd ecommerce-platform
git init

# Aggiungi servizi come submodules
git submodule add https://github.com/company/user-service.git services/users
git submodule add https://github.com/company/product-service.git services/products  
git submodule add https://github.com/company/order-service.git services/orders
git submodule add https://github.com/company/payment-service.git services/payments

# Aggiungi librerie condivise
git submodule add https://github.com/company/common-models.git shared/models
git submodule add https://github.com/company/auth-middleware.git shared/auth

# Struttura risultante:
# ecommerce-platform/
# ├── services/
# │   ├── users/
# │   ├── products/
# │   ├── orders/
# │   └── payments/
# └── shared/
#     ├── models/
#     └── auth/
```

### Caso 2: Libreria Condivisa

```bash
# Progetto Web App
mkdir web-app && cd web-app
git init
git submodule add https://github.com/company/ui-components.git src/components

# Progetto Mobile App
mkdir mobile-app && cd mobile-app  
git init
git submodule add https://github.com/company/ui-components.git lib/components

# Entrambi i progetti usano la stessa libreria UI
# Aggiornamenti nella libreria si riflettono in entrambi
```

### Caso 3: Documentation Website

```bash
# Website principale
mkdir company-docs && cd company-docs
git init

# Aggiungi documentazione dai vari progetti
git submodule add https://github.com/company/api-docs.git docs/api
git submodule add https://github.com/company/user-guides.git docs/guides  
git submodule add https://github.com/company/tutorials.git docs/tutorials

# Script di build che combina tutto
cat << 'EOF' > build.sh
#!/bin/bash
git submodule update --remote --recursive
# Genera sito statico combinando tutte le docs
mkdocs build
EOF
```

## ⚠️ Errori Comuni e Soluzioni

### 1. Submodule Non Inizializzato

```bash
# ❌ ERRORE: Directory vuota dopo clone
ls lib/auth
# Directory vuota

# ✅ SOLUZIONE: Inizializza submodules
git submodule update --init --recursive
```

### 2. Submodule in Stato "Detached HEAD"

```bash
# ❌ ERRORE: Modifiche in stato detached
cd lib/auth
git status
# HEAD detached at abc1234

# ✅ SOLUZIONE: Checkout su branch appropriato
git checkout main
# O crea nuovo branch per le modifiche
git checkout -b feature/my-changes abc1234
```

### 3. Conflitti durante Update

```bash
# ❌ ERRORE: Conflitti durante submodule update
git submodule update --remote
# error: Your local changes would be overwritten

# ✅ SOLUZIONE: Commit o stash modifiche prima
cd lib/auth
git stash
cd ..
git submodule update --remote
cd lib/auth
git stash pop
```

### 4. Submodule Punta a Commit Inesistente

```bash
# ❌ ERRORE: Commit non trovato
git submodule update
# fatal: reference is not a tree: abc1234

# ✅ SOLUZIONE: Aggiorna al branch HEAD
git submodule update --remote
git add lib/auth
git commit -m "Update submodule to latest commit"
```

## 💡 Best Practices

### 1. Versioning Strategy

```bash
# ✅ USA tag per release stabili
cd lib/auth
git tag v1.2.0
git push origin v1.2.0
cd ..

# Nel superproject, punta al tag
cd lib/auth
git checkout v1.2.0
cd ..
git add lib/auth
git commit -m "Pin auth library to v1.2.0"
```

### 2. Documentazione

```markdown
<!-- README.md nel superproject -->
## Submodules

Questo progetto usa i seguenti submodules:

- `lib/auth`: Libreria di autenticazione - [Repository](https://github.com/company/auth)
- `components/ui`: Componenti UI condivisi - [Repository](https://github.com/company/ui)

### Setup per Sviluppatori

```bash
git clone --recursive https://github.com/company/main-project.git
cd main-project
./setup.sh  # Script che configura tutto
```

### Aggiornamento Submodules

```bash
git submodule update --remote --recursive
git add .
git commit -m "Update all submodules"
```
```

### 3. Automation Scripts

```bash
# scripts/update-submodules.sh
#!/bin/bash
set -e

echo "🔄 Aggiornamento submodules..."

# Aggiorna tutti i submodules
git submodule update --remote --recursive

# Controlla se ci sono modifiche
if ! git diff-index --quiet HEAD --; then
    echo "📝 Submodules aggiornati, creando commit..."
    git add .
    git commit -m "chore: update submodules to latest versions"
    
    echo "✅ Submodules aggiornati con successo!"
else
    echo "ℹ️  Nessun aggiornamento necessario"
fi
```

### 4. CI/CD Integration

```yaml
# .github/workflows/test.yml
name: Test with Submodules

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
      with:
        submodules: recursive  # Importante!
        
    - name: Run tests
      run: |
        # Test del progetto principale
        npm test
        
        # Test dei submodules
        git submodule foreach 'npm test'
```

## 🧪 Quiz di Verifica

### Domanda 1
**Qual è la differenza principale tra submodules e copiare files da un altro repository?**

<details>
<summary>Risposta</summary>

Con i **submodules** mantieni il collegamento al repository originale e la sua cronologia Git completa. Puoi ricevere aggiornamenti e contribuire modifiche. Copiare files crea solo una snapshot senza cronologia o collegamento al progetto originale.
</details>

### Domanda 2
**Perché dopo `git clone` la directory del submodule è vuota?**

<details>
<summary>Risposta</summary>

Il clone standard scarica solo i metadati dei submodules (configurazione in `.gitmodules`). Devi usare `git clone --recursive` oppure dopo il clone eseguire `git submodule update --init --recursive` per scaricare il contenuto effettivo.
</details>

### Domanda 3
**Come aggiorno un submodule alla versione più recente del suo branch?**

<details>
<summary>Risposta</summary>

```bash
git submodule update --remote nome-submodule
# Oppure per tutti i submodules:
git submodule update --remote --recursive
```

Poi commit nel superproject per salvare la nuova versione:
```bash
git add nome-submodule
git commit -m "Update submodule to latest version"
```
</details>

### Domanda 4
**Cosa succede se modifico files dentro un submodule?**

<details>
<summary>Risposta</summary>

Il submodule diventa "modified" dal punto di vista del superproject. Devi:
1. Committare le modifiche nel submodule stesso
2. Nel superproject, fare `git add` del submodule modificato
3. Committare nel superproject per aggiornare il puntatore al nuovo commit
</details>

## 🛠️ Esercizio Pratico: Progetto Multi-Modulo

### Parte 1: Setup Base

```bash
# 1. Crea repository principale
mkdir webapp-multimodule && cd webapp-multimodule
git init
echo "# WebApp Multi-Module Project" > README.md
git add README.md
git commit -m "Initial commit"

# 2. Simula creazione di repositories per submodules
# (In realtà dovresti avere repository reali)
mkdir -p temp/auth-service && cd temp/auth-service
git init
echo "console.log('Auth Service v1.0');" > auth.js
echo "# Auth Service" > README.md
git add .
git commit -m "Initial auth service"
cd ../..

mkdir -p temp/ui-components && cd temp/ui-components  
git init
echo ".button { background: blue; }" > styles.css
echo "# UI Components Library" > README.md
git add .
git commit -m "Initial UI components"
cd ../..
```

### Parte 2: Aggiunta Submodules

```bash
# 3. Aggiungi submodules (usa path locali per esercizio)
git submodule add ./temp/auth-service modules/auth
git submodule add ./temp/ui-components modules/ui

# 4. Verifica struttura
tree -a
# .
# ├── .git/
# ├── .gitmodules
# ├── README.md
# ├── modules/
# │   ├── auth/
# │   │   ├── .git
# │   │   ├── auth.js
# │   │   └── README.md
# │   └── ui/
# │       ├── .git
# │       ├── styles.css
# │       └── README.md
# └── temp/

# 5. Commit configurazione
git add .gitmodules modules/
git commit -m "Add auth and UI submodules"
```

### Parte 3: Modifiche e Sincronizzazione

```bash
# 6. Modifica nel submodule auth
cd modules/auth
echo "console.log('Auth Service v1.1 - Added 2FA');" > auth.js
git add auth.js
git commit -m "Add two-factor authentication"
cd ../..

# 7. Il superproject vede la modifica
git status
# modified:   modules/auth (new commits)

# 8. Aggiorna superproject
git add modules/auth
git commit -m "Update auth service to v1.1"

# 9. Simula clone da parte di altro sviluppatore
cd ..
git clone webapp-multimodule webapp-clone
cd webapp-clone

# 10. Inizializza submodules nel clone
git submodule update --init --recursive

# 11. Verifica che tutto sia sincronizzato
cd modules/auth
cat auth.js
# Dovrebbe mostrare la versione v1.1
```

### Parte 4: Workflow Completo

```bash
# 12. Torna al progetto originale
cd ../../webapp-multimodule

# 13. Aggiorna tutti i submodules alle latest versions
git submodule update --remote --recursive

# 14. Crea script di utilità
cat << 'EOF' > scripts/update-all.sh
#!/bin/bash
echo "🔄 Updating all submodules..."
git submodule update --remote --recursive

echo "📊 Submodule status:"
git submodule status

echo "✅ Update complete!"
EOF

chmod +x scripts/update-all.sh

# 15. Test script
./scripts/update-all.sh

# 16. Documenta nel README
cat << 'EOF' >> README.md

## Submodules

- `modules/auth`: Authentication service
- `modules/ui`: Shared UI components

## Development Setup

```bash
git clone --recursive <repository-url>
cd <project-name>
./scripts/update-all.sh
```
EOF

git add scripts/ README.md
git commit -m "Add utility scripts and documentation"
```

## 🔗 Navigazione

**Precedente:** [05 - Branch Tracking](./05-branch-tracking.md)  
**Successivo:** [07 - Git Subtree](./07-git-subtree.md)  
**Torna all'Indice:** [README del Modulo](README.md)  
**Corso Principale:** [Git e GitHub by Example](../README.md)

## 📚 Risorse Aggiuntive

- [Git Submodules Documentation](https://git-scm.com/docs/git-submodule)
- [Pro Git Book - Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
- [Atlassian Submodules Tutorial](https://www.atlassian.com/git/tutorials/git-submodule)
- [GitHub Submodules Guide](https://github.blog/2016-02-01-working-with-submodules/)
