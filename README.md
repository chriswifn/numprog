# Numerik Programmieraufgaben WiSe 2023/2024

**Diese Form der Abgabe gilt erst ab der 2. Programmieraufgabe!!!**

Fuer die Abgaben sind nur die 2 untersten Sections wichtig. Alles darueber sind generelle Anleitungen, die sie ignorieren koennen, wenn sie wissen, was **Git** ist und wie es funktioniert.

Das was im folgenden beschrieben wird ist eine technische Dokumentation und sollte dementsprechend gelesen werden.

Die Numerik Programmieraufgaben dieses Semester werden anders ablaufen als in den vorherigen Semestern. Es wird keine Abgabe per E-Mail geben.

Stattdessen werden sie jeweils (pro Abgabe-Team) eine Private Git Repository erstellen.
Wie das ganze ablaufen wird, und wie sie das aufsetzen koennen wird im Folgenden beschrieben.

Die Aufgaben werden sie in **Branches** (ein Branch pro Abgabe) bearbeiten. Diese werden durch eine Public Repository bereitgestellt werden, die sie als **Upstream** in ihren privaten Fork integrieren muessen.

Bitte lesen sie sich selber in die Funktionsweise von **Git** ein, das wuerde den Rahmen dieser Anleitung sprengen.

Weiter unten in dieser Anleitung wird aber Schritt fuer Schritt beschrieben, wie sie vorgehen muessen um eine Programmieraufgabe zu bearbeiten und abzugeben. Desweiteren wird in jeder Programmieraufgabe genau beschrieben sein, wie sie fuer die jeweilige Programmieraufgabe vorzugehen haben. Bitte nehmen sie sich fuer die Bearbeitung Zeit, da vor allem als Anfaenger mit **Git** unerwartete Dinge passieren koennen, fuer die sie dann eventuell keine Zeit mehr haben, wenn sie die Aufgaben auf den letzten Druecker bearbeiten.


# GitHub account erstellen
Sie muessen einen [GitHub](https://github.com) erstellen, um die Aufgaben abzugeben. Sie werden eine E-Mail Adresse benoetigen. Wenn Sie in der Zukunft Vorteile von **GitHub** wollen verlinken sie den Account mit ihrer studentischen E-Mail. Das gibt ihnen bspw. kostenlosen Zugriff auf [GitHub Copilot](https://github.com/features/copilot).


# Git aufsetzen
Die Anleitung wird im Folgenden nur auf das `git` commandline-tool eingehen. Wenn sie das ganze etwas unkomplizierter umsetzen wollen installieren sie [GitHub Desktop](https://desktop.github.com/). Ich werde keine Anleitung fuer **GitHub Desktop** zur Verfuegung stellen, bin aber offen fuer Aenderungen an dieser Anleitung, wenn jemand dafuer eine detaillierte Beschreibung zur Verfuegung stellen will.
Eine allgemeine Anleitung fuer **GitHub Desktop** finden sie [hier](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/adding-and-cloning-repositories/cloning-and-forking-repositories-from-github-desktop)

Wenn sie mehr ueber die Technologie lernen wollen, benutzen sie `git`. Dadurch wird meiner Meinung nach die Funktionsweise klarer. Desweiteren sind alle Antworten auf Probleme mit **Git** fuer das commandline-tool `git` geschrieben, wenn Sie z.B. auf [stackoverflow](https://stackoverflow.com/) unterwegs sind.
Mit dem aktuellen Trend in Richtung **Cloud Services** kann es gut sein, dass sie sich irgendwann in einer Situation wiederfinden, wo sie auf einem Rechner ohne grafische Oberflaeche arbeiten muessen. Es kann also nicht schaden sich mit Kommandozeilen-Programmen vertraut zu machen.


## Umgebung fuer `git`

**DISCLAIMER**: **Git** muss nicht manuell ueber `git` umgesetzt werden. Alternativen sind GitHub Desktop oder Git-Bash

### Windows (1)
**DISCLAIMER**: Es braucht kein `wsl` fuer **Git**, aber es ist entspannter meiner Meinung nach.
Windows ist **KEINE** Umgebung fuer Software-Entwicklung. Gluecklicherweise ist das selbst Microsoft bekannt. Deswegen stellt Microsoft seit einigen Jahren eine virtuelle **Linux** Integration bereit, die voll in Windows integriert ist. Siehe [hier](https://learn.microsoft.com/de-de/windows/wsl/install)

Eine kurze Anleitung zur Installation von **WSL** (Windows Subsystem for Linux):

1. Oeffnen Sie Powershell oder die Windows Command Prompt als Administrator. Klicken sie dafuer mit Rechtsklick auf das Symbol und waehlen sie `Ausfuehren als Administrator` aus.
1. In der Kommandozeile fuehren sie den folgenden Befehl aus.
   ```powershell
   $ wsl --install
   ```
   Keine Sorge, ihr System bleibt dadurch unveraendert. Windows wird allerdings einige Updates ausfuehren muessen, d.h. sie muessen ihren PC nach Abschluss des Befehls neustarten muessen. Stellen sie sicher, dass sie waehrend des Prozesses eine funktionierende Internet-Verbindung haben.

Jetzt sollten sie eine funktionierende Installation von **WSL** haben. **WSL** ist sehr nuetzlich auch ausserhalb dieser Vorlesung, d.h. es kann nicht schaden den Installationsprozess einmal durchlaufen zu haben.

Oeffnen Sie **Ubuntu**. Beim ersten Start kann das einige Minuten dauern. Danach sollte **WSL** in unter eine Sekunde gestartet werden koennen. Sie werden nach einem Passwort gefragt werden. Benutzen sie ein sicheres Passwort. Jeder der Zugang zu diesem Passwort hat, kann theoretisch ihre Windows Installation zerstoeren.

### UNIX basierte Systeme (1)
Ignorieren sie diesen Punkt der Anleitung. Es muesste schon alles eingerichtet sein.


## `git` installieren
Ab hier wird angenommen, dass sie Zugang zu einer `bash`/`zsh`-Kommandozeile haben. Unter Linux und MacOS oeffnen sie dafuer einfach ein **Terminal**.
Unter Windows oeffnen sie **WSL**.

### Windows (2)
In **WSL** fuehren sie den folgenden Befehl aus:
```bash
$ sudo apt install git
```

### UNIX basierte Systeme (2)
Benutzen sie ihren **Packet Manager** um `git` zu installieren.

Unter **MacOS** gibt es die Options [Homebrew](https://brew.sh/).


## `git` aufsetzen
Sie werden einen **Benutzernamen** und eine **E-Mail** Adresse angeben muessen. Diese werden in `git` commits angezeigt, d.h. waehlen sie einen passenden Benutzernamen. Die **E-Mail** sollte dieselbe sein, wie die E-Mail die sie fuer ihren **GitHub**-Account benutzt haben.

Um diese Variablen auf ihren System lokal zu setzen kopieren sie die folgenden Befehle:
```bash
$ git config --global user.name "<YOUR_USERNAME>"
$ git config --global user.email "<YOUR_EMAIL>"
```


## `git` mit GitHub synchronisieren
Um erfolgreich einen `git` **push** auszufuehren, muessen sie **SSH**-keys generieren, die mit ihrem **GitHub** Profil synchronisiert werden muessen. Eventuell muessen sie vorher erst **SSH** installieren.

1. Oeffnen sie ein Terminal

1. Geben sie den folgenden Befehl ein:
   ```bash
   $ ssh-keygen -t ed25519 -C "<YOUR_EMAIL>"
   ```
   Das generiert einen neues **SSH**-Keypaar mit ihrer **E-Mail** als Label.

1. Fuegen sie den Key dem ssh-agent hinzu
   ```bash
   $ eval "$(ssh-agent -s)"
   $ ssh-add ~/.ssh/id_ed25519
   ```

1. Fuegen sie den **PUBLIC**!!!!! Key in ihrem **GitHub** Profil ein. Fuehren sie dazu die folgenden Schritte aus
   - **PUBLIC**!!!!! Key kopieren. Machen sie diesen Schritt niemals mit dem **PRIVATE** Key.
     ```bash
     $ cat ~/.ssh/id_ed25519.pub
     ```
     Waehlen sie den Text aus und kopieren sie ihn in ihr Clipboard. Bitte kopiert **NIEMALS** einen private key ins Clipboard.
   - Oben rechts auf ihrem Profil waehlen sie ihren Avatar aus und klickt auf **Einstellungen**
   - In dem **Zugriff**-Teil klicken sie auf **SSH key hinzufuegen**.
   - Fuegen sie hier ihren **SSH** key ein.


# `git` lernen
`git` kann nicht verstanden werden durch Theorie. Das muss manuell ausprobiert werden.
Erstellen sie dazu ein temporaeres Verzeichnis und wechseln sie in dieses.
```bash
$ cd "$(mktemp -d)"
```

Um ein normales Verzeichnis in eine `git` Repository umzuwandeln, muss `git` initialisiert werden.
```bash
$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>
```

Ignorieren sie diese hints. Das einzige was sie interessiert, ist ob der Befehl erfolgreich war. Checken kann man das mit dem Befehl
```bash
$ echo $?
```
Eine `0` heisst erfolgreich, bei Fehlercode wird ein Integer ungleich 0 zurueckgegeben.

Erstellen sie eine Datei in dem Verzeichnis. Es bietet sich ein **README** an. In dieser Datei stehen in der Regel Erklaerungen/Installation des Programmes.
```bash
$ touch README.md
```
Und befuellen sie die Datei mit Text
```bash
$ echo -e "# Das ist ein Test" > README.md
```

Wenn sie nun den Status der Repository kontrollieren wollen, benutzen sie den Befehl
```bash
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
```

Wie sie sehen koennen, sind sie im `master` branch. Das wird spaeter nochmal wichtig.
Was auch zu erkennen ist, dass `Untracked files` existieren.

Grob besteht eine `git` Verzeichnis aus den folgenden Bestandteilen:

1. **Working Directory**: Das Verzeichnis in dem sich ein `.git` Unterverzeichnis befindet. Das ist das Verzeichnis, in dem sie arbeiten. In der **Working Directory** sind die sogenannten **Untracket Files**, also die Dateien die nicht von der Git Repository geindexed werden. Wenn sie hier Aenderungen machen und nicht speichern, koennen diese verloren gehen.

2. **Staging Area**: `git` tracked und speichert Dateien in der Staging Area.
   ```bash
   $ git add <FILE>
   ```
   zur Staging Area hinzugefuegt werden

3. **Lokale Git repository**: Alles in dem `.git` Verzeichnis. Hier sind Checkpoints und commits gespeichert. In der repository wird alles gespeichert und geindexed. Loeschen sie **AUF GAR KEINEN FALL** das `.git` Verzeichnis. Einen Commit kann man sich als einen **Checkpoint** vorstellen. Alles was bis zu einem Commit gespeichert wird, ist gesichert. Wenn ein neuer Commit gemacht wird, kann bei Bedarf zu einem beliebig anderen Commit zurueckgesetzt werden, wenn das noetig ist.
   ```bash
   $ git commit -m "<COMMIT_MESSAGE>"
   ```

4. **Remote**: Eine Remote Repository (nicht die lokale Version, sondern extern gespeichert z.B. GitHub/GitLab,BitBucket,...). Eine `global` gespeicherte Kopie der lokalen Version.

Wenn sie die Datei `README.md` also hinzufuegen wollen zur Git Repository:
```bash
$ git add README.md
$ git commit -m "initial commit"
```

Die Programmieraufgaben werden jeweils in einem eigenen **Branch** bearbeitet und abgegeben.
Um einen neuen **Branch** auf Basis des aktuellen **Branches** zu erstellen, geht man wie folgt for

```bash
$ git checkout -b <NEW_BRANCH_NAME>
```

oder
```bash
$ git branch <NEW_BRANCH_NAME>
$ git checkout <NEW_BRANCH_NAME
```

Um alle **Branches** angezeigt zu bekommen, gibt es den folgenden Befehl

```bash
$ git branch
  master
* pa1
```
Der aktuelle Branch ist mit einem `*` markiert. Wenn sie Aenderungen in diesem Branch vornehmen **MUESSEN** diese zur Git repository hinzugefuegt werden, bevor sie den Branch wechseln. Sonst kommen alle ungespeicherten Aenderungen mit. DAS WILL MAN NICHT!!!!!

Jetzt sollten sie zumindest etwas mehr mit `git` vertraut sein.

Die Abgaben werden sie in einer privaten **upstream** Repository machen.
Dazu werden sie einen privaten **Fork** der globalen Repository erstellen muessen. Wie das geht wird im naechsten Punkt der Anleitung beschrieben.

# Privaten fork einer public Repository erstellen

## Was ist ein Fork?
Ein Fork ist eine neue Repository, die Dateien und Einstellungen mit dem Originalen "upstream"
teilt. Forks benutzt man, um spaeter ueber eine Pull Request einem Projekt mitzuwirken. Pull Requests sind fuer uns irrelevant (zumindest zum jetztigen Zeitpunkt, vielleicht lass ich mir noch was dazu einfallen). Das Problem ist, dass Forks auch die Einstellung zum Thema **Sichtbarkeit** teilen. D.h. wenn der "upstream" **public** ist, kann ein direkter Fork nicht **private** sein. Ihre Abgaben sollten aber privat sein. Deswegen muessen wir das ganze ueber einen Umweg machen.

## Privaten fork erstellen

Das ist eine allgemeine Anleitung. Der Username und Repo Name sind immer noch offen zur Debatte. Deswegen werden hier Generics benutzt.

1. Erstellen sie einen **bare** clone der public Repository. Diese ist temporaer, muss also nicht speziell irgendwo gespeichert werden, weil sie die danach loeschen koennen.
   ```bash
   $ git clone --bare https://github.com/<USERNAME>/<REPO_NAME>
   ```

2. Erstellen sie eine neue **PRIVATE** Repository in GitHub mit dem Namen `<REPO_NAME>`

3. Jetzt muss ein Mirror push vorgenommen werden
   ```bash
   $ cd <REPO_NAME>
   $ git push --mirror git@github.com:<YOUR_USERNAME>/<REPO_NAME>
   ```

4. Loeschen sie den bare clone
   ```bash
   $ cd ..
   $ rm -rf <REPO_NAME>
   ```

5. Cloned eure private Repository. Dieser Ordner sollte irgendwo abgespeichert werden, wo es Sinn macht.
   ```bash
   $ git clone git@github.com:<YOUR_USERNAME>/<REPO_NAME>
   ```

6. Die Original Repo muss als **remote** hinzugefuegt werden, dass sie spaeter Aenderungen **fetchen**/**clonen** koennen. Stellen sie sicher, dass sie **push** auf diesen **upstream** ausstellen. Sie werden sowieso nicht die Berechtigung dazu haben, aber **best practice** ist angesagt.
   ```bash
   $ git remote add upstream https://github.com/<USERNAME>/<REPO_NAME>.git
   ```
   Wobei hier dieser **remote** einfach als **upstream** betitelt wird.
   Wenn sie eine Liste aller **remotes** wollen, fuehren sie den Befehl
   ```bash
   $ git remote -v
   ```
   aus.

7. Wenn sie spaeter Aenderungen des **upstreams** zu ihrem Fork hinzufuegen wollen, geht das ueber einen **fetch**
   ```bash
   $ git fetch upstream
   $ git rebase upstream/<BRANCH_YOU_WANT_TO_FETCH>
   ```
   Es kann sein, je nachdem wie bzw. wann sie diesen **Rebase** durchfuehren, dass ihr **remote** Branch `origin/<BRANCH_NAME>` und ihr **lokaler** `<BRANCH_NAME>` divergieren, d.h. sie muessen erst einen pull durchfuehren, wenn sie weiter machen wollen:
   ```bash
   $ git pull
   ```
   Wenn an dieser Stelle eine Error-Meldung angezeigt wird, liegt das daran, dass sie eine Strategie festlegen muessen:
   ```bash
   $ git config pull.rebase false
   ```
   sollte diesen Error beheben.
   Wenn sie dann die Aenderungen auf ihrem **PRIVATEN** remote abspeichern wollen:
   ```bash
   $ git push origin <BRANCH_YOU_WANT_TO_PUSH_TO>
   ```

# Wie laufen die Uebungsaufgaben ab?

Es wird eine **public** repository geben. Die URL ist noch nicht bekannt. Deswegen wieder mit Generics. In den jeweiligen Aufgaben sollte das angegeben sein.

Folgen sie den Schritten und erstellen sie einen privaten Fork dieser Repository.
Diese wird so aussehen: `https://github.com/<USER_NAME>/<REPOSITORY_NAME>`
Gluecklicherweise muessen sie das nur einmal machen.

Als Beispiel gehen wir das Vorgehen fuer die erste Programmieraufgabe durch.

Es wird einen Branch `pa1` geben, in den sie zuerst wechseln muessen.

```bash
$ git checkout pa1
```

Danach muessen sie Aenderungen von dem "upstream" fetchen.

```bash
$ git fetch upstream
$ git rebase upstream/pa1
```

Dann koennen sie Dateien nach der Beschreibung in der Aufgabenstellung erstellen.

**WICHTIG**: Ich werde eine `.gitignore` Datei einrichten, die Dateinamen die nicht exakt der Aufgabenstellung entsprechen fuer die `git` Repository ignorieren wird. D.h. wenn sie die Dateien nicht exakt so benennen wie in der Aufgabenstellung, wird die Abgabe automatisch nicht akzeptiert, d.h. mit 0 Punkten bewertet. Wenn die `.gitignore` Datei von ihnen geaendert wird, wird die Abgabe ebenfalls mit 0 Punkten bewertet werden.
Wenn sie testen wollen, ob ihre Dateien getracked werden, koennen sie das so testen:
```bash
git ls-tree --full-tree --name-only -r <BRANCH_NAME>
```
Wenn die Dateien, die sie abgeben wollen nicht in dieser Liste vorhanden sind, dann haben sie falsche Namen benutzt.

Danach `pushen` sie ihre Loesung auf den `origin` ihres privaten Forks:

```bash
$ git add .
$ git commit -m "Solution to pa1"
$ git push origin pa1
```

Der Punkt in `git add .` steht fuer alle nicht getrackten Dateien oder geaenderte Dateien. Wenn sie einzelne Dateien auswaehlen wollen, koennen sie auch einzeln hinzufuegen.

Sie koennen so viele Commits machen wie sie wollen. Es wird sogar bevorzugt, haeufig commits zu machen, weil diese als Checkpoints benutzt werden koennen, falls sie aus Versehen Aenderungen vornehmen, die sie wieder rueckgaengig machen wollen.

**WICHTIG**: Da ihr Fork **privat** sein wird, muss der Korrektur GitHub Account zu ihrer privaten Repository als **Contributer** hinzugefuegt werden. Der Account wird noch bekannt gegeben. Das kann in den Einstellungen der Repository auf der GitHub Website vorgenommen werden. Der Name des Korrektur-Accounts wird ihnen rechtzeitig mitgeteilt.

Ich werde dann, wenn die Bewertung abgeschlossen ist, in die `README.md` Datei die Punktzahl eintragen und die Aenderungen `pushen`. Dann koennen sie ihre Punktzahl in der `README.md` Datei einsehen.
