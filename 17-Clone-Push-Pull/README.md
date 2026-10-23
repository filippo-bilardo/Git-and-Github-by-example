# 17 - Clone Push Pull

## 📖 Descrizione

I comandi fondamentali per sincronizzare repository locali e remoti. Questa esercitazione ti insegnerà a clonare progetti esistenti, inviare le tue modifiche, e ricevere aggiornamenti da collaboratori.

## 🎯 Obiettivi di Apprendimento

Al termine di questa esercitazione sarai in grado di:

- ✅ Clonare repository da GitHub con `git clone`
- ✅ Configurare remote con `git remote`
- ✅ Inviare modifiche con `git push`
- ✅ Ricevere aggiornamenti con `git pull` e `git fetch`
- ✅ Gestire branch remoti
- ✅ Risolvere conflitti durante pull
- ✅ Utilizzare `git push --set-upstream`
- ✅ Comprendere origin e upstream
- ✅ Implementare Git Submodules per progetti modulari
- ✅ Utilizzare Git Subtree per integrare repository esterni
- ✅ Scegliere tra submodules e subtree in base al caso d'uso

## 📋 Prerequisiti

- **Account GitHub configurato** (esercitazione precedente)
- **Repository Git locale** con commit
- **Autenticazione SSH** funzionante

## ⏱️ Durata Stimata

**120-180 minuti** (pratica con repository remoti, submoduli e subtree)

## 🎯 Risultato Finale

Padroneggerai la sincronizzazione tra repository locali e remoti, base essenziale per qualsiasi collaborazione con Git.

## 📚 Indice degli Argomenti

### Guide Teoriche
1. [01 - Git Clone](./01-git-clone.md)
2. [02 - Remote Repository](./02-remote-repository.md)
3. [03 - Git Push](./03-git-push.md)
4. [04 - Git Pull vs Fetch](./04-pull-vs-fetch.md)
5. [05 - Branch Tracking](./05-branch-tracking.md)
6. [06 - Git Submodules](./06-git-submodules.md)
7. [07 - Git Subtree](./07-git-subtree.md)

### Esempi Pratici
1. [01 - Clone e Setup](./esempi/01-clone-setup.md)
2. [02 - Push Workflow](./esempi/02-push-workflow.md)
3. [03 - Pull e Sync](./esempi/03-pull-sync.md)
4. [04 - Remote Management](./esempi/04-remote-management.md)
5. [05 - Submodules Example](./esempi/05-submodules-example.md)
6. [06 - Subtree Example](./esempi/06-subtree-example.md)

### Strumenti di Supporto
- [📋 Script di Setup Automatico](./esempi/setup-examples.sh)
- [👨‍🏫 Guida per l'Istruttore](./esempi/instructor-guide.md)
4. [04 - Remote Management](./esempi/04-remote-management.md)

### Esercizi di Consolidamento
1. [01 - Repository Sync](./esercizi/01-repository-sync.md)
2. [02 - Collaboration Basics](./esercizi/02-collaboration-basics.md)
3. [03 - Advanced Workflow Scenarios](./esercizi/03-advanced-workflow-scenarios.md)

## 🚀 Come Procedere

1. **Pratica clone** con repository pubblici
2. **Crea repository** su GitHub e collegalo
3. **Sperimenta push/pull** con modifiche
4. **Simula collaborazione** con branch multipli

## 🔍 Comandi Essenziali

```bash
# Clone
git clone <url>                    # Clona repository
git clone <url> <directory>        # Clona in directory specifica

# Remote
git remote -v                      # Mostra remote configurati
git remote add origin <url>        # Aggiungi remote
git remote set-url origin <url>    # Cambia URL remote

# Push
git push origin main               # Push su branch main
git push -u origin feature-branch # Push e set tracking
git push --set-upstream origin new-branch

# Pull/Fetch
git pull origin main               # Pull da main
git fetch origin                   # Fetch senza merge
git pull --rebase                  # Pull con rebase
```

## 🔄 Navigazione del Corso

- [📑 Indice](../README.md)
- [⬅️ 16-Introduzione-GitHub](../16-Introduzione-GitHub/README.md)
- [➡️ 18-Collaborazione-Base](../18-Collaborazione-Base/README.md)
