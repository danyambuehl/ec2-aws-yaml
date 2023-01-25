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

# Testing Übersicht AWS Script

| Beschreibung | Test Step | Erwartung | Status | Script Line |
| ---     | ---   | ---     | ---   |  ---   |
| `Fehlermanagement`| Script ohne Argumente Ausführen | Warnhinweis mindestens zwei Argumente benötigt| OK | 7 |
| `Fehlermanagement`| Script mit einem Argumente Ausführen | Warnhinweis mindestens zwei Argumente benötigt| OK | 7 |
| `Fehlermanagement`| Script ohne Argumente Ausführen | Warnhinweis mindestens zwei Argumente benötigt| OK | 7 |
| `Fehlermanagement`| ohne Verbindung zum Internet ausführen | Exit mit Fehler | Fail | 42 |
| `Fehlermanagement`| ohne Verbindung zum Internet ausführen | Log wird geschriben | OK | 52,79,81 - 85 |

---

web: [`Weblnk`](https://www.linkl.com),
---

> [⇧ **Zurück zur Hauptseite**](/README.md)

---
