# 11 - Concetti di Branching

## 📖 Descrizione

Il branching è una delle funzionalità più potenti di Git. Questa esercitazione introduce i concetti fondamentali che ti permetteranno di lavorare su funzionalità parallele, sperimentare senza rischi, e collaborare efficacemente in team.

## 🎯 Obiettivi di Apprendimento

Al termine di questa esercitazione sarai in grado di:

- ✅ Comprendere cos'è un branch e perché è importante
- ✅ Visualizzare la struttura ad albero di Git
- ✅ Distinguere tra branch locali e remoti
- ✅ Comprendere il concetto di HEAD e puntatori
- ✅ Pianificare strategie di branching
- ✅ Identificare quando creare nuovi branch
- ✅ Comprendere i workflow di branching comuni

## 📋 Prerequisiti

- **Solida comprensione di commit e cronologia**
- **Familiarità con navigazione Git**
- **Repository con alcuni commit esistenti**

## ⏱️ Durata Stimata

**60-75 minuti** (teoria fondamentale + visualizzazioni)

## 🎯 Risultato Finale

Avrai una comprensione concettuale solida del branching che ti preparerà per implementazioni pratiche e strategie avanzate.

![Git Branching Concept](./esempi/immagini/git-branching-concept.png)

## 📚 Indice degli Argomenti

### Guide Teoriche
1. [01 - Concetti Fondamentali](./01-concetti-fondamentali.md)
2. [02 - Cos'è un Branch](./02-cos-e-branch.md)
3. [03 - Struttura ad Albero Git](./03-struttura-albero.md)
4. [04 - HEAD e Puntatori](./04-head-puntatori.md)
5. [05 - Branch Locali vs Remoti](./05-locali-vs-remoti.md)
6. [06 - Strategie di Branching](./06-strategie-branching.md)
7. [07 - Workflow Comuni](./07-workflow-comuni.md)

### Esempi Pratici
1. [01 - Visualizzazione Branch](./esempi/01-visualizzazione-branch.md)
2. [02 - Scenari di Branching](./esempi/02-scenari-branching.md)
3. [03 - Pianificazione Strategica](./esempi/03-pianificazione-strategica.md)
4. [04 - Team Workflow](./esempi/04-team-workflow.md)

### Esercizi di Consolidamento
1. [01 - Analisi Repository](./esercizi/01-analisi-repository.md)
2. [02 - Progettazione Branch](./esercizi/02-progettazione-branch.md)
3. [03 - Strategia Personale](./esercizi/03-strategia-personale.md)

## 🚀 Come Procedere

1. **Assimila i concetti teorici** fondamentali
2. **Visualizza repository esistenti** per vedere branching in azione
3. **Pianifica** la tua strategia di branching
4. **Prepara** i prossimi esercizi pratici

## 🔍 Punti Chiave da Ricordare

- Branch = puntatore mobile a un commit
- Git memorizza snapshot, non differenze
- Creare branch è istantaneo e "economico"
- HEAD punta al branch corrente
- Ogni branch ha la sua linea di sviluppo

## 💡 Vantaggi del Branching

### Sviluppo Parallelo
- Lavora su feature senza interferire con main
- Sperimenta senza rischi
- Mantieni versioni stabili separate

### Collaborazione Team
- Ogni sviluppatore ha il suo spazio
- Integrazione controllata
- Review del codice facilitata

### Gestione Release
- Branch per versioni diverse
- Hotfix separati da sviluppo
- Testing isolato

## 🏗️ Modelli di Branching Comuni

### 1. **GitHub Flow**
- `main` + feature branches
- Semplice e efficace

### 2. **Git Flow**
- `main`, `develop`, `feature/*`, `release/*`, `hotfix/*`
- Completo ma complesso

### 3. **GitLab Flow**
- Environment branches
- Deployment continuo

## 📚 Risorse Aggiuntive

- [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
- [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)
- [GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html)

## 🔄 Navigazione del Corso

- [📑 Indice](../README.md)
- [⬅️ 11-Annullare-Modifiche](../11-Annullare-Modifiche/README.md)
- [➡️ 13-Creare-e-Gestire-Branch](../13-Creare-e-Gestire-Branch/README.md)

---

**Prossimo passo**: [13-Creare-e-Gestire-Branch](../13-Creare-e-Gestire-Branch/README.md) - Implementazione pratica del branching
