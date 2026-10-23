# 05 - Area di Staging

## 📖 Descrizione

L'area di staging è uno dei concetti fondamentali di Git che lo distingue da altri sistemi di controllo versione. Questa esercitazione ti insegnerà a padroneggiare questo potente strumento per controllo preciso dei tuoi commit.

## 🎯 Obiettivi di Apprendimento

Al termine di questa esercitazione sarai in grado di:

- ✅ Comprendere cos'è l'area di staging e perché è importante
- ✅ Distinguere tra working directory, staging area e repository
- ✅ Utilizzare `git add` in modo selettivo
- ✅ Gestire l'area di staging con `git reset`
- ✅ Fare commit parziali di file modificati
- ✅ Utilizzare `git add -p` per staging interattivo
- ✅ Visualizzare differenze tra aree diverse

## 📋 Prerequisiti

- **Conoscenza comandi base Git** (esercitazione precedente)
- **Repository Git attivo** con alcuni commit
- **Familiarità con modifiche ai file**

## ⏱️ Durata Stimata

**90-120 minuti** (teoria + pratica approfondita)

## 🎯 Risultato Finale

Padroneggerai l'area di staging per creare commit precisi e ben organizzati, migliorando significativamente la qualità della cronologia del tuo progetto.

![Staging Area Workflow](./esempi/immagini/staging-workflow.png)

## 📚 Indice degli Argomenti

### Guide Teoriche
1. [01 - Concetto di Staging Area](./01-concetto-staging.md)
2. [02 - Working Directory vs Staging vs Repository](./02-tre-aree-git.md)
3. [03 - Git Add Avanzato](./03-git-add-avanzato.md)
4. [04 - Git Reset e Staging](./04-git-reset-staging.md)
5. [05 - Staging Interattivo](./05-staging-interattivo.md)

### Esempi Pratici
1. [01 - Staging Selettivo](./esempi/01-staging-selettivo.md)
2. [02 - Commit Parziali](./esempi/02-commit-parziali.md)
3. [03 - Correzione Staging](./esempi/03-correzione-staging.md)
4. [04 - Workflow Complesso](./esempi/04-workflow-complesso.md)

### Esercizi di Consolidamento
1. [01 - Pratica Staging Base](./esercizi/01-pratica-staging-base.md)
2. [02 - Staging Interattivo](./esercizi/02-staging-interattivo.md)
3. [03 - Progetto Multi-File](./esercizi/03-progetto-multi-file.md)

## 🚀 Come Procedere

1. **Comprendi la teoria** delle tre aree di Git
2. **Pratica i comandi** con esempi graduali
3. **Sperimenta** con staging interattivo
4. **Applica** a un progetto reale

## 🔍 Punti Chiave da Ricordare

- L'area di staging ti permette controllo preciso sui commit
- `git add .` vs `git add -A` vs `git add -u` hanno comportamenti diversi
- `git reset` rimuove file dall'area di staging
- `git add -p` è potentissimo per commit selettivi

## 🆘 Problemi Comuni

- **File non desiderato nello staging**: Usa `git reset HEAD filename`
- **Commit troppo grandi**: Dividi usando staging selettivo
- **Modifiche miste**: Usa `git add -p` per separare

## 📚 Risorse Aggiuntive

- [Pro Git - Staging Area](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)
- [Interactive Staging](https://git-scm.com/book/en/v2/Git-Tools-Interactive-Staging)

## 🔄 Navigazione del Corso

- [📑 Indice](../README.md)
- [⬅️ 04-Comandi-Base-Git](../04-Comandi-Base-Git/README.md)
- [➡️ 06-Gestione-File-e-Directory](../06-Gestione-File-e-Directory/README.md)

---

**Prossimo passo**: [06-Gestione-File-e-Directory](../06-Gestione-File-e-Directory/README.md) - Gestione avanzata di file e cartelle
