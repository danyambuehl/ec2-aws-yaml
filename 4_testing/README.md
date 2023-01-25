Testing
====

# Ziel

Hier werden einige Scenarios getesten und kurz und knackig in einer Tabelle dokumentiert.

# Testing Übersicht Git Lab Script

| Beschreibung | Test Step | Erwartung | Status | Script Line |
| ---     | ---   | ---     | ---   |  ---   |
| `Fehlermanagement`| Script ohne Argumente Ausführen | Warnhinweis mindestens zwei Argumente benötigt| OK | 7 |
| `Fehlermanagement`| Script mit einem Argumente Ausführen | Warnhinweis mindestens zwei Argumente benötigt| OK | 7 |
| `Fehlermanagement`| Script ohne Argumente Ausführen | Warnhinweis mindestens zwei Argumente benötigt| OK | 7 |
| `Fehlermanagement`| ohne Verbindung zum Internet ausführen | Exit mit Fehler | Fail | 42 |
| `Fehlermanagement`| ohne Verbindung zum Internet ausführen | Log wird geschriben | OK | 52,79,81 - 85 |
| `Fehlermanagement`| Falsches Passwort eingeben | Exit mit Fehler | Fail | 42 |
| `Create`| ohne Folder Structre (n) | keine Folderstructure in Git Repo | OK | 23 |
| `Create`| ohne Folder Structre (n) | README.md existiert | OK | 65 |
| `Create`| mit Folder Structre (y) | Folderstructure in Git Repo ersichtlich | OK | 23 |
| `Create`| Falsche Antwort Folder Structre (W) | Exit mit Error | OK | 23 |
| `Git Ignore`| git.log, git_remote.sh auf lokal Repo suchen | existieren | OK | 75 |
| `Git Ignore`| git.log, git_remote.sh auf remote Repo suchen | existieren nicht | OK | 60 |
| `Git add`| Neues File kann erstellt werde | wird hinzugefügt | OK | 0 |
| `Git commit`| Neues File kann commited werde | wird comited | OK | 0 |
| `Git push`| Neues File kann gepushed werde | wird gepushed | OK | 0 |
| `Git pull`| Neue Files werden heruntergeladen | wird gepulled | OK | 0 |
| `echo`| Link für Repo zugriff funktioniert | Repo wird im Browser angezeigt | OK | 88 |

# Testing Übersicht AWS yaml

| Beschreibung | Test Step | Erwartung | Status | Script Line |
| ---     | ---   | ---     | ---   |  ---   |
| `EnviromentType`| Script ohne EnvironmenType ausführen | t2.nano Instance | OK | 11 |
| `EnviromentType`| Script mit EnvironmenType test ausführen | t2.micro Instance | OK | 29 |
| `EnviromentType`| Script mit EnvironmenType dev ausführen | t2.nano Instance | OK | 24 |
| `ImageId`| Ubuntu 20.04 | EC2 mit Ubuntu 20.04 ist installiert | OK | 36 |
| `Fehlermanagement`| MinLength of KeyPair testen mit keinem Burchstaben  | Exit mit Fehler | OK  | 19 |
| `Fehlermanagement`| MaxLength of KeyPair testen mit 36 Burchstaben  | Exit mit Fehler | OK  | 20 |
| `Fehlermanagement`| Ohne KeyPair Parameter | Fehler | OK | 16 |
| `Fehlermanagement`| MaxLength of KeyPair testen mit 36 Burchstaben  | Exit mit Fehler | OK  | 20 |
| `Security Name`| Erstellen der Sicherheitsgruppe  | Port 80 / 443 und 22 sind offen | OK  | 53-65 |
| `Security Name`| webapp-secuirty-group-dev  | name ändert sich je nach Environment dev / test | OK  | 51 |
|  `Security Name`| Neue Instance Deployed  | existirende Instance wird übernommen | Failed  | 0 |
| `Outpupts`| Public DNS wird angezeigt  | ec2-34-204-7-54.compute-1.amazonaws.com | OK  | 73 |
| `Outpupts`| SSH kann direkt koppiert werden  | verbindung mit Server wird hergestellt | OK  | 79 |


---

> [⇧ **Zurück zur Hauptseite**](/README.md)

---
