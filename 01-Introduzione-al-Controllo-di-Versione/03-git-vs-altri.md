# 03 - Git vs Altri Sistemi di Controllo Versione

## 📖 Spiegazione Concettuale

Git non è l'unico sistema di controllo versione disponibile oggi. Comprendere le differenze con altri sistemi popolari ti aiuterà a capire perché Git è diventato lo standard de facto e quando potrebbe essere più appropriato usare alternative.

## 🏆 Panoramica dei Sistemi Attuali

### Sistemi Centralizzati
- **Subversion (SVN)** - Ancora usato in molte aziende
- **Perforce** - Popolare nell'industria dei videogames
- **Team Foundation Server (TFS)** - Ecosistema Microsoft

### Sistemi Distribuiti
- **Git** - Dominante nel mercato
- **Mercurial** - Alternativa più semplice
- **Bazaar** - Utilizzato principalmente da Canonical

## 🔍 Confronto Dettagliato: Git vs SVN

### Architettura Fondamentale

#### SVN (Centralizzato)
```
Repository Centrale (Server)
         ↓
    Working Copy (Client)
```

**Workflow SVN:**
1. Checkout dal server
2. Modifica locale
3. Commit diretto al server
4. Update per sincronizzare

#### Git (Distribuito)
```
Repository Remoto
         ↓
Repository Locale ← Working Directory
         ↓
    Staging Area
```

**Workflow Git:**
1. Clone completo repository
2. Modifica locale
3. Add to staging
4. Commit locale
5. Push al repository remoto

### Vantaggi e Svantaggi

| Aspetto | SVN | Git |
|---------|-----|-----|
| **Curva di Apprendimento** | ✅ Più semplice | ❌ Più complessa |
| **Velocità Operazioni** | ❌ Richiede rete | ✅ Locale veloce |
| **Branching** | ❌ Costoso | ✅ Istantaneo |
| **Merging** | ❌ Manuale spesso | ✅ Automatico intelligente |
| **Lavoro Offline** | ❌ Limitato | ✅ Completo |
| **Backup** | ❌ Single point failure | ✅ Ogni clone è backup |
| **File Binari Grandi** | ✅ Gestisce bene | ❌ Problemi storici |

## 🚀 Git vs Mercurial

Mercurial era il principale concorrente di Git nei primi anni 2000.

### Similarità
- Entrambi distribuiti
- Performance simili
- Supporto cross-platform
- Open source

### Differenze Chiave

#### Git
```bash
# Più potente ma più complesso
git rebase -i HEAD~3
git cherry-pick commit-hash
git reflog
```

#### Mercurial
```bash
# Più semplice e coerente
hg pull
hg update
hg commit
```

### Perché Git ha Vinto?

1. **Ecosistema**: GitHub ha cambiato tutto
2. **Flessibilità**: Git permette workflow più complessi
3. **Performance**: Marginalmente più veloce su operazioni complesse
4. **Adozione Early**: Progetti high-profile come Linux Kernel

## 🎮 Git vs Perforce

Perforce è ancora molto popolare nell'industria dei videogames.

### Perforce - Punti di Forza
- **File binari enormi**: Gestisce asset da GB senza problemi
- **Locking esclusivo**: Importante per asset non-mergeable
- **Performance con file grandi**: Ottimizzato per questa use case
- **Visual tools**: Interfacce grafiche molto mature

### Git - Svantaggi con Asset Grandi
```bash
# File da 500MB in Git = problemi
git clone big-game-repo  # Download di molti GB
git status              # Lento con migliaia di file grandi
```

### Soluzione: Git LFS
```bash
# Git Large File Storage per asset grandi
git lfs track "*.psd"
git lfs track "*.mp4"
git add .gitattributes
```

## 🏢 Git vs Team Foundation Server (TFS/Azure DevOps)

### TFS/Azure DevOps
- **Integrazione Microsoft**: Visual Studio, Azure, Office
- **ALM completo**: Work items, builds, testing, deploy
- **Git support**: Ora supporta Git come backend
- **Licensing model**: Spesso già pagato dalle aziende Microsoft

### Quando Preferire TFS
- Ecosistema completamente Microsoft
- Team non-tecnici (Project Managers, Designers)
- Aziende con heavy compliance requirements
- Integrazione con Active Directory necessaria

## 📊 Statistiche di Adozione (2024)

```
Git:           ~95% nuovi progetti
SVN:           ~3% (legacy principalmente)
Mercurial:     ~1%
Perforce:      ~1% (gaming/enterprise)
Altri:         <1%
```

### Settori per Sistema

| Settore | Sistema Preferito | Motivo |
|---------|------------------|--------|
| **Web Development** | Git | GitHub, workflow agile |
| **Mobile Apps** | Git | CI/CD pipelines |
| **Gaming** | Perforce/Git | Asset grandi |
| **Enterprise Legacy** | SVN/TFS | Sistemi esistenti |
| **Open Source** | Git | GitHub/GitLab |

## 💼 Casi d'Uso Specifici

### Quando Scegliere Git
✅ **Team distribuito geograficamente**
✅ **Progetti open source**
✅ **Sviluppo agile con branch frequenti**
✅ **CI/CD automation**
✅ **Progetti con code review intensive**

### Quando Considerare Alternative

#### SVN se:
- Team nuovo al version control
- Struttura aziendale molto gerarchica
- File binari grandi senza Git LFS
- Legacy systems integration

#### Perforce se:
- Asset binari enormi (gaming/multimedia)
- Workflow di locking necessari
- Performance critica con TB di dati
- Budget enterprise disponibile

#### Mercurial se:
- Team preferisce semplicità
- Workflow lineari principalmente
- Python-first environment

## ⚠️ Errori Comuni nella Scelta

### 1. **"Usiamo SVN perché è più semplice"**
❌ **Problema**: La semplicità apparente nasconde limitazioni severe
✅ **Soluzione**: Investi tempo nell'apprendimento Git - i benefici superano i costi

### 2. **"Git non funziona con file grandi"**  
❌ **Problema**: Informazione obsoleta
✅ **Soluzione**: Git LFS risolve questo problema efficacemente

### 3. **"Cambiare sistema costa troppo"**
❌ **Problema**: I costi di migrazione sembrano alti
✅ **Soluzione**: I benefici a lungo termine giustificano l'investimento

## 💡 Best Practices per la Migrazione

### Da SVN a Git

#### 1. **Migrazione Tecnica**
```bash
# Tool ufficiale per migrazione
git svn clone svn://svn.example.com/project
```

#### 2. **Migrazione Team**
- Training graduale
- Dual-running period
- Champion interni per supporto
- Documentazione workflow Git

#### 3. **Migrazione Workflow**
```
SVN Workflow → Git Workflow
─────────────────────────────
trunk         → main/master
branches      → feature branches
tags          → git tags
```

### Da Altri Sistemi

#### Mercurial → Git
```bash
# Tool di conversione
git clone hg::https://bitbucket.org/user/repo
```

#### Perforce → Git
- **Git P4**: Tool ufficiale per sincronizzazione
- **Gradual migration**: Start con Git mirrors
- **Selective migration**: Solo alcuni progetti inizialmente

## 🧠 Quiz di Autovalutazione

### Domanda 1
Qual è la principale differenza architetturale tra Git e SVN?
- A) Git è più veloce
- B) Git è distribuito, SVN è centralizzato
- C) Git ha più comandi
- D) Git costa meno

<details>
<summary>Risposta</summary>
<strong>B) Git è distribuito, SVN è centralizzato</strong><br>
Questa differenza architettuale influenza tutte le altre caratteristiche.
</details>

### Domanda 2
In quale scenario Perforce potrebbe essere preferibile a Git?
- A) Sviluppo web
- B) Progetti open source
- C) Gaming con asset da GB
- D) Team piccoli

<details>
<summary>Risposta</summary>
<strong>C) Gaming con asset da GB</strong><br>
Perforce è ottimizzato per gestire file binari molto grandi.
</details>

### Domanda 3
Perché Git ha superato Mercurial nonostante la semplicità di quest'ultimo?
- A) Git è più veloce
- B) L'ecosistema GitHub
- C) Git costa meno
- D) Git è più colorato

<details>
<summary>Risposta</summary>
<strong>B) L'ecosistema GitHub</strong><br>
GitHub ha reso Git lo standard de facto fornendo hosting e tools collaborativi.
</details>

## 🏋️ Esercizi Pratici

### Esercizio 1: Analisi Aziendale
Sei consulente per una azienda che deve scegliere un VCS. Analizza questi scenari:

**Scenario A**: Startup web con 5 sviluppatori remoti
- Sistema consigliato: ____________
- Motivo: ____________________

**Scenario B**: Studio gaming con asset 3D da 2GB ciascuno  
- Sistema consigliato: ____________
- Motivo: ____________________

**Scenario C**: Banca con sviluppo .NET enterprise
- Sistema consigliato: ____________
- Motivo: ____________________

### Esercizio 2: Migrazione Planning
Una azienda con 50 sviluppatori vuole migrare da SVN a Git. Crea un piano:

**Fase 1 (Settimana 1-2)**: ________________
**Fase 2 (Settimana 3-4)**: ________________  
**Fase 3 (Settimana 5-8)**: ________________

### Esercizio 3: Confronto Features
Compila questa tabella di confronto:

| Feature | Git | SVN | Mercurial | Perforce |
|---------|-----|-----|-----------|----------|
| **Branching** | _____ | _____ | _____ | _____ |
| **File Grandi** | _____ | _____ | _____ | _____ |
| **Semplicità** | _____ | _____ | _____ | _____ |
| **Performance** | _____ | _____ | _____ | _____ |

## 📖 Approfondimenti

### Confronti Dettagliati
- [Git vs SVN - Atlassian](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [Git vs Mercurial - Joel Spolsky](https://hginit.github.io/)
- [Perforce vs Git - Gaming Industry](https://www.perforce.com/blog/vcs/git-vs-perforce-version-control-gaming)

### Tool di Migrazione
- [git-svn documentation](https://git-scm.com/docs/git-svn)
- [GitHub Importer](https://github.com/github/git-sizer)
- [GitKraken Glo Migration Tools](https://www.gitkraken.com/)

## 🧭 Navigazione del Corso

- [📑 Indice](README.md)
- [⬅️ Storia e Evoluzione](02-storia-evoluzione.md)
- [➡️ Concetti Fondamentali](04-concetti-fondamentali.md)
