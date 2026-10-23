# 08 - Visualizzare Storia Commit

## 📖 Descrizione

Imparare a navigare nella cronologia dei commit è essenziale per comprendere l'evoluzione del progetto, trovare bug, e collaborare efficacemente. Questa esercitazione ti insegnerà tutti i modi per esplorare la storia del tuo repository.

## 🎯 Obiettivi di Apprendimento

Al termine di questa esercitazione sarai in grado di:

- ✅ Utilizzare `git log` con varie opzioni di formattazione
- ✅ Filtrare la cronologia per autore, data, e contenuto
- ✅ Visualizzare modifiche specifiche con `git show`
- ✅ Creare alias per comandi log personalizzati
- ✅ Utilizzare strumenti grafici per visualizzare la cronologia
- ✅ Cercare commit specifici nella storia
- ✅ Comprendere il grafo della cronologia Git

## 📋 Prerequisiti

- **Repository Git con cronologia** (diversi commit)
- **Familiarità con comandi base Git**
- **Editor di testo** configurato

## ⏱️ Durata Stimata

**60-75 minuti** (esplorazione + personalizzazione)

## 🎯 Risultato Finale

Sarai in grado di navigare efficacemente nella cronologia di qualsiasi repository Git e trovare rapidamente le informazioni di cui hai bisogno.

![Git Log Visualization](./esempi/immagini/git-log-visualization.png)

## 📚 Indice degli Argomenti

### Guide Teoriche
1. [01 - Git Log Fondamentali](./01-git-log-fondamentali.md)
2. [02 - Opzioni di Formattazione](./02-opzioni-formattazione.md)
3. [03 - Filtri e Ricerche](./03-filtri-ricerche.md)
4. [04 - Git Show e Dettagli](./04-git-show-dettagli.md)
5. [05 - Alias e Personalizzazione](./05-alias-personalizzazione.md)
6. [06 - Strumenti Grafici](./06-strumenti-grafici.md)

### Esempi Pratici
1. [01 - Log Base e Formattazione](./esempi/01-log-base-formattazione.md)
2. [02 - Ricerca nella Cronologia](./esempi/02-ricerca-cronologia.md)
3. [03 - Analisi Modifiche](./esempi/03-analisi-modifiche.md)
4. [04 - Cronologia Visuale](./esempi/04-cronologia-visuale.md)

### Esercizi di Consolidamento
1. [01 - Esplorazione Repository](./esercizi/01-esplorazione-repository.md)
2. [02 - Detective Git](./esercizi/02-detective-git.md)
3. [03 - Personalizzazione Log](./esercizi/03-personalizzazione-log.md)
4. [04 - Investigazione Forense](./esercizi/04-forensic-investigation.md) ⭐⭐⭐⭐⭐

## 🚀 Come Procedere

1. **Impara i comandi base** di `git log`
2. **Sperimenta con formattazioni** diverse
3. **Pratica la ricerca** nella cronologia
4. **Personalizza** i tuoi alias preferiti

## 🔍 Punti Chiave da Ricordare

- `git log --oneline` per vista compatta
- `git log --graph` per visualizzare branch
- `git show` per dettagli di un commit specifico
- Filtri per autore: `git log --author="nome"`
- Ricerca nel contenuto: `git log --grep="pattern"`

## 🆘 Problemi Comuni

- **Output troppo lungo**: Usa `--oneline` o `--n` per limitare
- **Difficile leggere**: Prova `--graph --decorate --all`
- **Cercare modifiche**: Usa `git log -p` per vedere patch

## 📚 Risorse Aggiuntive

- [Git Log Documentation](https://git-scm.com/docs/git-log)
- [GitKraken - Visual Git Tool](https://www.gitkraken.com/)

## 🔄 Navigazione del Corso

- [📑 Indice](../README.md)
- [⬅️ 07-Gitignore-e-File-Tracking](../07-Gitignore-e-File-Tracking/README.md)
- [➡️ 10-Navigare-tra-Commit](../10-Navigare-tra-Commit/README.md)

---

**Prossimo passo**: [10-Navigare-tra-Commit](../10-Navigare-tra-Commit/README.md) - Spostarsi nella cronologia Git
