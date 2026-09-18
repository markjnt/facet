---
icon: LiSettings
modified: 2026-09-19 00:42
---
## Einstieg für Agenten
Diese Datei ist verbindlich. Bei Widerspruch zu anderen Notizen gilt sie.

Der Zugriff auf den Vault läuft – lesend wie schreibend – über den **Obsidian-MCP-Server**, nicht über direkten Dateizugriff.

1. Diese Datei lesen – sie regelt Struktur, Format und Vorgehen.
2. [[USER]] lesen – Kontext über die Person, ihre Projekte und Arbeitsweise.
3. Passenden Skill laden (siehe [[#Skills]]), **bevor** die erste Datei geschrieben wird.
4. Nach jeder Änderung die Prüfung aus [[#Prüfung nach jeder Änderung]] durchlaufen.

Verweise in dieser Datei sind Obsidian-Wikilinks: `[[USER]]` meint die Datei `USER.md` im Vault-Root, `[[USER#Projekte]]` deren Abschnitt „Projekte", und `[[#Skills]]` einen Abschnitt in dieser Datei.

## Ordner
- `Notes/`: alle normalen Notizen (flach, keine Unterordner)
- `Periodic/`: Daily `D<TT-MM-JJJJ>`, Weekly `W<KW>-JJJJ` (ISO-Kalenderwoche), Monthly `M<MM>-JJJJ`, Yearly `Y<JJJJ>`
  Beispiele: `D15-09-2026`, `W23-2026`, `M06-2026`, `Y2026`
- `Templates/`: nur Vorlagen, **nie bearbeiten ohne Auftrag**
- `Bases/`: `.base`-Dateien
- `Attachments/`: Bilder, PDFs usw.
- Unklar, wohin? → `Notes/` mit `status: offen` und nachfragen
- Ausnahme: `README.md`, `AGENTS.md` und `USER.md` liegen im Vault-Root, damit sie für den gesamten Vault gelten

## Frontmatter
| Feld         | Pflicht                  | Format / Werte                                                          |
| ------------ | ------------------------ | ----------------------------------------------------------------------- |
| `type`       | ja                       | nur aus der Liste unten                                                 |
| `area`       | ja                       | Bildung, Arbeit, Persönlich, Wissen                                     |
| `project`    | nein                     | nur Werte aus [[USER#Projekte]]                                         |
| `subproject` | nein                     | nur Werte aus [[USER#Subprojekte]]                                      |
| `status`     | nur wenn sinnvoll | offen, in Arbeit, abgeschlossen                                         |
| `tags`       | ja                       | Liste, darf leer sein                                                   |
| `aliases`    | ja                       | Liste, darf leer sein                                                   |
| `icon`       | ja                       | Lucide-Name mit `Li`-Präfix, z. B. `LiStickyNote`                       |
| `created`    | ja                       | `YYYY-MM-DD`, beim Anlegen setzen                                       |
| `modified`   | ja                       | beim Anlegen leer lassen, nie selbst setzen – wird automatisch gepflegt |

Die Root-Dateien `README.md`, `AGENTS.md` und `USER.md` sind vom Schema ausgenommen – sie sind Systemdateien, keine Notizen, und tauchen in keiner Base auf. Ihr Frontmatter wird nicht ergänzt.

Weicht `Templates/` von dieser Datei ab, gilt diese Datei. Die Vorlage wird dann angepasst, nicht umgekehrt.

**`status`**: nur setzen, wenn die Notiz einen Bearbeitungsstand hat – also etwas laufend ist oder abgeschlossen wird. Reine Wissensnotizen (Theorie, Glossar, Referenz, Zitat) lassen das Feld leer, sie sind weder offen noch abgeschlossen. Bei `literatur` gelten stattdessen ungelesen und gelesen.

**Erlaubte `type`-Werte**
- Notizen: modell, setup, anleitung, methodik, auswertung, sprint, theorie, learnings, referenz, bewerbung, log, finanzen, canvas, checkliste, liste, ziel, zitat, gesundheit, idee, glossar, projekt-übersicht, sonstiges
- Eigene Vorlage: literatur, rezept, meeting
- `Periodic/`: daily, weekly, monthly, yearly

Passt für eine Notiz kein Wert, wird ein neuer **vorgeschlagen** statt einen unpassenden zu nehmen – mit einem Satz, wofür er steht und warum die vorhandenen nicht reichen. Nach Zustimmung kommt er in diese Liste **und** in `Templates/Notiz.md`.

**Zusatzfelder je Typ**
- `literatur`: `autor`, `jahr`, `quelle`
- `rezept`: `mahlzeit` (Allgemein, Frühstück, Mittagessen, Abendessen, Snack, Sonstiges)
- `meeting`: `attendees`
- `daily`: `journal: daily`, `journal-date`; kein `area`, kein `status`
- `weekly`/`monthly`/`yearly`: `journal` = weekly/monthly/yearly, dazu `journal-start-date` und `journal-end-date` statt `journal-date`; kein `area`, kein `status`

Neue Werte nur nach Rückfrage.

## Tags
- Kleinschreibung, Wörter mit `-` verbunden
- Umlaute ausschreiben: `ae`, `oe`, `ue`, `ss` (z. B. `ernaehrung`, `vermoegensaufbau`)
- Vor dem Vergeben bestehende Tags prüfen, keine Synonyme neu anlegen
- Tags beschreiben das **Thema**. Status, Typ, Bereich und Projekt stehen in den Properties, nicht als Tag.

## Notiz-Aufbau
**Gibt es für den Typ eine Vorlage in `Templates/`** (literatur, rezept, meeting, daily, weekly, monthly, yearly), gilt deren Aufbau. Die Überschriften der Vorlage bleiben stehen, auch wenn ein Abschnitt leer bleibt. Zusätzliche Abschnitte nur, wenn der Inhalt sie verlangt.

**Für alle anderen Typen** richtet sich der Aufbau nach dem Inhalt, nicht nach einem festen Schema. Eine Gliederung wählen, die zur jeweiligen Notiz passt; bei bestehenden Notizen die vorhandene beibehalten und nicht ungefragt umbauen.

Unabhängig vom Aufbau gilt:
- Überholtes wird **ersetzt, nicht darunter gestapelt**. Eine Notiz darf sich nicht selbst widersprechen.
- Steht eine Entscheidung dahinter, kurz festhalten **was gilt und warum**. Das ist der Teil, der später fehlt.
- Historie gehört nach `Periodic/`, nicht in die Notiz.

**Daily Notes** – ergänzend zur Vorlage:
- Unter `## Projekte` je Projekt eine eigene Überschrift: `### <Projektname> #<projekt-tag>`
- Der Überschriftentext ist exakt der `project`-Wert aus [[USER#Projekte]]
- Der Tag ist derselbe Name in Tag-Schreibweise: klein, Leerzeichen als `-`, Umlaute ausgeschrieben – aus `Hausbau Süd` wird `#hausbau-sued`
- Der Tag ist die einzige Verbindung zu den Projekt-Bases (`file.hasTag(...)`). Fehlt er, taucht die Notiz dort nicht auf.

## Wahrheit & Ownership

**Eine Wahrheit, ein Owner**
- Jedes Thema hat genau **eine** Notiz, die den aktuellen Stand besitzt.
- Andere Notizen **verlinken** darauf und wiederholen ihn nicht.
- Widersprüche werden beim Owner korrigiert, nie in der Kopie.
- **Vor dem Anlegen einer neuen Notiz suchen** – nach Titel *und* Inhalt. Gibt es schon eine zuständige Notiz, wird sie erweitert statt eine zweite anzulegen. Ist unklar, wem das Thema gehört: nachfragen.

**Input ist noch keine Wahrheit**
- `Periodic/` ist Chronik und Beleg: Was an einem Tag passiert ist, bleibt stehen und wird **nicht rückwirkend geändert**.
- `Notes/` besitzt den aktuellen Stand.
- Eine Erkenntnis aus einer Daily Note wird in die zuständige Notiz **übertragen**, nicht dort liegengelassen. Die Daily Note bleibt als Beleg unverändert.

## Bases
- **Standardfall:** kein neues `.base` anlegen, sondern der passenden Area-Base (`Arbeit`, `Bildung`, `Persönlich`, `Wissen`) eine **neue View** hinzufügen.
- **Eigene Base nur**, wenn ein Projekt so groß wird, dass es eine eigene verdient. Anhaltspunkte: mehr als ~25 Notizen, mehrere Subprojekte, oder mehr als ~4 eigene Views in der Area-Base.
- Der Vorschlag für eine eigene Base kommt vom Agenten, die **Entscheidung trifft die Person**. Ungefragt wird keine neue Base angelegt.
- Filter bevorzugt über Properties (`type`, `area`, `project`, `subproject`, `status`), Tags nur ergänzend.
- Bestehende Views nicht umbenennen oder löschen ohne Auftrag.

## Skills
Der Skill wird **vor** dem ersten Schreibvorgang geladen, nicht nachträglich.

| Skill | Wann |
|---|---|
| `obsidian-markdown` | Notizen (`.md`) erstellen oder bearbeiten |
| `obsidian-bases` | Bases (`.base`) erstellen oder bearbeiten |

**Skill nicht verfügbar?** Nicht improvisieren. Stattdessen melden, welcher der hier aufgelisteten Skills fehlt, und fragen, ob trotzdem ohne ihn weitergearbeitet werden soll.

## Bearbeiten
- Bestehende Notizen per **gezielter Teilersetzung** ändern, nicht als Ganzes überschreiben. Vollständig neu schreiben nur bei echtem Umbau der ganzen Notiz. (Beim MCP-Server heißt das meist `patch_note` statt `write_note` im Overwrite-Modus.)
- Geht es nur ums Frontmatter, nur das ändern, statt die Datei neu zu schreiben (meist `update_frontmatter`)
- Keine Templater-Syntax (`<% %>`, `{{VALUE}}`) in fertige Notizen
- Links als `[[Notiz]]`, keine Markdown-Links auf Vault-Notizen
- Keine Notiz löschen oder umbenennen ohne ausdrücklichen Auftrag

## Prüfung nach jeder Änderung
Eine Bearbeitung gilt erst als abgeschlossen, wenn geprüft ist:
- Frontmatter vollständig, `type`/`area`/`status` nur mit erlaubten Werten
- Neue `[[Links]]` zeigen auf existierende Notizen (keine ungewollten leeren Links)
- Neue Tags existieren bereits oder sind bewusst neu angelegt
- Kein Widerspruch zum Owner des Themas, keine zweite Version derselben Wahrheit
- Überholte Angaben wurden ersetzt, nicht darunter gestapelt

Kurz benennen, was geändert wurde, und was davon Annahme statt gesicherter Information ist.

## USER pflegen
- [[USER]] enthält **ausschließlich Kontext über die Person** – keine Aufgaben, Checklisten oder Hinweise, was dort noch fehlt.
- Eine **leere Überschrift** bedeutet: noch nicht gefüllt. Sie wird gefüllt, sobald das Thema ohnehin aufkommt – durch Nachfragen, nicht durch Erfinden. Keine separate Fragerunde nur dafür, und leere Überschriften bleiben stehen, bis es etwas einzutragen gibt.
- Kommt in einem Gespräch dauerhafter Kontext auf, der dort hingehört – neues Projekt, geänderte Rolle, andere Arbeitsweise, wiederkehrende Person –, wird ein **Update vorgeschlagen** und nach Zustimmung eingetragen.
- Abgeschlossene oder überholte Angaben werden ersetzt, nicht angehäuft. [[USER]] bleibt kurz; Ausführliches steht in der zuständigen Notiz und wird nur verlinkt.
- Es gilt dieselbe Grenze wie überall: nur was die Person selbst gesagt hat, keine Schlüsse über sie.

## Wiederkehrende Aufgaben
Fällt auf, dass eine Aufgabe wiederkehrt – gleicher Ablauf zum zweiten oder dritten Mal, oder die Person beschreibt sie als „mache ich regelmäßig" –, wird das **angesprochen** statt stillschweigend jedes Mal neu gemacht:
1. Kurz benennen, welcher Ablauf sich wiederholt.
2. Prüfen, ob es dafür schon einen Skill gibt (vorhandene Skills, sonstige öffentliche Quellen, bekannte Skill-Bibliotheken) – sonst einen eigenen vorschlagen.
3. Die Entscheidung trifft die Person. Ungefragt wird kein Skill erstellt oder installiert.
4. Wird einer übernommen, kommt er oben in die Skill-Tabelle, mit einem Satz, wann er greift.
