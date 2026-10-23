# 13 - Merge e Strategie

## 📖 Descrizione

Il merge è il processo di unificazione del lavoro da branch diversi. Questa esercitazione ti insegnerà le diverse strategie di merge, quando usarle, e come gestire l'integrazione del codice in modo pulito ed efficace.

## 🎯 Obiettivi di Apprendimento

Al termine di questa esercitazione sarai in grado di:

- ✅ Comprendere i tipi di merge: fast-forward, recursive, squash
- ✅ Eseguire merge con `git merge`
- ✅ Scegliere la strategia di merge appropriata
- ✅ Utilizzare `git merge --no-ff` per preservare cronologia
- ✅ Implementare squash merge per cronologia pulita
- ✅ Gestire merge commit con messaggi appropriati
- ✅ Comprendere quando NON fare merge
- ✅ Preparare branch per merge puliti

## 📋 Prerequisiti

- **Padronanza gestione branch** (esercitazione precedente)
- **Repository con branch multipli**
- **Comprensione cronologia Git**

## ⏱️ Durata Stimata

**90-120 minuti** (teoria + pratica estrategie diverse)

## 🎯 Risultato Finale

Saprai gestire merge complessi e scegliere la strategia appropriata per mantenere una cronologia Git pulita e comprensibile.

![Merge Strategies](./esempi/immagini/merge-strategies.png)

## 📚 Indice degli Argomenti

### Guide Teoriche
1. [01 - Tipi di Merge](./01-tipi-merge.md)
2. [02 - Fast-Forward Merge](./02-fast-forward.md)
3. [03 - Recursive Merge](./03-recursive-merge.md)
4. [04 - Squash Merge](./04-squash-merge.md)
5. [05 - Merge vs Rebase](./05-merge-vs-rebase.md)
6. [06 - Strategie Avanzate](./06-strategie-avanzate.md)

### Esempi Pratici
1. [01 - Merge Semplice](./esempi/01-merge-semplice.md)
2. [02 - Feature Integration](./esempi/02-feature-integration.md)
3. [03 - Release Preparation](./esempi/03-release-preparation.md)
4. [04 - Hotfix Merge](./esempi/04-hotfix-merge.md)

### Esercizi di Consolidamento
1. [01 - Merge Workflow](./esercizi/01-merge-workflow.md)
2. [02 - Strategy Selection](./esercizi/02-strategy-selection.md)
3. [03 - Complex Integration](./esercizi/03-complex-integration.md)

## 🚀 Come Procedere

1. **Comprendi le strategie** teoricamente
2. **Pratica ogni tipo** di merge separatamente
3. **Sperimenta con repository** di test
4. **Applica a workflow** realistici

## 🔍 Tipi di Merge

### 1. **Fast-Forward Merge**
```bash
git merge feature-branch
# Nessun merge commit se lineare
```

### 2. **No Fast-Forward**
```bash
git merge --no-ff feature-branch
# Sempre crea merge commit
```

### 3. **Squash Merge**
```bash
git merge --squash feature-branch
git commit -m "Add complete feature"
# Tutti i commit diventano uno
```

## 🔍 Punti Chiave da Ricordare

- Fast-forward: cronologia lineare, no merge commit
- Recursive: merge commit mostra convergenza
- Squash: cronologia pulita, perde dettaglio
- `--no-ff` preserva struttura branch
- Messaggi merge commit dovrebbero essere informativi

## 📊 Quando Usare Ogni Strategia

### Fast-Forward
- ✅ Hotfix semplici
- ✅ Aggiornamenti lineari
- ❌ Feature complesse

### No Fast-Forward
- ✅ Feature development
- ✅ Cronologia branch importante
- ✅ Code review workflow

### Squash Merge
- ✅ Feature con commit "sporchi"
- ✅ Cronologia principale pulita
- ❌ Quando serve dettaglio sviluppo

## 🆘 Problemi Comuni

- **Merge non necessario**: Controlla se fast-forward possibile
- **Cronologia confusa**: Usa `--no-ff` per chiarezza
- **Troppi merge commit**: Considera squash o rebase
- **Merge commit vuoto**: Assicurati ci siano differenze

## 💡 Best Practices

### Preparazione Merge
1. **Aggiorna target branch** prima del merge
2. **Testa il branch** completamente
3. **Pulisci commit** se necessario
4. **Scrivi messaggio** descrittivo

### Messaggio Merge Commit
```
Merge branch 'feature/user-authentication'

* Add login/logout functionality
* Implement password reset
* Add user session management

Closes #123
```

## ⚠️ Avvertenze

- Non fare merge di branch non testati
- Sempre backup prima di merge complessi
- Considera rebase per cronologia più pulita
- Coordina con team su strategia merge

## 📚 Risorse Aggiuntive

- [Git Merge Documentation](https://git-scm.com/docs/git-merge)
- [Atlassian - Git Merge Strategies](https://www.atlassian.com/git/tutorials/using-branches/git-merge)

## 🔄 Navigazione del Corso

- [📑 Indice](../README.md)
- [⬅️ 13-Creare-e-Gestire-Branch](../13-Creare-e-Gestire-Branch/README.md)
- [➡️ 15-Risoluzione-Conflitti](../15-Risoluzione-Conflitti/README.md)

---

**Prossimo passo**: [15-Risoluzione-Conflitti](../15-Risoluzione-Conflitti/README.md) - Gestire conflitti durante il merge
