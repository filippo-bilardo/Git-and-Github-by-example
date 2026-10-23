# 01 - Cos'è GitHub e Come Funziona

## 📖 Spiegazione Concettuale

**GitHub** è una piattaforma di hosting per repository Git basata su cloud che aggiunge funzionalità collaborative e di gestione progetti sopra al sistema di controllo versione Git. Pensalo come "Git + Collaboration + Project Management + Social Coding".

### Git vs GitHub

| Git | GitHub |
|-----|--------|
| Sistema di controllo versione | Piattaforma di hosting |
| Locale sul tuo computer | Nel cloud |
| Command line / GUI tools | Interfaccia web + API |
| Gestisce versioni del codice | Aggiunge collaborazione |

### GitHub come "Social Network per Programmatori"

```
Repository → Post del blog
Star → Like
Fork → Condivisione
Pull Request → Commento collaborativo
Issues → Discussioni
Followers → Network professionale
```

## 🌐 Architettura GitHub

### Struttura Base
```
GitHub.com
├── Account Personale
│   ├── Repository Pubblici
│   ├── Repository Privati
│   ├── Gists (snippet di codice)
│   └── Profilo Pubblico
├── Organizations
│   ├── Team Management
│   ├── Repository Aziendali
│   └── Permissions & Security
└── GitHub Enterprise
    ├── Self-hosted
    └── Cloud privato
```

### Componenti Principali

#### 1. **Repository**
- Container per il progetto
- Include codice, documentazione, history
- Pubblico o privato
- Collaboratori e permessi

#### 2. **Issues**
- Sistema di ticket per bug/feature
- Discussioni strutturate
- Assegnazioni e milestone
- Labels per organizzazione

#### 3. **Pull Requests**
- Proposta di modifiche
- Code review integrato
- Discussioni su righe specifiche
- Merge/approval workflow

#### 4. **Actions**
- CI/CD integrato
- Automazione workflow
- Building e testing automatico
- Deploy automatizzato

#### 5. **Projects**
- Kanban boards
- Issue tracking avanzato
- Milestone e roadmap
- Team collaboration

## 💡 Casi d'Uso Pratici

### Scenario 1: Sviluppatore Solo
```
Portfolio Personale
├── 📁 portfolio-website (pubblico)
├── 📁 learning-python (pubblico)
├── 📁 personal-finance-app (privato)
└── 📄 README profilo (presentazione)

Benefici:
✅ Backup automatico nel cloud
✅ Portfolio visibile ai recruiter
✅ Storico completo del lavoro
✅ Accesso da qualsiasi dispositivo
```

### Scenario 2: Team Aziendale
```
Azienda: TechCorp
├── 🏢 Organization "TechCorp"
│   ├── 👥 Team Frontend (3 sviluppatori)
│   ├── 👥 Team Backend (4 sviluppatori)
│   └── 👥 Team DevOps (2 specialisti)
├── 📁 website-frontend (React)
├── 📁 api-backend (Node.js)
├── 📁 mobile-app (React Native)
└── 📁 infrastructure (Terraform)

Workflow:
1. Issues per planning sprint
2. Feature branch per sviluppo
3. Pull Request per review
4. Actions per CI/CD
5. Projects per tracking progress
```

### Scenario 3: Progetto Open Source
```
Progetto: awesome-web-framework
├── 🌟 1.2k Stars (popolarità)
├── 🍴 340 Forks (contributi)
├── 📝 45 Issues aperte (bug/feature)
├── 🔄 12 Pull Request (contributi pending)
├── 📊 Contributors da tutto il mondo
└── 📖 Documentation completa

Community Management:
- Issue templates per bug report
- PR templates per contributi
- Code of conduct
- Contributing guidelines
```

### Scenario 4: Studente/Apprendimento
```
Percorso di Apprendimento
├── 📚 Corsi completati
│   ├── html-css-basics ⭐ (pubblico)
│   ├── javascript-fundamentals ⭐
│   └── react-projects ⭐
├── 🔄 Fork di progetti interessanti
├── ⭐ Star per repository utili
└── 👥 Following esperti del settore

Benefits per la carriera:
- Dimostra costanza nello studio
- Mostra progressi nel tempo
- Network con altri sviluppatori
- Visibilità per opportunità lavorative
```

## 🔧 Funzionalità Avanzate GitHub

### 1. **GitHub Pages**
```bash
# Hosting gratuito per siti statici
repository-name.github.io
# Automatic deploy da repository
# Perfetto per documentazione, portfolio, blog
```

### 2. **GitHub Actions**
```yaml
# .github/workflows/ci.yml
name: CI/CD Pipeline
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Setup Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '16'
    - run: npm install
    - run: npm test
```

### 3. **GitHub Codespaces**
```
Development Environment nel Browser
├── VS Code nel cloud
├── Environment pre-configurato
├── Accesso da qualsiasi dispositivo
└── Computing power di GitHub
```

### 4. **GitHub Security**
```
Security Features
├── 🔒 Dependabot (aggiornamenti sicurezza)
├── 🛡️ Security Advisories
├── 🔍 Code Scanning (vulnerabilità)
├── 🔐 Secret Scanning
└── 📋 Security Tab per overview
```

### 5. **GitHub Discussions**
```
Community Features
├── 💬 Discussions (forum del progetto)
├── 🎯 Q&A structured
├── 💡 Ideas e feedback
└── 📢 Announcements
```

## 🌟 Ecosistema GitHub

### Integrazioni Popolari
```
Development Tools
├── 🔗 VS Code (GitHub extension)
├── 🔗 JetBrains IDEs
├── 🔗 Slack/Discord notifications
├── 🔗 Jira/Asana project management
└── 🔗 Heroku/Vercel deployment

Third-party Services
├── 📊 Code Climate (quality analysis)
├── 🔍 SonarQube (code analysis)
├── 📈 Codecov (test coverage)
└── 🚀 CircleCI (CI/CD alternative)
```

### GitHub API
```javascript
// Esempio: Fetch repository info
const response = await fetch('https://api.github.com/repos/owner/repo');
const repoData = await response.json();

console.log(`Repository: ${repoData.name}`);
console.log(`Stars: ${repoData.stargazers_count}`);
console.log(`Language: ${repoData.language}`);
```

## ⚠️ Errori Comuni per Principianti

### 1. **Confondere Git e GitHub**
```bash
# ❌ ERRORE: "Installo GitHub"
# Git è il tool, GitHub è la piattaforma

# ✅ CORRETTO: "Installo Git e uso GitHub"
git --version  # Verifica Git installato
# GitHub è accessibile via browser
```

### 2. **Repository Pubblico con Dati Sensibili**
```bash
# ❌ PERICOLOSO: Dati sensibili in repo pubblico
git add .env  # File con password/API keys
git commit -m "Add configuration"
git push origin main  # Ora è pubblico!

# ✅ SICURO: Usa .gitignore
echo ".env" >> .gitignore
echo "config/secrets.json" >> .gitignore
```

### 3. **Commit Direttamente su Main**
```bash
# ❌ CATTIVA PRATICA: Commit diretti su main
git checkout main
git add feature.js
git commit -m "New feature"
git push origin main

# ✅ BUONA PRATICA: Use feature branches
git checkout -b feature/new-functionality
git add feature.js
git commit -m "Add new functionality"
git push origin feature/new-functionality
# Then create Pull Request
```

### 4. **Non Leggere la Documentazione**
```markdown
# ❌ Ignorare README.md, CONTRIBUTING.md
# ✅ Sempre leggere la documentazione prima di contribuire

Files importanti:
- README.md (overview progetto)
- CONTRIBUTING.md (come contribuire)
- CODE_OF_CONDUCT.md (regole community)
- LICENSE (termini di utilizzo)
```

## 🎯 Best Practices GitHub

### 1. **Profilo Professionale**
```markdown
# README del profilo (username/username/README.md)
# 👋 Hi, I'm @username

## 🚀 About Me
- 🔭 I'm currently working on [Project Name]
- 🌱 I'm currently learning React and Node.js
- 👯 I'm looking to collaborate on open source projects
- 📫 How to reach me: email@example.com

## 🛠️ Technologies & Tools
![JavaScript](https://img.shields.io/badge/-JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![React](https://img.shields.io/badge/-React-61DAFB?style=flat&logo=react&logoColor=black)
![Node.js](https://img.shields.io/badge/-Node.js-339933?style=flat&logo=node.js&logoColor=white)

## 📊 GitHub Stats
![Your GitHub stats](https://github-readme-stats.vercel.app/api?username=username&show_icons=true)
```

### 2. **Repository Documentation**
```markdown
# README.md template per progetti
# Project Name

Brief description of what this project does.

## 🚀 Quick Start
```bash
npm install
npm start
```

## 📋 Features
- [ ] Feature 1
- [x] Feature 2 (completed)
- [ ] Feature 3

## 🤝 Contributing
See [CONTRIBUTING.md](CONTRIBUTING.md)

## 📄 License
MIT License - see [LICENSE](LICENSE)
```

### 3. **Issue Templates**
```markdown
<!-- .github/ISSUE_TEMPLATE/bug_report.md -->
**Describe the bug**
A clear description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Go to '...'
2. Click on '...'
3. See error

**Expected behavior**
What you expected to happen.

**Screenshots**
If applicable, add screenshots.

**Environment:**
- OS: [e.g. iOS]
- Browser: [e.g. chrome, safari]
- Version: [e.g. 22]
```

### 4. **Pull Request Template**
```markdown
<!-- .github/PULL_REQUEST_TEMPLATE.md -->
## Description
Brief description of changes made.

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Tests pass locally
- [ ] I have added tests for my changes
- [ ] All new and existing tests pass

## Checklist
- [ ] My code follows the project's style guidelines
- [ ] I have performed a self-review
- [ ] I have commented my code where necessary
```

## 🧪 Quiz di Autovalutazione

**1. Qual è la differenza principale tra Git e GitHub?**
- a) Sono la stessa cosa
- b) Git è locale, GitHub è nel cloud con funzionalità collaborative
- c) GitHub è più veloce di Git
- d) Git è gratuito, GitHub è a pagamento

**2. Cosa sono le GitHub Actions?**
- a) Un editor di codice
- b) Un sistema di CI/CD integrato
- c) Un modo per organizzare i file
- d) Un social network

**3. Quando dovresti usare un repository privato?**
- a) Mai, tutto dovrebbe essere pubblico
- b) Solo per progetti aziendali/personali sensibili
- c) Sempre, è più sicuro
- d) Solo se hai molti collaboratori

**4. Cos'è un Fork su GitHub?**
- a) Un errore nel codice
- b) Una copia del repository nel tuo account
- c) Un branch speciale
- d) Un tipo di commit

<details>
<summary>🔍 Risposte</summary>

1. **b)** Git è locale, GitHub è nel cloud con funzionalità collaborative
2. **b)** Un sistema di CI/CD integrato
3. **b)** Solo per progetti aziendali/personali sensibili
4. **b)** Una copia del repository nel tuo account

</details>

## 💻 Esercizi Pratici

### Esercizio 1: Esplora GitHub
1. Visita github.com e esplora alcuni repository popolari
2. Guarda le sezioni: Code, Issues, Pull Requests, Actions
3. Identifica pattern comuni nei README.md

### Esercizio 2: Analizza un Progetto Open Source
1. Trova un progetto open source interessante
2. Leggi il README.md e CONTRIBUTING.md
3. Guarda alcune Issues e Pull Request
4. Nota come è organizzata la community

### Esercizio 3: Pianifica il Tuo Profilo
1. Pensa a come vorresti presentarti su GitHub
2. Elenca progetti che vorresti mostrare
3. Progetta la struttura del tuo README profilo

## 🔗 Collegamenti Rapidi

- **Guida successiva**: [02 - Creare Account e Setup](02-setup-account.md)
- **Modulo precedente**: [14 - Risoluzione Conflitti](../../14-Risoluzione-Conflitti/README.md)

## Navigazione del Corso
- [📑 Indice](README.md)
- [⬅️ 14-Risoluzione-Conflitti](../../14-Risoluzione-Conflitti/README.md)
- [➡️ 16-Clone-Push-Pull](../../16-Clone-Push-Pull/README.md)
