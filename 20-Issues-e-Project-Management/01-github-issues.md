# 01 - Introduzione alle GitHub Issues

## 📖 Spiegazione Concettuale

Le **GitHub Issues** sono uno strumento di tracciamento integrato per gestire bug, richieste di funzionalità, domande e qualsiasi tipo di discussione relativa a un progetto. Pensale come il "centro di controllo" per la comunicazione e l'organizzazione del lavoro.

## 🎯 Cosa Sono le Issues

### Definizione
Un **Issue** è un thread di discussione collegato a un repository che permette di:
- Segnalare bug e problemi
- Richiedere nuove funzionalità
- Porre domande al team
- Discutere implementazioni
- Organizzare il lavoro

### Anatomia di un Issue
```
┌─ Issue #42: Fix navigation bug ──────┐
│ 🏷️ bug, navigation, high-priority    │
│ 👤 Assigned to: @developer           │
│ 📋 Milestone: v2.1                   │
│ 📅 Created: 2 days ago               │
├───────────────────────────────────────┤
│ **Description**                       │
│ When clicking the navigation menu...  │
│                                       │
│ **Steps to reproduce**                │
│ 1. Open homepage                     │
│ 2. Click menu button                 │
│ 3. Notice error in console           │
│                                       │
│ **Expected behavior**                 │
│ Menu should open smoothly             │
│                                       │
│ **Screenshots**                       │
│ [attached screenshots]                │
├───────────────────────────────────────┤
│ 💬 Comments (3)                      │
│ @developer: I'll investigate this... │
│ @user: Same issue on mobile          │
│ @maintainer: Fixed in PR #43         │
└───────────────────────────────────────┘
```

## 🗂️ Tipi di Issues

### 🐛 Bug Reports
**Scopo**: Segnalare malfunzionamenti

**Template tipo**:
```markdown
## Bug Description
Brief description of the bug.

## Steps to Reproduce
1. Step one
2. Step two
3. Step three

## Expected Behavior
What should happen.

## Actual Behavior
What actually happens.

## Environment
- OS: [e.g., Windows 10]
- Browser: [e.g., Chrome 91]
- Version: [e.g., v1.2.3]

## Additional Context
Screenshots, logs, etc.
```

### ✨ Feature Requests
**Scopo**: Proporre nuove funzionalità

**Template tipo**:
```markdown
## Feature Summary
One-line summary of the feature.

## Problem Statement
What problem does this solve?

## Proposed Solution
Detailed description of the proposed feature.

## Alternatives Considered
Other solutions you've considered.

## Additional Context
Mockups, examples, etc.
```

### ❓ Questions
**Scopo**: Ottenere aiuto e chiarimenti

**Template tipo**:
```markdown
## Question
What would you like to know?

## Context
What are you trying to achieve?

## What I've Tried
Steps you've already taken.

## Additional Information
Relevant links, code snippets, etc.
```

### 📋 Tasks
**Scopo**: Organizzare lavoro e todo items

**Template tipo**:
```markdown
## Task Description
What needs to be done.

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Technical Notes
Implementation details.

## Dependencies
Related issues or PRs.
```

## 🏷️ Sistema di Labels

### Labels di Tipo
- `bug` 🐛 - Malfunzionamenti
- `enhancement` ✨ - Nuove funzionalità
- `question` ❓ - Domande e aiuto
- `documentation` 📚 - Relativo alla documentazione
- `duplicate` 👥 - Issue duplicato
- `invalid` ❌ - Issue non valido

### Labels di Priorità
- `priority: critical` 🔴 - Blocca il sistema
- `priority: high` 🟠 - Importante ma non critico
- `priority: medium` 🟡 - Priorità normale
- `priority: low` 🟢 - Può aspettare

### Labels di Difficoltà
- `good first issue` 🌱 - Perfetto per principianti
- `help wanted` 🙋 - Cerca contributori
- `easy` 😊 - Richiede poco tempo
- `hard` 😰 - Richiede esperienza

### Labels di Area
- `frontend` 🎨 - Interfaccia utente
- `backend` ⚙️ - Server e API
- `database` 🗄️ - Relativo al database
- `security` 🛡️ - Problemi di sicurezza
- `performance` ⚡ - Ottimizzazioni

## 👤 Gestione Assegnazioni

### Assignees
```
Chi può essere assegnato:
✅ Collaboratori del repository
✅ Owner e maintainer
❌ Utenti esterni (solo se invitati)

Casi d'uso:
- Assegnare lavoro specifico
- Indicare responsabilità
- Bilanciare carico di lavoro
```

### Self-Assignment
```
Scenari comuni:
1. "I'll take this" - Developer si auto-assegna
2. "Working on it" - Indica che è in corso
3. "Can I help?" - Richiesta di assignment
```

## 📅 Milestones

### Concetto
Le **Milestones** raggruppano issues verso un obiettivo comune (versione, sprint, deadline).

### Struttura Milestone
```
Milestone: Version 2.0 🎯
├─ Due date: December 31, 2024
├─ Progress: 12/20 issues closed (60%)
├─ Issues:
│  ├─ #45: User authentication ✅
│  ├─ #46: Password reset ✅  
│  ├─ #47: Email verification 🔄
│  └─ #48: Social login ⏳
└─ Description: Major release with auth features
```

### Best Practices Milestones
```
✅ DO:
- Obiettivi chiari e raggiungibili
- Date realistiche
- Issues correlate logicamente
- Revisione regolare del progresso

❌ DON'T:
- Troppi issues per milestone
- Date troppo rigide
- Milestone senza scopo chiaro
- Ignorare milestone scadute
```

## 🔄 Workflow del Ciclo di Vita

### Stati dell'Issue
```
1. 🆕 Open: Issue creato, in attesa di triaging
2. 🔍 Triaged: Review completata, pronto per lavoro
3. 🔄 In Progress: Qualcuno ci sta lavorando
4. 🔀 In Review: Soluzione proposta, in review
5. ✅ Closed: Risolto e completato
6. 🚫 Rejected: Chiuso senza implementazione
```

### Processo di Triaging
```
Fase 1: Initial Review
├─ Validare il problema
├─ Aggiungere labels appropriate
├─ Assegnare priorità
└─ Richiedere info aggiuntive se necessario

Fase 2: Planning
├─ Stimare effort required
├─ Assegnare a milestone
├─ Identificare dependencies
└─ Assegnare a developer

Fase 3: Implementation
├─ Developer inizia lavoro
├─ Aggiornamenti regolari nei commenti
├─ Link a PR quando ready
└─ Review e testing

Fase 4: Closure
├─ Verificare risoluzione
├─ Aggiornare documentazione
├─ Chiudere issue con summary
└─ Follow-up se necessario
```

## 💬 Best Practices per Commenti

### Comunicazione Efficace
```markdown
✅ Good Comment:
"I've identified the root cause in line 45 of auth.js. 
The token validation is failing when special characters 
are present. Working on a fix that escapes these 
characters properly. ETA: end of week."

❌ Poor Comment:
"Working on it"
```

### Tipi di Commenti Utili
- **Status updates**: Progresso del lavoro
- **Questions**: Chiarimenti necessari
- **Technical details**: Dettagli implementazione
- **Cross-references**: Link a PR/issues correlati
- **Test results**: Risultati di testing
- **Workarounds**: Soluzioni temporanee

## 🔗 Collegamenti e References

### Linking Issues
```markdown
# Riferimenti automatici
"This fixes #42"          # Chiude issue #42 quando PR merged
"Related to #15"          # Link senza chiusura automatica  
"Duplicate of #8"         # Indica duplicato
"Blocked by #23"          # Indica dipendenza

# Cross-repository
"Fixes user/repo#42"      # Issue in altro repository
"See microsoft/vscode#123" # Riferimento esterno
```

### Collegamento con PR
```markdown
# Nel PR description
"This PR addresses #42 by implementing..."

# Nell'issue
"Solution proposed in PR #87"

# Commit messages  
"fix: resolve navigation issue (closes #42)"
```

## 📊 Metriche e Analytics

### KPI Importanti
```
📈 Issue Metrics:
- Time to first response
- Time to resolution  
- Issue closure rate
- Backlog growth rate

👥 Community Metrics:
- New contributors via issues
- Community engagement level
- Question response quality
- Bug report quality
```

### GitHub Insights
```
Accessible via repository Insights tab:
- Issue activity over time
- Most active contributors  
- Response times
- Label usage statistics
```

## 🎯 Issues per Diversi Tipi di Progetto

### Open Source Project
```
Focus areas:
✅ Community engagement
✅ Contributor onboarding
✅ Clear contribution guidelines
✅ Good first issues
✅ Responsive maintainers
```

### Private Team Project
```
Focus areas:
✅ Sprint planning
✅ Bug tracking
✅ Feature requests
✅ Internal documentation
✅ Progress tracking
```

### Personal Project
```
Focus areas:
✅ Todo list management
✅ Feature planning
✅ Bug self-reporting
✅ Learning documentation
✅ Milestone tracking
```

## 🛠️ Template Configuration

### Issue Templates
GitHub permette di creare template predefiniti:

```yaml
# .github/ISSUE_TEMPLATE/bug_report.yml
name: Bug Report
description: File a bug report
title: "[Bug]: "
labels: ["bug", "triage"]
assignees:
  - maintainer-username
body:
  - type: markdown
    attributes:
      value: |
        Thanks for taking the time to fill out this bug report!
  - type: input
    id: summary
    attributes:
      label: Bug Summary
      description: A brief description of the bug
      placeholder: Tell us what you see!
    validations:
      required: true
```

## 🔮 Tendenze Future

### Automazione Issues
- **Auto-labeling** basato su contenuto
- **Smart assignment** basato su expertise
- **Predictive analytics** per prioritizzazione
- **Integration** con project management tools

### AI Integration
- **Automated responses** per FAQ comuni
- **Issue categorization** intelligente
- **Similar issue detection**
- **Resolution suggestions**

---

## 🎯 Punti Chiave da Ricordare

1. **Issues = Comunicazione**: Sono il centro della collaborazione
2. **Templates aiutano**: Strutturano informazioni utili
3. **Labels organizzano**: Facilitano filtraggio e ricerca
4. **Milestones pianificano**: Raggruppano lavoro verso obiettivi
5. **Commenti aggiornano**: Mantengono tutti informati
6. **References collegano**: Creano contesto tra elementi correlati

---

**Prossimo**: [Gestione Progetti con GitHub Projects](02-github-projects.md) | [Torna alle guide](README.md)
