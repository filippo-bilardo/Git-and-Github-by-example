# Autenticazione SSH con GitHub

## 🎯 Obiettivo e risultato finale

Configura l'accesso SSH al tuo account GitHub e dimostra che funziona inviando due commit a un repository personale chiamato `prova-ssh-github`.

Al termine saprai distinguere l'identità dell'autore di un commit dalle credenziali di accesso, gestire una coppia di chiavi e riconoscere un URL remoto SSH.

**Durata indicativa:** 45-60 minuti.

## 📋 Prerequisiti e ambiente di lavoro

Servono un account GitHub con email verificata, Git, OpenSSH e un editor di testo. Devi già conoscere `git add`, `git commit` e `git status`.

Scegli **un solo ambiente** per tutta l'attività:

| Ambiente | Terminale da usare |
|----------|-------------------|
| PC Linux o macOS | Terminale locale |
| PC Windows | **Git Bash**, incluso in Git for Windows; i comandi seguenti usano la sintassi Bash |
| Web4Student, se previsto dal docente | Terminale remoto del tuo account personale |

Se lavori su Web4Student, collegati prima dal PC:

```bash
ssh -p 2222 username@w4s.filippobilardo.it
```

Sostituisci `username` con il tuo utente Web4Student. Da questo momento esegui tutti i comandi nel terminale remoto; il browser resta sul PC.

La chiave deve trovarsi nell'ambiente che esegue Git. Una chiave presente sul PC non viene automaticamente usata su Web4Student.

```text
Percorso locale:    PC ── SSH con chiave del PC ──> GitHub
Percorso remoto:   PC ── accesso Web4Student ──> Web4Student ── propria chiave SSH ──> GitHub
```

Il laboratorio usa una cartella dedicata nella tua home, separata da eventuali siti o altri repository.

## Passo 1 - Verificare gli strumenti e capire cosa autentichi

```bash
git --version
ssh -V
pwd
```

**Verifica:** i primi due comandi mostrano le versioni; `pwd` indica dove stai lavorando.

In questo esercizio incontrerai tre informazioni diverse:

| Informazione | Funzione |
|--------------|----------|
| `user.name` e `user.email` di Git | Identificano l'autore dei commit |
| Chiave SSH registrata su GitHub | Autentica l'accesso del client al tuo account |
| Permessi sul repository | Stabiliscono se il tuo account può leggere o scrivere |

Puoi creare commit senza collegarti a GitHub. Il push richiede invece autenticazione e permessi di scrittura. Nell'indirizzo `git@github.com` l'utente SSH è sempre `git`: GitHub riconosce il tuo account dalla chiave presentata.

Riferimento: [GitHub Docs - Informazioni su SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh).

## Passo 2 - Controllare le chiavi esistenti

```bash
ls -la ~/.ssh
```

Se la directory non esiste, la creerai al passo successivo. Se trovi già una coppia adatta, puoi riutilizzarla e saltare la generazione, adattando i percorsi successivi.

Per questo laboratorio useremo questi nomi:

| File | Uso |
|------|-----|
| `~/.ssh/github_ed25519` | Chiave privata: rimane nel tuo account sul computer o server scelto |
| `~/.ssh/github_ed25519.pub` | Chiave pubblica: va registrata su GitHub |

Non sovrascrivere chiavi esistenti. Se questi nomi sono occupati e devi creare un'altra coppia, scegli un nome diverso e usalo in tutti i passaggi.

Riferimento: [GitHub Docs - Controllare le chiavi esistenti](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys).

## Passo 3 - Generare la coppia di chiavi

Se non riutilizzi una coppia esistente:

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
ssh-keygen -t ed25519 -C "tua.email@example.com" -f ~/.ssh/github_ed25519
```

Sostituisci l'email. `-t` sceglie l'algoritmo, `-C` aggiunge un'etichetta e `-f` indica il file della chiave privata. L'email è un commento, non una credenziale.

Inserisci una **passphrase** quando richiesta e ripetila. Durante la digitazione il terminale non mostra i caratteri. La passphrase protegge l'uso della chiave privata e può essere diversa dalla password GitHub.

Controlla i file generati:

```bash
ls -l ~/.ssh/github_ed25519 ~/.ssh/github_ed25519.pub
chmod 600 ~/.ssh/github_ed25519
```

**Verifica:** esistono entrambi i file. La chiave privata deve restare fuori dal repository e non va consegnata al docente.

Riferimento: [GitHub Docs - Generazione di una chiave SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

## Passo 4 - Registrare la chiave pubblica su GitHub

Nel terminale:

```bash
cat ~/.ssh/github_ed25519.pub
```

Copia l'intera riga, dall'inizio `ssh-ed25519` fino al commento finale. Nel browser:

1. Accedi al tuo account e apri [Settings → SSH and GPG keys](https://github.com/settings/keys).
2. Premi **New SSH key**.
3. Assegna un titolo riconoscibile, per esempio `Portatile scuola` oppure `Web4Student personale`.
4. Scegli **Authentication Key** come tipo.
5. Incolla la chiave pubblica nel campo **Key** e premi **Add SSH key**.
6. Conferma l'accesso se GitHub lo richiede.

**Verifica:** la nuova chiave compare nell'elenco dell'account corretto. Registrarla permette di autenticarti con i permessi che il tuo account già possiede.

Riferimento: [GitHub Docs - Aggiungere una chiave all'account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).

## Passo 5 - Indicare a SSH quale chiave usare

Apri `~/.ssh/config` con un editor, per esempio:

```bash
nano ~/.ssh/config
```

Inserisci il blocco seguente. Se esiste già una sezione per `github.com`, integra quella sezione senza duplicarla o cancellare le altre configurazioni.

```sshconfig
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/github_ed25519
    IdentitiesOnly yes
```

Salva il file. Con `nano`: `Ctrl+O`, `Invio`, `Ctrl+X`.

```bash
chmod 600 ~/.ssh/config
```

`IdentityFile` seleziona la chiave con il nome personalizzato; `IdentitiesOnly yes` limita le identità proposte a quelle configurate. Questa attività assume un solo account GitHub nell'ambiente scelto.

Per evitare di ridigitare la passphrase a ogni operazione puoi caricare la chiave nell'agent della sessione:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/github_ed25519
ssh-add -l
```

**Verifica:** l'ultimo comando elenca l'impronta della chiave. Alla chiusura della sessione potrebbe essere necessario caricarla di nuovo; senza agent SSH può comunque chiedere direttamente la passphrase.

Su Windows esegui anche questi comandi in **Git Bash**, mantenendo lo stesso ambiente. Per l'integrazione con il portachiavi macOS o con l'agent nativo Windows consulta la [guida ufficiale all'agent SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

## Passo 6 - Provare l'autenticazione

```bash
ssh -T git@github.com
```

Alla prima connessione potrebbe essere richiesta conferma dell'identità del server. Confronta l'impronta mostrata con quella dello stesso algoritmo nella [pagina ufficiale delle impronte SSH di GitHub](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints). Scrivi `yes` soltanto se coincidono.

L'impronta del server identifica **GitHub**; quella della tua chiave identifica la tua chiave. Non sono lo stesso valore.

Il risultato atteso è:

```text
Hi TUO-ACCOUNT! You've successfully authenticated, but GitHub does not provide shell access.
```

**Verifica:** compare il tuo username GitHub. L'assenza di una shell interattiva è normale. Il test restituisce codice di uscita **1 anche quando l'autenticazione riesce**: valuta il messaggio, non soltanto il codice.

Riferimento: [GitHub Docs - Testare la connessione SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection).

## Passo 7 - Preparare un repository di prova

Nel browser crea un repository personale chiamato **`prova-ssh-github`**. Scegli la visibilità indicata dal docente e lascialo **vuoto**, senza README, `.gitignore` o licenza generati da GitHub.

Nel terminale crea una cartella nuova. Se `~/prova-ssh-github` esiste già, scegli un altro nome per la cartella locale.

```bash
cd ~
mkdir prova-ssh-github
cd prova-ssh-github
git init -b main
git config user.name "Nome Cognome"
git config user.email "tua.email@example.com"
```

Usa l'email verificata su GitHub oppure l'indirizzo `noreply` fornito nelle tue impostazioni email. Qui la configurazione vale soltanto per questo repository.

Crea `README.md` con l'editor:

```markdown
# Prova di autenticazione SSH

Studente: Nome Cognome
Ambiente di lavoro: PC personale oppure Web4Student

Questo repository documenta una connessione SSH funzionante verso GitHub.
```

Registra il primo commit:

```bash
git add README.md
git diff --cached
git commit -m "Aggiungi il resoconto della prova SSH"
```

## Passo 8 - Collegare il remoto SSH e inviare il primo commit

Sostituisci `TUO-ACCOUNT` con il tuo username **GitHub**, che può differire da quello del PC o di Web4Student:

```bash
git remote add origin git@github.com:TUO-ACCOUNT/prova-ssh-github.git
git remote -v
git push -u origin main
```

**Verifica:** `git remote -v` mostra un URL che inizia con `git@github.com:`. Aggiornando la pagina del repository su GitHub trovi il README e il primo commit.

Se vuoi applicare la configurazione a un altro repository che ha già un remoto HTTPS, controllane prima l'indirizzo con `git remote -v`. Per cambiare un remoto esistente si usa `git remote set-url origin URL-SSH`, indicando l'URL SSH di **quel repository**.

Riferimento: [GitHub Docs - Gestire i repository remoti](https://docs.github.com/en/get-started/git-basics/managing-remote-repositories).

## Passo 9 - Ripetere il ciclo modifica, commit e push

Apri il README e aggiungi una sezione `## Esito` con la data della prova e una breve spiegazione della differenza tra chiave pubblica e privata.

```bash
git diff -- README.md
git add README.md
git commit -m "Documenta l'esito dell'autenticazione SSH"
git push
git log --oneline -2
git status
```

**Verifica:** GitHub mostra due commit; il README contiene la nuova sezione e `git status` non segnala modifiche da registrare. Salvare il file modifica la copia di lavoro, il commit registra la versione locale e il push invia i commit al remoto.

## 🛠️ Risoluzione dei problemi

| Sintomo | Controllo da eseguire |
|---------|----------------------|
| `Permission denied (publickey)` | Controlla che la pubblica sia registrata sul tuo account e che `IdentityFile` indichi la privata corrispondente. Prova `ssh -vT git@github.com` per vedere quale chiave viene proposta |
| Il test saluta un altro account | Verifica la chiave selezionata e l'account sul quale l'hai registrata |
| `Could not open a connection to your authentication agent` | Avvia l'agent nello stesso terminale prima di eseguire `ssh-add` |
| `remote origin already exists` | Leggi `git remote -v`; se necessario modifica l'URL con `git remote set-url origin URL-SSH` |
| Il push chiede username e token | Controlla se `origin` usa ancora HTTPS |
| `Repository not found` o push negato | Controlla proprietario, nome del repository e permessi: un test SSH riuscito non concede accesso a tutti i repository |
| Connessione in timeout sulla porta 22 | Verifica le regole della rete con il docente; GitHub documenta anche [SSH sulla porta HTTPS](https://docs.github.com/en/authentication/troubleshooting-ssh/using-ssh-over-the-https-port) |
| Push rifiutato perché il remoto contiene altri commit | Controlla `git status` e la cronologia remota con il docente prima di integrare; la procedura guidata richiede un remoto inizialmente vuoto |

Per approfondire: [GitHub Docs - Permission denied (publickey)](https://docs.github.com/en/authentication/troubleshooting-ssh/error-permission-denied-publickey).

## 📝 Consegna e autovalutazione

Consegna:

1. URL del repository e identificativi dei due commit.
2. Output del test SSH con il tuo account riconosciuto e di `git remote -v`.
3. Un breve resoconto dell'ambiente usato e degli eventuali problemi risolti.
4. Risposte alle domande seguenti.

Non includere chiavi private, passphrase o altri segreti nel repository o nella consegna.

### Domande

1. Perché impostare `user.name` e `user.email` non basta per autenticarsi su GitHub?
2. Quale file registri su GitHub e dove conservi l'altro?
3. Perché usi `git@github.com` anziché il tuo username come utente SSH?
4. Se lavori su Web4Student, su quale macchina deve trovarsi la chiave privata?
5. Che cosa dimostra il test SSH? Che cosa dimostra in più un push riuscito?
6. A cosa serve la passphrase e quale ruolo ha `ssh-agent`?
7. Perché configurare SSH non cambia automaticamente un remoto HTTPS?

### Criteri di completamento

- [ ] La chiave pubblica è registrata sull'account corretto.
- [ ] Il test SSH riconosce il mio username GitHub.
- [ ] Il remoto del laboratorio usa un URL SSH.
- [ ] I due commit e il README aggiornato sono visibili su GitHub.
- [ ] So spiegare la differenza tra identità Git, autenticazione e permessi.

## 📚 Riferimento dell'attività

Esercizio ispirato alla parte sull'autenticazione SSH di [Git e GitHub per l'intera cartella www](https://github.com/filippo-bilardo/Learning-PHP-by-example/blob/main/docs/02-Ambiente_di_sviluppo/esercizi/02_Git_e_GitHub.md), di Filippo Bilardo, adattata a un laboratorio autonomo sul controllo di versione. Le pagine ufficiali GitHub sono collegate nei relativi passaggi.

---

[Indice degli esercizi](README.md) · [Guida teorica: autenticazione SSH](../05-autenticazione-ssh.md) · [Esercizio successivo: creazione di repository](02-repository-creation.md)
