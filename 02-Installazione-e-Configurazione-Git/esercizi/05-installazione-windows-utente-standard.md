# Esercizio 05 - Installare e usare Git su Windows con un utente standard

## 🎯 Obiettivo

Prepara una postazione Windows utilizzabile senza privilegi amministrativi: Git e VS Code nel profilo personale, comandi disponibili tramite PATH utente, Git Bash come terminale e VS Code come editor dei commit.

**Durata:** 60-75 minuti. **Prerequisiti:** account Windows standard, accesso Internet e possibilità di eseguire software nelle cartelle personali. Non serve GitHub.

Puoi consultare l'[esempio guidato](../esempi/05-setup-windows-senza-amministratore.md). Se la postazione è già configurata, verifica l'installazione esistente senza reinstallarla e documenta i percorsi che trovi.

## 📋 Attività 1 - Pianificare l'installazione

Compila questa tabella prima di procedere:

| Informazione | Il tuo valore |
|--------------|---------------|
| Architettura Windows e pacchetto scelto | |
| Cartella di Git o PortableGit | |
| Cartella di VS Code | |
| Directory da aggiungere al PATH per Git | |
| Directory da aggiungere al PATH per `code` | |

Scarica i programmi dalle pagine ufficiali collegate nell'esempio. Installa Git in una cartella personale e VS Code con lo **User Installer**. In alternativa, usa PortableGit se consentito dalla postazione e adatta i percorsi.

**Da dimostrare:** programmi eseguiti con il tuo account standard e percorsi effettivi annotati. Se interviene un blocco del laboratorio, registra il messaggio e chiedi al docente di predisporre un percorso consentito.

## 🛤️ Attività 2 - Configurare e verificare il PATH utente

Apri le variabili di ambiente del tuo account. Conserva le voci presenti e aggiungi soltanto quelle necessarie: `cmd` dentro la cartella di Git e `bin` dentro quella di VS Code. Non modificare le variabili di sistema.

Chiudi terminali e tutte le finestre VS Code, poi apri una nuova finestra **PowerShell** dal menu Start:

```powershell
git --version
where.exe git
code --version
where.exe code
```

Annota versioni e percorsi. Se esistono più installazioni, indica quale viene trovata per prima. Se il percorso non è quello pianificato, confrontalo con il docente prima di modificare configurazioni preesistenti.

**Domanda:** perché trovare Git dentro Git Bash non basta a verificare il PATH di Windows?

## 💻 Attività 3 - Orientarsi in Git Bash

Apri Git Bash dal menu Start o dalla cartella del programma:

```bash
pwd
printf '%s\n' "$HOME"
git --version
command -v git
cygpath -w "$(command -v git)"
cd ~
mkdir -p git-esercizi
cd git-esercizi
ls -la
```

Scrivi il percorso di `git-esercizi` sia in formato Windows sia in formato Bash. Spiega il significato di `~`, `pwd` e `cd`.

**Da dimostrare:** sai riconoscere in quale shell stai lavorando e sai raggiungere una cartella del tuo profilo.

## ⚙️ Attività 4 - Integrare Git e Git Bash in VS Code

1. Apri VS Code e imposta Git Bash tramite **Terminal: Select Default Profile**.
2. Se il profilo non viene rilevato, configura il percorso effettivo di `bin\bash.exe` nelle **impostazioni utente**, seguendo il JSON dell'esempio.
3. Crea un nuovo terminale e verifica `git --version`, `pwd` e `command -v git`.
4. Apri **Git: Show Git Output** e annota quale eseguibile usa l'integrazione Git.
5. Se necessario, imposta `git.path` con il percorso assoluto di `cmd\git.exe`, poi riavvia VS Code.

**Da dimostrare:** il terminale integrato usa Bash e l'integrazione Git trova l'installazione prevista. Il percorso della shell e quello di Git hanno funzioni diverse.

## 👤 Attività 5 - Configurare identità ed editor

Nel terminale **Git Bash** di VS Code, usando nome ed email personali:

```bash
git config --global user.name "Nome Cognome"
git config --global user.email "tua.email@example.com"
git config --global init.defaultBranch main
git config --global core.editor "code --wait"
git config --global --show-origin --list
```

Indica da quale file vengono lette queste impostazioni e spiega perché non servono privilegi amministrativi. Non includere nella consegna eventuali altre configurazioni con dati riservati.

## 🧪 Attività 6 - Realizzare una prova completa

In Git Bash crea un repository nuovo. Se il nome è già occupato, scegline un altro:

```bash
cd ~/git-esercizi
mkdir verifica-git-windows
cd verifica-git-windows
git init -b main
code .
```

Da VS Code crea un file `README.md` che contenga:

- Nome e cognome, classe e data della prova.
- Metodo scelto: Setup per utente o PortableGit.
- Percorsi effettivi di Git e VS Code.
- Spiegazione in due frasi del PATH utente.

Salva e registra il primo commit dal terminale integrato:

```bash
git add README.md
git commit -m "Documenta la postazione Windows"
```

Aggiungi al README una sezione `## Verifiche` con i risultati delle versioni e una spiegazione della differenza tra Git Bash e Git. In **Source Control** osserva la modifica e leggi le differenze.

Poi esegui:

```bash
git diff -- README.md
git add README.md
git commit
```

Scrivi il messaggio del secondo commit nell'editor che si apre. Salva e chiudi la scheda del messaggio per terminare il comando.

```bash
git log --oneline -2
git status
```

**Risultato richiesto:** due commit, directory di lavoro pulita e repository riconosciuto dal pannello Source Control.

## 🔍 Attività 7 - Diagnosticare un guasto

Scegli uno scenario e descrivi i controlli che faresti, senza alterare un ambiente già funzionante:

1. `git --version` funziona in Git Bash ma PowerShell non trova `git`.
2. Git funziona nel terminale integrato, ma il pannello Source Control non lo rileva.
3. Hai cambiato il profilo predefinito, ma il vecchio terminale VS Code resta PowerShell.
4. `git commit` rimane in attesa con una scheda aperta in VS Code.

Per ogni scenario scelto indica **causa possibile, verifica e soluzione**.

## 📝 Consegna

Consegna un breve resoconto con:

1. Tabella dei percorsi e metodo di installazione.
2. Risultati dei quattro comandi PowerShell dell'attività 2.
3. Evidenza del terminale Git Bash integrato e dell'eseguibile trovato da VS Code.
4. Valore di `core.editor`, origine della configurazione e identificativi dei due commit.
5. Contenuto finale del README e risultato di `git status`.
6. Diagnosi dello scenario scelto e risposte alle domande finali.

È sufficiente allegare output testuale o schermate pertinenti. Non è richiesto pubblicare il repository online.

### Domande finali

1. Perché nel PATH si aggiunge una cartella e non `git.exe`?
2. Che differenza c'è tra PATH utente e PATH di sistema?
3. Perché riaprire soltanto un terminale dentro un VS Code rimasto aperto può non bastare?
4. Che cosa cambia tra `Git\cmd\git.exe`, `Git\bin\bash.exe` e `git-bash.exe`?
5. Perché `git config --global` è utilizzabile da un utente standard?
6. Quale problema risolve `--wait` nel comando dell'editor?

### Valutazione

| Criterio | Punti |
|----------|-------|
| Installazione o verifica corretta nel profilo personale | 2 |
| PATH utente verificato da PowerShell | 2 |
| Uso di Git Bash e integrazione con VS Code | 2 |
| Identità, editor e prova con due commit | 2 |
| Resoconto, spiegazioni e diagnosi | 2 |
| **Totale** | **10** |

---

[Esempio guidato](../esempi/05-setup-windows-senza-amministratore.md) · [Indice del modulo](../README.md) · [Configurazione identità](../02-configurazione-identita.md)
