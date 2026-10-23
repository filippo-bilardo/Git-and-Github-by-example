# 02 - Storia e Evoluzione del Controllo di Versione

## 📖 Spiegazione Concettuale

La storia del controllo di versione riflette l'evoluzione dello sviluppo software, dalle soluzioni rudimentali ai sistemi distribuiti moderni. Comprendere questa evoluzione ci aiuta ad apprezzare le caratteristiche innovative di Git.

## 🕰️ Timeline Storica

### 1970s - Gli Inizi: SCCS
**Source Code Control System (SCCS)**
- Primo sistema di controllo versione commerciale
- Sviluppato da Bell Labs
- Solo un utente alla volta poteva modificare un file
- Sistema completamente locale

```
Limitazioni:
❌ Un solo utente per file
❌ Nessuna collaborazione
❌ Solo sistemi Unix
```

### 1980s - Evoluzione: RCS  
**Revision Control System (RCS)**
- Miglioramento di SCCS
- Introdotto il concetto di "lock" dei file
- Più efficiente nella gestione delle versioni

```
Miglioramenti:
✅ Gestione più efficiente
✅ Migliore interfaccia utente
❌ Ancora limitato alla collaborazione
```

### 1990s - Era Centralizzata: CVS
**Concurrent Versions System (CVS)**
- Primo sistema veramente collaborativo
- Server centrale con repository
- Múltipli sviluppatori possono lavorare contemporaneamente

```
Caratteristiche CVS:
✅ Collaborazione multi-utente
✅ Repository centrale
✅ Branching (limitato)
❌ Problemi con file binari
❌ Operazioni atomiche limitate
```

### 2000s - Maturità: Subversion (SVN)
**Apache Subversion**
- Successore diretto di CVS
- Risolve molti problemi di CVS
- Diventa lo standard industriale

```
Miglioramenti SVN:
✅ Operazioni atomiche
✅ Migliore gestione file binari
✅ Rinominazione e spostamento file
✅ Metadata dei file
❌ Ancora centralizzato
❌ Problemi di performance con repository grandi
```

### 2005 - Rivoluzione: Git
**Git - Distributed Version Control**
- Creato da Linus Torvalds per Linux Kernel
- Cambia completamente il paradigma
- Sistema distribuito e decentralizzato

## 🏗️ Architetture a Confronto

### Sistema Centralizzato (CVS, SVN)
```
    [Sviluppatore A] ←→ [Server Centrale] ←→ [Sviluppatore B]
                          ↑
                     [Repository Unico]
                          ↓
                     [Sviluppatore C]
```

**Problemi:**
- Single point of failure
- Necessaria connessione di rete
- Operazioni lente
- Difficile lavorare offline

### Sistema Distribuito (Git)
```
[Repository A] ←→ [Repository Centrale] ←→ [Repository B]
     ↑                    ↑                      ↑
[Sviluppatore A]    [Repository C]        [Sviluppatore B]
                         ↑
                 [Sviluppatore C]
```

**Vantaggi:**
- Ogni repository è completo
- Lavoro offline completo
- Backup naturale
- Flessibilità nelle strategie di merge

## 🐧 La Storia di Git

### Prima di Git: lo Sviluppo del Kernel Linux

Nei primi anni del progetto Linux, dal 1991 al 2002, gli sviluppatori si scambiavano modifiche sotto forma di **patch**, cioè file che descrivono le differenze da applicare al codice. Coordinare questi contributi diventava più difficile con la crescita del progetto.

Nel **2002**, il progetto iniziò a usare **BitKeeper**, un sistema di controllo di versione distribuito ma proprietario. Nel **2005**, i rapporti tra la comunità Linux e l'azienda produttrice si interruppero e venne meno la possibilità di usarlo gratuitamente. Questa situazione spinse Linus Torvalds, creatore del kernel Linux, a sviluppare un nuovo strumento. [Fonte: Pro Git, breve storia di Git](https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git).

### Aprile 2005: Nasce Git

Torvalds cercava un sistema veloce, distribuito e adatto a un progetto grande, con molti rami di sviluppo paralleli. Le esigenze del kernel orientarono quindi il progetto di Git fin dall'inizio. [Fonte: obiettivi iniziali di Git](https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git).

Il **7 aprile 2005**, Torvalds registrò il primo commit del repository di Git. La prima implementazione era essenziale, ma permetteva già di registrare la propria storia: Git veniva usato per sviluppare Git stesso. Il sistema nacque quindi da un problema concreto di collaborazione, prima di diventare uno strumento utilizzato anche fuori dal mondo Linux. [Fonte: intervista a Linus Torvalds per i vent'anni di Git](https://github.blog/open-source/git/git-turns-20-a-qa-with-linus-torvalds/).

### Luglio-Dicembre 2005: da Torvalds alla Comunità

Altri sviluppatori contribuirono presto al progetto. Tra questi c'era **Junio C. Hamano**, al quale Torvalds affidò il ruolo di **maintainer il 26 luglio 2005**. Il maintainer coordina lo sviluppo, valuta i contributi e prepara le nuove versioni.

Il **21 dicembre 2005** venne pubblicato **Git 1.0**. In pochi mesi, lo strumento creato per rispondere alle esigenze di Linux era diventato un progetto con una propria comunità e un percorso di sviluppo autonomo. [Fonte: ricostruzione storica di Patrick Steinhardt, sviluppatore di Git](https://about.gitlab.com/blog/journey-through-gits-20-year-history/).

### 2008: il Lancio di GitHub

Il **10 aprile 2008** venne lanciato pubblicamente **GitHub**, un servizio per ospitare repository Git e collaborare sul codice attraverso il web. Git esisteva già da tre anni: GitHub costruì una piattaforma attorno allo strumento di controllo di versione. [Fonte: annuncio originale del lancio di GitHub](https://github.blog/news-insights/we-launched/).

Per esempio, uno studente può creare commit nel proprio repository locale senza collegarsi a GitHub; può poi pubblicarli su un repository remoto per condividerli con i compagni. Questa possibilità deriva dall'architettura distribuita di Git.

### Le Tappe da Ricordare

| Anno o data | Evento |
|-------------|--------|
| **2002** | Il progetto Linux inizia a usare BitKeeper |
| **7 aprile 2005** | Primo commit di Git, creato da Linus Torvalds |
| **26 luglio 2005** | Junio C. Hamano assume il ruolo di maintainer |
| **21 dicembre 2005** | Pubblicazione di Git 1.0 |
| **10 aprile 2008** | Lancio pubblico di GitHub |

## 🚀 L'Innovazione di Git

### Dalle Esigenze di Linux alle Caratteristiche di Git

Le scelte progettuali rispondono ai problemi incontrati nello sviluppo del kernel:

1. **Velocità** - Molte operazioni si svolgono sui dati locali, evitando richieste a un server
2. **Sviluppo non lineare** - Branch e merge consentono di sviluppare e integrare modifiche in parallelo
3. **Distribuzione** - Ogni clone completo conserva la cronologia e permette di creare commit offline
4. **Gestione di progetti grandi** - Le strutture dati sono progettate per gestire molti file e revisioni
5. **Integrità dei dati** - Gli hash consentono di identificare gli oggetti e rilevare alterazioni dei contenuti

### Caratteristiche Rivoluzionarie

#### 1. **Hash SHA-1**
```bash
# Ogni commit ha un identificatore unico e non modificabile
commit 1a2b3c4d5e6f7g8h9i0j1k2l3m4n5o6p7q8r9s0t
```

#### 2. **Snapshot, non Differenze**
```
CVS/SVN (delta-based):
File A: versione1 → diff1 → diff2 → diff3

Git (snapshot-based):  
Commit 1: [snapshot completo]
Commit 2: [snapshot completo]
Commit 3: [snapshot completo]
```

#### 3. **Branching Leggero**
```bash
# Creare un branch in Git = creare un puntatore (0.1 secondi)
# Creare un branch in SVN = copiare cartelle (minuti)
```

## 📊 Evoluzione dell'Adozione

### 2005-2008: Nascita e Prime Adozioni
- Linux Kernel migra a Git
- Comunità open source inizia ad adottarlo
- Git viene usato prima della nascita di GitHub

### Dal 2008: Collaborazione sul Web

GitHub nasce per facilitare la collaborazione sui progetti Git. Nei dieci anni successivi al lancio, la piattaforma viene utilizzata sia dalle comunità open source sia dalle aziende. [Fonte: GitHub, bilancio dei primi dieci anni](https://github.blog/news-insights/the-library/ten-years-of-code/).

### 2018: Microsoft Acquisisce GitHub

Il **26 ottobre 2018**, Microsoft annuncia il completamento dell'acquisizione di GitHub. L'acquisizione riguarda la piattaforma GitHub; Git resta un progetto open source distinto. [Fonte: annuncio ufficiale di Microsoft](https://blogs.microsoft.com/blog/2018/10/26/microsoft-completes-github-acquisition/).

## 🔍 Confronto Moderni Sistemi

| Caratteristica | CVS | SVN | Git | Mercurial |
|---------------|-----|-----|-----|-----------|
| **Tipo** | Centralizzato | Centralizzato | Distribuito | Distribuito |
| **Performance** | Lenta | Media | Veloce | Veloce |
| **Branching** | Difficile | Medio | Eccellente | Buono |
| **Curva di Apprendimento** | Media | Facile | Ripida | Media |
| **Adozione Attuale** | Obsoleto | Calante | Dominante | Nicchia |

## ⚠️ Errori Comuni nella Comprensione

### 1. **"Git è solo una versione migliorata di SVN"**
❌ **Sbagliato**: Git ha un paradigma completamente diverso
✅ **Realtà**: Git è distribuito, SVN è centralizzato

### 2. **"Tutti i VCS fanno la stessa cosa"**
❌ **Sbagliato**: Le architetture influenzano workflow e possibilità
✅ **Realtà**: Git permette workflow impossibili con sistemi centralizzati

### 3. **"Git è troppo complicato"**
❌ **Parzialmente vero**: La flessibilità può confondere inizialmente
✅ **Realtà**: I comandi base sono semplici, la potenza sta nelle opzioni avanzate

## 💡 Best Practices Storiche

### Lezioni dal Passato

#### 1. **Non Ignorare la Curva di Apprendimento**
Ogni transizione (CVS→SVN→Git) ha richiesto formazione del team

#### 2. **La Flessibilità Vince sulla Semplicità**
Git ha vinto nonostante la curva di apprendimento più ripida

#### 3. **Il Backup Distribuito è Cruciale**
I sistemi centralizzati hanno sempre il rischio del single point of failure

## 🧠 Quiz di Autovalutazione

### Domanda 1
Qual era il principale limite dei primi sistemi di controllo versione (SCCS, RCS)?
- A) Erano troppo veloci
- B) Non supportavano la collaborazione
- C) Erano troppo distribuiti
- D) Non funzionavano su Unix

<details>
<summary>Risposta</summary>
<strong>B) Non supportavano la collaborazione</strong><br>
I primi sistemi permettevano solo a un utente di modificare un file alla volta.
</details>

### Domanda 2  
Cosa distingue principalmente Git dai sistemi centralizzati come SVN?
- A) Git è più colorato
- B) Git è più veloce
- C) Ogni repository Git è completo e indipendente
- D) Git usa meno memoria

<details>
<summary>Risposta</summary>
<strong>C) Ogni repository Git è completo e indipendente</strong><br>
Questa è la caratteristica fondamentale dei sistemi distribuiti.
</details>

### Domanda 3
Perché Linus Torvalds creò Git?
- A) Per guadagnare soldi
- B) Perché si annoiava
- C) Perché aveva bisogno di un sistema veloce e distribuito per Linux
- D) Per competere con Microsoft

<details>
<summary>Risposta</summary>
<strong>C) Perché aveva bisogno di un sistema veloce e distribuito per Linux</strong><br>
Git fu creato specificatamente per gestire lo sviluppo del kernel Linux.
</details>

## 🏋️ Esercizi Pratici

### Esercizio 1: Timeline Personale
Crea una timeline dei sistemi di controllo versione che hai usato (o sentito nominare):

```
Anno: Sistema: Esperienza/Conoscenza:
_____________________________________
20__: _______ → ___________________
20__: _______ → ___________________  
20__: _______ → ___________________
```

### Esercizio 2: Analisi Comparativa
Compila questa tabella con i vantaggi/svantaggi:

| Aspetto | Sistema Centralizzato | Sistema Distribuito |
|---------|----------------------|-------------------|
| **Backup** | _________________ | _________________ |
| **Velocità** | _______________ | _________________ |
| **Collaborazione** | _________ | _________________ |
| **Complessità** | ___________ | _________________ |

### Esercizio 3: Scenario di Migrazione
Una azienda vuole migrare da SVN a Git. Elenca 3 sfide principali e 3 benefici:

**Sfide:**
1. _________________
2. _________________  
3. _________________

**Benefici:**
1. _________________
2. _________________
3. _________________

## 📖 Approfondimenti

### Documentazione Storica
- [Pro Git - Breve storia di Git, capitolo 1.2](https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git)
- [Intervista a Linus Torvalds per i vent'anni di Git (2025)](https://github.blog/open-source/git/git-turns-20-a-qa-with-linus-torvalds/)
- [GitLab - Vent'anni di storia di Git, di Patrick Steinhardt](https://about.gitlab.com/blog/journey-through-gits-20-year-history/)
- [GitHub - Annuncio del lancio pubblico (2008)](https://github.blog/news-insights/we-launched/)
- [Linus Torvalds - Git Talk (2007)](https://www.youtube.com/watch?v=4XpnKHJAok8)

### Confronti Dettagliati  
- [Git vs SVN - Atlassian](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [Pro Git - Che cos'è Git, capitolo 1.3](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)

## 🧭 Navigazione del Corso

- [📑 Indice](README.md)
- [⬅️ Cos'è il Controllo di Versione](01-controllo-versione.md)
- [➡️ Git vs Altri Sistemi](03-git-vs-altri.md)
