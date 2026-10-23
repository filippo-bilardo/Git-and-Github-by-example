# Esempio 05 - Git su Windows senza privilegi di amministratore

## 🎯 Scenario e risultato

Mario usa Windows con un account standard. Deve installare Git per il proprio utente, lavorare in Git Bash e usare Visual Studio Code sia come editor dei commit sia per il controllo di versione.

Il percorso guidato usa **Windows 10/11**, una connessione Internet e cartelle personali scrivibili. Non richiede un account GitHub. Su un PC gestito dalla scuola, l'esecuzione di programmi nelle cartelle utente deve essere consentita dalle regole del laboratorio.

**Tempo indicativo:** 45-60 minuti.

## 1. Riconoscere programmi, terminali e percorsi

| Componente | Funzione |
|------------|----------|
| Git, eseguibile `git.exe` | Gestisce repository e commit |
| Git Bash | Ambiente Bash incluso in Git for Windows |
| VS Code | Editor con interfaccia Git integrata |
| PATH utente | Elenco di cartelle in cui cercare i comandi del proprio account |

Per questo esempio scegliamo questi percorsi, sostituendo `Mario` con il nome effettivo della cartella del profilo Windows:

```text
C:\Users\Mario\AppData\Local\Programs\Git
C:\Users\Mario\AppData\Local\Programs\Microsoft VS Code
```

`%LOCALAPPDATA%` identifica la cartella `AppData\Local` del tuo profilo. I percorsi sono una scelta del laboratorio: controlla sempre quelli effettivi sul tuo PC.

## 2. Installare Git nel proprio profilo

1. Apri la [pagina ufficiale di Git per Windows](https://git-scm.com/install/windows) e scarica il **Setup** adatto all'architettura del PC, normalmente x64.
2. Avvia il file con un doppio clic dal tuo account standard.
3. Scegli come destinazione la cartella personale indicata sopra, evitando `Program Files`.
4. Alla scelta dell'editor puoi lasciare quello proposto: configureremo VS Code dopo averlo installato.
5. Alla schermata del PATH scegli **Git from the command line and also from 3rd-party software**.
6. Per il terminale esterno Git Bash puoi mantenere **MinTTY**; completa l'installazione con le altre opzioni predefinite.

L'installer di Git for Windows supporta anche l'installazione senza elevazione, come documentato nel [codice ufficiale dell'installer](https://github.com/git-for-windows/build-extra/blob/main/installer/install.iss). Se viene richiesta una password amministrativa, annulla: verifica di non aver scelto una destinazione protetta o un pacchetto diverso.

### Alternativa: PortableGit

Se il Setup non è utilizzabile e il laboratorio consente programmi portabili, scarica **Portable** dalla stessa pagina ufficiale. Estrailo, per esempio, in:

```text
C:\Users\Mario\AppData\Local\Programs\PortableGit
```

Avvia `git-bash.exe` dalla cartella estratta. Nei passaggi successivi sostituisci `Programs\Git` con `Programs\PortableGit` nel PATH e nelle impostazioni VS Code. Il pacchetto portabile non configura automaticamente il PATH di Windows.

Se una regola del PC blocca anche i programmi portabili, segnala il blocco al docente per predisporre l'ambiente.

## 3. Installare VS Code come utente

Se VS Code non è già installato, scarica lo **User Installer** dal [sito ufficiale](https://code.visualstudio.com/download). Avvialo normalmente e mantieni la destinazione nel profilo personale. Se disponibile, seleziona **Add to PATH**.

Lo User Setup non richiede privilegi amministrativi; il System Setup installa invece per tutti gli utenti. Il percorso tipico dello User Setup è `%LOCALAPPDATA%\Programs\Microsoft VS Code`. Riferimento: [installazione ufficiale di VS Code su Windows](https://code.visualstudio.com/docs/setup/windows).

## 4. Impostare il PATH utente in modo permanente

### Che cos'è il PATH e a cosa serve

Il **PATH** è una **variabile di ambiente**, cioè un'impostazione che il sistema rende disponibile ai programmi. Contiene un elenco di cartelle nelle quali cercare gli eseguibili quando scrivi un comando senza indicarne il percorso completo.

Per esempio, quando digiti `git --version`, la shell deve trovare il programma Git. Se la cartella che contiene `git.exe` è nel PATH, puoi richiamarlo con il solo nome `git`, anche mentre lavori in un'altra directory. Altrimenti potresti ricevere un messaggio come «comando non riconosciuto», pur avendo Git installato.

Il PATH contiene **cartelle**, non il percorso completo di un file `.exe`. Per il nostro esempio, la voce corretta è:

```text
C:\Users\Mario\AppData\Local\Programs\Git\cmd
```

Windows rappresenta l'elenco delle cartelle separandole con un punto e virgola (`;`); la finestra di modifica normalmente mostra ogni voce su una riga. L'ordine delle voci conta: se più cartelle contengono un eseguibile con lo stesso nome, quello trovato prima può essere selezionato.

### PATH utente, PATH di sistema e modifica permanente

| Impostazione | A chi si applica |
|--------------|------------------|
| **PATH utente** | Al tuo account Windows; puoi modificarlo senza privilegi amministrativi |
| **PATH di sistema** | A tutti gli utenti del PC; modificarlo normalmente richiede privilegi amministrativi |

I programmi avviati dal tuo account ricevono un PATH che comprende le voci di sistema e quelle personali. In questo laboratorio aggiungiamo le cartelle al **PATH utente**, conservando tutte le voci già presenti.

Una modifica **permanente** viene salvata nelle impostazioni dell'account e resta disponibile anche dopo il riavvio del PC. Una modifica fatta soltanto nell'ambiente di un terminale vale invece per quella sessione e per i programmi avviati da essa. Aggiungere una cartella al PATH non installa il programma: rende raggiungibile un eseguibile già presente.

Git Bash prepara già il proprio ambiente: il fatto che `git` funzioni lì non prova che PowerShell o VS Code possano trovarlo.

### Procedura di configurazione

1. Nel menu Start cerca **Modifica le variabili di ambiente per l'account**.
2. Nella sezione **Variabili utente per …** seleziona `Path`, poi **Modifica**. Se manca, creala come variabile utente.
3. Conserva le voci esistenti. Aggiungi, soltanto se assenti, queste due cartelle effettive:

```text
C:\Users\Mario\AppData\Local\Programs\Git\cmd
C:\Users\Mario\AppData\Local\Programs\Microsoft VS Code\bin
```

4. Conferma tutte le finestre con **OK**.
5. Chiudi tutte le finestre di VS Code e i terminali già aperti. Riapri PowerShell dal menu Start.

Modifica il **PATH utente**. Aggiungi le directory senza virgolette nel relativo elenco, anche se contengono spazi. Per Git è sufficiente `Git\cmd`: non occorre esportare gli strumenti Unix di `Git\usr\bin` nel PATH di Windows.

Le nuove applicazioni ereditano l'ambiente aggiornato; un terminale appena creato dentro un VS Code rimasto aperto può ereditare ancora il vecchio PATH.

Riferimento sul ruolo del PATH: [Microsoft Learn - path](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/path).

### Verifica in una nuova finestra PowerShell

```powershell
git --version
where.exe git
code --version
where.exe code
```

Per Mario, `where.exe git` dovrebbe includere:

```text
C:\Users\Mario\AppData\Local\Programs\Git\cmd\git.exe
```

In PowerShell usa **`where.exe`**: `where` da solo è un alias PowerShell. Se compaiono più installazioni, confronta il primo risultato con quello scelto per il laboratorio: aggiungere una voce al PATH utente non garantisce che preceda un Git già nel PATH di sistema.

Per distinguere un errore di PATH da un programma mancante, prova i percorsi completi, adattandoli se hai scelto PortableGit:

```powershell
& "$env:LOCALAPPDATA\Programs\Git\cmd\git.exe" --version
& "$env:LOCALAPPDATA\Programs\Microsoft VS Code\bin\code.cmd" --version
```

Se questi comandi funzionano e quelli brevi no, controlla le voci del PATH e il riavvio delle applicazioni.

## 5. Usare Git Bash

Apri **Git Bash** dal menu Start oppure avvia `git-bash.exe` dalla cartella di Git. I comandi seguenti vanno eseguiti in Bash, non in PowerShell:

```bash
pwd
printf '%s\n' "$HOME"
git --version
command -v git
cygpath -w "$(command -v git)"
cd ~
mkdir -p git-laboratorio
cd git-laboratorio
ls -la
```

`pwd` mostra la directory corrente; `~` indica la home di Bash, normalmente il profilo Windows. `command -v` mostra il comando risolto da Bash; `cygpath -w` ne mostra il percorso in formato Windows. All'interno di Git Bash può comparire un eseguibile nella sottocartella `mingw64\bin` della stessa distribuzione.

| Percorso Windows di esempio | Percorso in Git Bash |
|----------------------------|----------------------|
| `C:\Users\Mario` | `/c/Users/Mario` |
| `C:\Users\Mario\git-laboratorio` | `/c/Users/Mario/git-laboratorio` |

Usa `/` nei percorsi Bash e le virgolette se contengono spazi. La sintassi delle variabili cambia con la shell: `%LOCALAPPDATA%` nelle finestre Windows/CMD, `$env:LOCALAPPDATA` in PowerShell, `$LOCALAPPDATA` in Git Bash.

## 6. Configurare VS Code e il terminale integrato

Apri VS Code, premi `Ctrl+Shift+P`, esegui **Terminal: Select Default Profile** e scegli **Git Bash**. Crea poi un **nuovo** terminale dal menu **Terminal → New Terminal**: quelli già aperti mantengono la shell precedente.

Se Git Bash non compare, apri **Preferences: Open User Settings (JSON)** dalla palette e integra queste proprietà nelle impostazioni utente esistenti:

```json
{
    "terminal.integrated.profiles.windows": {
        "Git Bash utente": {
            "path": "${env:LOCALAPPDATA}\\Programs\\Git\\bin\\bash.exe",
            "args": ["--login", "-i"]
        }
    },
    "terminal.integrated.defaultProfile.windows": "Git Bash utente"
}
```

Il profilo usa **`bin\bash.exe`**, la shell ospitata dal terminale integrato; `git-bash.exe` avvia invece il terminale esterno. Non sostituire l'intero file delle impostazioni se contiene altre preferenze.

Riferimento: [VS Code - Profili del terminale](https://code.visualstudio.com/docs/terminal/profiles).

### Se VS Code non trova Git

La shell integrata e il pannello **Source Control** sono configurazioni distinte. Cerca **Git: Show Git Output** nella palette per vedere quale Git usa l'integrazione.

Se il rilevamento automatico fallisce o seleziona un'altra installazione, imposta nelle **impostazioni utente** il percorso concreto del tuo eseguibile:

```json
{
    "git.path": "C:/Users/Mario/AppData/Local/Programs/Git/cmd/git.exe"
}
```

Sostituisci `Mario` e integra questa proprietà nello stesso oggetto JSON del tuo file. Per `git.path` usa un percorso assoluto effettivo, senza `%LOCALAPPDATA%`. Riavvia VS Code e ricontrolla l'output Git.

Il supporto Git è integrato in VS Code: per questo esempio non servono estensioni aggiuntive. Riferimento: [VS Code - Controllo di versione](https://code.visualstudio.com/docs/sourcecontrol/overview).

Per il rilevamento dell'eseguibile e l'uso di `git.path`: [VS Code - Git non trovato](https://code.visualstudio.com/docs/sourcecontrol/troubleshooting#git-not-found).

## 7. Configurare Git per il proprio utente

Dal nuovo terminale **Git Bash** di VS Code:

```bash
git config --global user.name "Mario Rossi"
git config --global user.email "mario.rossi@example.com"
git config --global init.defaultBranch main
git config --global core.editor "code --wait"
git config --global --get user.name
git config --global --get user.email
git config --global --get core.editor
git config --global --show-origin --list
```

Personalizza nome ed email. `--global` significa **configurazione dell'utente**, normalmente nel file `~/.gitconfig`; non significa configurazione di tutti gli utenti del PC. `--system` riguarda invece l'installazione ed è fuori dal percorso di questo laboratorio.

`code --wait` fa attendere Git finché non chiudi il file aperto per il messaggio di commit. Nome ed email identificano l'autore: non sono credenziali GitHub.

## 8. Verificare tutto con due commit

Nel terminale Git Bash, dalla cartella `~/git-laboratorio`, crea una directory nuova. Se `prova-windows-utente` esiste già, scegli un nome libero:

```bash
cd ~/git-laboratorio
mkdir prova-windows-utente
cd prova-windows-utente
git init -b main
printf '# Git su Windows come utente standard\n' > README.md
git add README.md
git commit -m "Crea il laboratorio Windows"
code .
```

In VS Code apri **Source Control** (`Ctrl+Shift+G`): deve riconoscere il repository. Aggiungi al README una frase sul tuo ambiente e salva. Il file appare tra le modifiche; selezionalo per leggere le differenze.

Dal terminale Git Bash integrato:

```bash
git diff -- README.md
git add README.md
git commit
```

L'ultimo comando apre il messaggio di commit in VS Code. Scrivi `Verifica Git Bash e VS Code`, salva e **chiudi la scheda del messaggio**. Il comando può restare in attesa finché quella scheda è aperta.

```bash
git log --oneline -2
git status
```

**Risultato atteso:** due commit, nessuna modifica da registrare e pannello Source Control coerente con `git status`.

## 🛠️ Diagnosi rapida

| Problema | Controllo |
|----------|-----------|
| L'installazione chiede privilegi elevati | Verifica pacchetto e destinazione personale; valuta il percorso PortableGit consentito dal laboratorio |
| Git funziona in Bash ma non in PowerShell | Verifica `Git\cmd` nel PATH utente e apri una nuova finestra PowerShell |
| `code` non viene trovato | Verifica `Microsoft VS Code\bin` nel PATH utente e riapri tutte le applicazioni |
| Il terminale VS Code apre PowerShell | Seleziona il profilo Git Bash e crea un nuovo terminale |
| Il terminale usa Git ma Source Control no | Riavvia VS Code; controlla l'output Git ed eventualmente `git.path` |
| Percorso Git Bash del profilo inesistente | Controlla la cartella scelta nel Setup o sostituisci `Git` con `PortableGit` |
| `git commit` sembra fermo | Salva e chiudi la scheda del messaggio aperta da `code --wait` |

## ➡️ Prova autonoma

Completa l'[esercizio Windows con utente standard](../esercizi/05-installazione-windows-utente-standard.md).

[Indice del modulo](../README.md) · [Installazione sui diversi sistemi operativi](../01-installazione-os.md) · [Configurazione di editor e tool](../04-editor-tool.md)
