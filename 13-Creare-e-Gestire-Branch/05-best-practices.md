# 05 - Best Practices per Branch

## 📖 Principi Fondamentali

Le **best practices per il branching** sono linee guida che aiutano i team a mantenere un repository organizzato, una storia git pulita e un workflow efficiente. Seguire queste pratiche previene problemi comuni e migliora la collaborazione.

### Filosofia del Branching

```
🎯 Un branch = Una responsabilità
🏷️ Nomi descrittivi = Comunicazione chiara
🧹 Cleanup regolare = Repository pulito
🔄 Workflow coerente = Team produttivo
```

## 🏷️ Convenzioni di Naming

### Pattern Raccomandati

```bash
# Feature branches
feature/user-authentication
feature/payment-integration
feature/email-notifications
feature/admin-dashboard

# Bug fixes
bugfix/login-validation-error
bugfix/payment-timeout-issue
bugfix/mobile-responsive-header

# Hotfixes (urgenti)
hotfix/security-vulnerability
hotfix/critical-performance-issue
hotfix/data-corruption-fix

# Release branches
release/v1.2.0
release/v2.0.0-beta
release/2024-q1-launch

# Experimental/Spike
spike/performance-investigation
experiment/new-architecture
poc/machine-learning-integration
```

### Struttura Gerarchica

```bash
# Per progetti grandi, usa namespace
frontend/feature/user-profile
backend/feature/api-refactor
mobile/bugfix/crash-on-startup
docs/improvement/api-documentation

# Per sviluppatori specifici (brevi esperimenti)
dev/mario/performance-test
dev/sara/ui-experiment
```

## 🔄 Workflow Patterns

### Git Flow (Progetti con Release Pianificate)

```bash
# Branch permanenti
main        # Produzione stabile
develop     # Integrazione sviluppo

# Branch temporanei
feature/*   # Nuove feature da develop
release/*   # Preparazione release da develop
hotfix/*    # Fix urgenti da main

# Esempio workflow
git switch develop
git switch -c feature/user-profile
# ... sviluppo ...
git switch develop
git merge feature/user-profile
git branch -d feature/user-profile
```

### GitHub Flow (Deployment Continuo)

```bash
# Branch principale
main        # Sempre deployabile

# Pattern semplice
git switch main
git pull origin main
git switch -c feature/new-feature
# ... sviluppo e test ...
# Pull request → Review → Merge → Deploy

# Esempio pratico
git switch main
git switch -c feature/shopping-cart
echo "Cart component" > cart.js
git add . && git commit -m "Add shopping cart component"
git push -u origin feature/shopping-cart
# Crea Pull Request su GitHub
```

### Feature Branch Workflow

```bash
# Ogni feature in branch separato
git switch main
git pull origin main
git switch -c feature/user-notifications

# Sviluppo isolato
echo "Notification system" > notifications.js
git add . && git commit -m "Implement notification system"
git push -u origin feature/user-notifications

# Merge quando pronto
git switch main
git merge feature/user-notifications
git push origin main
git branch -d feature/user-notifications
git push origin --delete feature/user-notifications
```

## 📏 Dimensione e Durata Branch

### Branch di Dimensione Ottimale

```bash
# ✅ Branch piccoli e focalizzati
feature/add-login-button        # 1-3 giorni, 5-10 commits
bugfix/fix-email-validation     # 1 giorno, 1-3 commits
hotfix/patch-security-issue     # Ore, 1-2 commits

# ❌ Branch troppo grandi
feature/complete-user-system    # Settimane, 50+ commits
```

### Gestione Branch Long-Running

```bash
# Per feature complesse, suddividi
feature/payment-system-base     # Infrastruttura base
feature/payment-system-ui       # Interfaccia utente
feature/payment-system-api      # API integration

# Oppure usa feature flags
git switch -c feature/new-dashboard
echo "if (FEATURE_FLAGS.newDashboard) {" > dashboard.js
echo "  // nuovo codice" >> dashboard.js
echo "}" >> dashboard.js
```

## 🔀 Strategie di Merge

### Merge Commit (Preserva Storia)

```bash
# Mantiene storia completa del branch
git switch main
git merge --no-ff feature/user-profile
# Crea merge commit anche per fast-forward

# Risultato nella storia:
# *   a1b2c3d Merge branch 'feature/user-profile'
# |\
# | * 9x8y7z6 Add profile validation
# | * 5u6i7o8 Add profile form
# |/
# * 2a3b4c5 Update main branch
```

### Squash Merge (Storia Lineare)

```bash
# Combina tutti i commits del branch in uno
git switch main
git merge --squash feature/user-profile
git commit -m "Add complete user profile feature"

# Risultato nella storia:
# * a1b2c3d Add complete user profile feature
# * 2a3b4c5 Update main branch
```

### Rebase (Storia Lineare Preservando Commits)

```bash
# Riproduce commits del branch su main aggiornato
git switch feature/user-profile
git rebase main
git switch main
git merge feature/user-profile  # Fast-forward

# Risultato nella storia:
# * 9x8y7z6 Add profile validation
# * 5u6i7o8 Add profile form
# * 2a3b4c5 Update main branch (linear)
```

## 🧹 Gestione e Cleanup

### Cleanup Automatico Branch Merged

```bash
# Script per cleanup branch locali mergiate
cleanup_merged_branches() {
    git branch --merged main | \
    grep -v "\* main" | \
    grep -v "main" | \
    xargs -n 1 git branch -d
}

# Usa come alias Git
git config --global alias.cleanup '!git branch --merged main | grep -v "\* main" | grep -v "main" | xargs -n 1 git branch -d'

# Uso: git cleanup
```

### Cleanup Branch Remoti

```bash
# Script completo di cleanup
#!/bin/bash
echo "🧹 Starting branch cleanup..."

# 1. Fetch latest state
git fetch --prune

# 2. Delete merged local branches
echo "Cleaning local merged branches..."
git branch --merged main | grep -v "\* main" | grep -v "main" | xargs -n 1 git branch -d

# 3. Show unmerged branches for manual review
echo "Unmerged branches requiring manual review:"
git branch --no-merged main

echo "✅ Cleanup completed!"
```

### Archiviazione Branch Importanti

```bash
# Prima di cancellare branch importanti, crea tag
git tag archive/feature-important-experiment feature-important-experiment
git branch -D feature-important-experiment

# Recupera in futuro se necessario
git switch -c recovered-feature archive/feature-important-experiment
```

## 👥 Collaborazione Team

### Branch Protection Rules

```bash
# Configurazioni consigliate per main branch:
# - Require pull request reviews (1-2 reviewers)
# - Require status checks to pass
# - Require branches to be up to date
# - Require linear history (optional)
# - Restrict pushes to main branch
```

### Code Review Process

```bash
# 1. Sviluppatore crea branch e PR
git switch -c feature/user-dashboard
# ... sviluppo ...
git push -u origin feature/user-dashboard
# Crea Pull Request

# 2. Review process
# - Code review da team members
# - Automated tests pass
# - Approval da lead developer

# 3. Merge strategy coerente
# Squash merge per feature piccole
# Merge commit per feature documentate
# Rebase per mantenere storia lineare
```

### Comunicazione Branch

```bash
# Branch temporanei con informazioni
git switch -c wip/mario/experiment-$(date +%Y%m%d)
echo "Experiment: Testing new user flow" > .branch-info

# Commit messages descrittivi
git commit -m "feat: add user dashboard component

- Implement responsive layout
- Add data visualization charts
- Include user preference settings

Closes #123, References #124"
```

## 🚀 Performance e Ottimizzazione

### Branch Leggeri

```bash
# Evita di includere file grandi nei branch feature
# Usa .gitignore per build artifacts
echo "dist/" >> .gitignore
echo "node_modules/" >> .gitignore
echo "*.log" >> .gitignore

# Branch per documentazione separati da codice
git switch -c docs/api-documentation
# Solo modifiche a documentazione
```

### Ottimizzazione Repository

```bash
# Cleanup periodico del repository
git gc --aggressive --prune=now

# Verifica dimensione repository
git count-objects -vH

# Trova file grandi nella storia
git rev-list --objects --all | \
  git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | \
  sed -n 's/^blob //p' | \
  sort --numeric-sort --key=2 | \
  tail -20
```

## 📊 Monitoring e Analisi

### Branch Analytics

```bash
# Script per analisi branch attivi
#!/bin/bash
echo "📊 Branch Analysis Report"
echo "========================"

echo "Active branches:"
git branch -a | wc -l

echo "Branches by author:"
git for-each-ref --format='%(authorname)' refs/heads | sort | uniq -c | sort -nr

echo "Oldest unmerged branches:"
git for-each-ref --sort=committerdate refs/heads --format='%(refname:short) %(committerdate)'

echo "Branch sizes (commits ahead of main):"
git branch | while read branch; do
    if [ "$branch" != "* main" ] && [ "$branch" != "main" ]; then
        count=$(git rev-list --count main..$branch 2>/dev/null || echo "0")
        echo "$branch: $count commits"
    fi
done
```

### Health Check Repository

```bash
# Script per verifica salute repository
#!/bin/bash
echo "🏥 Repository Health Check"
echo "=========================="

# Verifica branch orfani
echo "Checking for orphaned branches..."
git fsck --unreachable

# Verifica integrità
echo "Checking repository integrity..."
git fsck

# Verifica configurazione
echo "Remote configuration:"
git remote -v

echo "Branch tracking status:"
git branch -vv

echo "✅ Health check completed!"
```

## 🛡️ Sicurezza Branch

### Protezione Informazioni Sensibili

```bash
# Verifica che branch non contengano secrets
# Usa tools come git-secrets
git secrets --scan

# Pre-commit hook per validazione
#!/bin/bash
# .git/hooks/pre-commit
if git diff --cached --name-only | grep -q "\.env$"; then
    echo "🚫 Cannot commit .env files!"
    exit 1
fi

# Verifica API keys nei commit
if git diff --cached | grep -qE "(api[_-]?key|secret|password|token).*="; then
    echo "🚫 Possible secret detected in commit!"
    exit 1
fi
```

### Backup e Recovery

```bash
# Backup branch critici prima di operazioni rischiose
git tag backup/feature-critical-$(date +%Y%m%d) feature-critical

# Recovery da backup
git switch -c recovery-branch backup/feature-critical-20241201

# Backup completo dello stato repository
git bundle create repository-backup-$(date +%Y%m%d).bundle --all
```

## 📋 Checklist Best Practices

### ✅ Prima di Creare Branch

- [ ] Pull latest main: `git pull origin main`
- [ ] Nome branch descrittivo e seguire convenzioni
- [ ] Branch focalizzato su single responsibility
- [ ] Verifica che feature/bug non sia già in sviluppo

### ✅ Durante Sviluppo

- [ ] Commit frequenti con messaggi chiari
- [ ] Test delle modifiche localmente
- [ ] Rebase/merge main periodicamente per grandi feature
- [ ] Push regolare per backup

### ✅ Prima del Merge

- [ ] Code review completato
- [ ] Test passed (automated + manual)
- [ ] Documentazione aggiornata
- [ ] Branch up-to-date con main
- [ ] Conflicts risolti

### ✅ Dopo il Merge

- [ ] Branch locale cancellato: `git branch -d feature-name`
- [ ] Branch remoto cancellato: `git push origin --delete feature-name`
- [ ] Deploy verificato (se applicabile)
- [ ] Issue/ticket chiuso

## 📚 Risorse Aggiuntive

- [Git Flow](https://nvie.com/posts/a-successful-git-branching-model/)
- [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html)

---

## 🔄 Navigazione

- [⬅️ 04 - Branch Remoti](04-branch-remoti.md)
- [➡️ 06 - Troubleshooting](06-troubleshooting.md)
- [🏠 README](README.md)

---

*Prossimo: Risolveremo i problemi comuni nel lavoro con i branch*
