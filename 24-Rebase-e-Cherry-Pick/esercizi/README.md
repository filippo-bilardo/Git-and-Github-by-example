# Esercizi Pratici - Rebase e Cherry-Pick

Questa sezione contiene esercizi pratici per masterizzare le tecniche avanzate di Git relative a rebase e cherry-pick. Gli esercizi sono ordinati per difficoltà crescente e coprono scenari reali di sviluppo software.

## 📚 Indice degli Esercizi

### 🟢 Livello Base
- **[Esercizio 1: Rebase di Base](01-basic-rebase-exercise.md)**
  - Scenario semplice di rebase lineare
  - Sincronizzazione branch feature con main
  - Gestione base dei conflitti
  - **Durata stimata:** 30-45 minuti
  - **Prerequisiti:** Conoscenza base di Git (commit, branch, merge)

### 🟡 Livello Intermedio  
- **[Esercizio 2: Interactive Rebase e Cleanup](02-interactive-cleanup-exercise.md)**
  - Uso completo dell'interactive rebase
  - Operazioni: squash, fixup, reword, edit, drop
  - Pulizia cronologia di sviluppo disordinata
  - **Durata stimata:** 60-90 minuti
  - **Prerequisiti:** Completamento Esercizio 1

- **[Esercizio 3: Cherry-Pick Mastery](03-cherry-pick-mastery-exercise.md)**
  - Cherry-pick in ambiente multi-versione
  - Gestione hotfix e backporting
  - Cherry-pick di range e risoluzione conflitti
  - **Durata stimata:** 75-120 minuti
  - **Prerequisiti:** Completamento Esercizi 1-2

### 🔴 Livello Avanzato
- **[Esercizio 4: Rebase vs Merge - Scenario Decisionale](04-rebase-vs-merge-decision-exercise.md)**
  - Analisi comparativa rebase vs merge
  - Sviluppo multi-developer simulation
  - Creazione policy di team
  - **Durata stimata:** 120-180 minuti  
  - **Prerequisiti:** Completamento di tutti gli esercizi precedenti

- **[Esercizio 5: Risoluzione Avanzata di Conflitti](05-advanced-conflict-resolution-exercise.md)**
  - Gestione conflitti complessi durante rebase
  - Integrazione sistemi paralleli con conflitti a cascata
  - Recovery da operazioni fallite
  - **Durata stimata:** 45-60 minuti
  - **Prerequisiti:** Completamento Esercizi 1-4

## 🎯 Obiettivi di Apprendimento

Al completamento di tutti gli esercizi, sarai in grado di:

### Competenze Tecniche
- ✅ Eseguire rebase semplici e interattivi con sicurezza
- ✅ Utilizzare cherry-pick per scenari complessi di backporting
- ✅ Risolvere conflitti durante operazioni di rebase/cherry-pick
- ✅ Scegliere tra rebase e merge in base al contesto
- ✅ Implementare workflow di cleanup professionale
- ✅ Gestire cronologie di branch complesse

### Competenze Strategiche  
- ✅ Sviluppare policy Git per team di sviluppatori
- ✅ Pianificare strategie di branching e merging
- ✅ Gestire release e hotfix in ambiente multi-versione
- ✅ Ottimizzare workflow per code review e CI/CD

## 🛠️ Setup dell'Ambiente

### Prerequisiti Sistema
```bash
# Verifica versione Git (minima: 2.20)
git --version

# Configura editor preferito (opzionale)
git config --global core.editor "code --wait"  # VS Code
# oppure
git config --global core.editor "vim"          # Vim

# Configura merge tool (opzionale) 
git config --global merge.tool vimdiff
```

### Configurazione per gli Esercizi
```bash
# Crea directory di lavoro
mkdir git-rebase-exercises
cd git-rebase-exercises

# Configurazione base per gli esercizi
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Alias utili per gli esercizi
git config --global alias.lg "log --oneline --graph --all"
git config --global alias.st "status --short"
git config --global alias.co "checkout"
git config --global alias.br "branch"
```

## 📊 Percorso di Apprendimento Consigliato

### Per Principianti
1. **Settimana 1:** Esercizio 1 (Rebase di Base)
   - Familiarizzazione con concetti fondamentali
   - Pratica risoluzione conflitti semplici

2. **Settimana 2:** Esercizio 2 (Interactive Cleanup)  
   - Apprendimento interactive rebase
   - Sviluppo best practices di cleanup

3. **Settimana 3:** Esercizio 3 (Cherry-Pick)
   - Gestione scenari multi-versione
   - Tecniche di backporting selettivo

4. **Settimana 4:** Esercizio 4 (Decision Making)
   - Integrazione conoscenze acquisite
   - Sviluppo capacità decisionali

### Per Sviluppatori Esperti
- **Giornata intensiva:** Tutti gli esercizi in sequenza
- **Focus specifico:** Salta al livello di complessità appropriato
- **Approfondimento:** Completa tutti i bonus challenge

## 🔍 Troubleshooting Comune

### Problemi Frequenti e Soluzioni

**🚨 "Conflitti durante rebase"**
```bash
# Risolvi manualmente i conflitti, poi:
git add .
git rebase --continue

# Per abbandonare il rebase:
git rebase --abort
```

**🚨 "Ho fatto rebase ma voglio tornare indietro"**
```bash
# Usa reflog per trovare lo stato precedente
git reflog
git reset --hard HEAD@{n}
```

**🚨 "Cherry-pick non funziona"**
```bash
# Verifica che il commit esista
git log --oneline --all | grep "pattern"

# Cherry-pick con strategia di merge specifica
git cherry-pick -X theirs <commit-hash>
```

**🚨 "Cronologia troppo complessa"**
```bash
# Visualizza con tool grafico
git log --oneline --graph --all
gitk --all  # Se disponibile
```

## 📈 Valutazione e Autoverifica

### Checklist di Completamento

**Esercizio 1:**
- [ ] Rebase completato senza errori
- [ ] Cronologia lineare ottenuta
- [ ] Conflitti risolti correttamente
- [ ] Comprensione differenza rebase vs merge

**Esercizio 2:**
- [ ] Tutte le operazioni interactive utilizzate
- [ ] Cronologia pulita e professionale
- [ ] Messaggi commit migliorati
- [ ] Workflow di cleanup automatizzato

**Esercizio 3:**
- [ ] Cherry-pick multi-branch eseguiti
- [ ] Hotfix applicati correttamente
- [ ] Conflitti complessi risolti
- [ ] Strategie di backporting implementate

**Esercizio 4:**
- [ ] Analisi comparativa completata
- [ ] Policy di team definita
- [ ] Scenari decisionali testati
- [ ] Raccomandazioni documentate

### Quiz di Autovalutazione

1. **Quando useresti rebase invece di merge?**
2. **Come gestiresti un hotfix critico su multiple versioni?**
3. **Qual è il rischio principale del rebase di commit pubblici?**
4. **Come sceglieresti tra squash e fixup in interactive rebase?**

## 🎉 Progetti Avanzati Post-Esercizi

Dopo aver completato tutti gli esercizi, considera questi progetti:

1. **Automazione Workflow Git**
   - Script per rebase automatico con test
   - Hook pre-commit per validazione
   - Integration con CI/CD pipeline

2. **Tool di Team Management**
   - Dashboard per monitoring branch status
   - Automated branch cleanup
   - Policy enforcement automation

3. **Git Training Program**
   - Creazione materiale formativo per team
   - Workshop interattivi
   - Assessment e certificazione

## 📚 Risorse Aggiuntive

### Guide di Riferimento
- [Rebase Fundamentals](../01-rebase-fundamentals.md)
- [Interactive Rebase](../02-interactive-rebase.md)  
- [Cherry-Pick Guide](../03-cherry-pick-guide.md)
- [Rebase vs Merge](../04-rebase-vs-merge.md)

### Esempi Pratici
- [Simple Rebase Example](../esempi/01-simple-rebase.md)
- [Interactive Cleanup Example](../esempi/02-interactive-cleanup.md)

### Documentazione Esterna
- [Git Official Documentation](https://git-scm.com/docs)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)
- [Pro Git Book](https://git-scm.com/book)

---

## 🤝 Contributi e Feedback

Se trovi errori, hai suggerimenti per miglioramenti, o vuoi contribuire con nuovi esercizi:

1. **Segnala Issues:** Descrivi problemi o ambiguità trovate
2. **Proponi Miglioramenti:** Suggerisci scenari aggiuntivi o chiarimenti
3. **Condividi Esperienza:** Racconta come gli esercizi ti hanno aiutato nel lavoro reale

**Buon apprendimento e happy coding! 🚀**
