# Hari Growth Dashboard

Statisches Dashboard (`index.html` + `data.json`) auf GitHub Pages, für Handy und Laptop. `data.json` ist die Quelle der Wahrheit. Nur belegte Metriken eintragen; unbekannte Werte bleiben unverändert.

## Wie Hari freigibt

Im Panel **„Wartet auf Hari“** erscheinen Ideen mit `status: "draft"` und Aufgaben mit `status: "pending"`.

Ideen-Status: `draft | approved | scheduled | filming | posted` – `scheduled` = liegt in Buffer/Queue mit Uhrzeit (Vienna) + Post-ID in `notes`. Das Missions-Board zeigt aktive Ideen (draft/approved/scheduled/filming) zuerst und lässt sich per Status-Chip filtern.

1. **Freigeben** setzt die Idee in der lokalen Vorschau auf `approved`; **Ablehnen** entfernt sie. **Erledigt** setzt eine Aufgabe auf `done`.
2. **data.json herunterladen** erzeugt die Datei mit den vorgemerkten Änderungen. Die Klicks sind bis zum Commit ungespeichert; GitHub Pages kann die Quelldatei nicht selbst schreiben.
3. Vor dem Ersetzen mit der neuesten `data.json` im GitHub-Repo vergleichen. Bei parallelen Agent-Updates ausschließlich die eigenen Statusänderungen bzw. entfernten Drafts in die neueste Datei übertragen; Agent-Felder und neue Ideen erhalten.
4. Die geprüfte `data.json` im Repo committen. Nach dem GitHub-Pages-Update ist die Freigabe dauerhaft sichtbar.

Alternativ direkt `data.json` im Repo bearbeiten: die gewünschte Draft-Idee anhand ihrer `id` finden und nur `status` auf `"approved"` setzen; beim Ablehnen das betreffende Draft-Objekt aus `ideas` entfernen. Für eine erledigte Aufgabe nur `status` auf `"done"` setzen. Anschließend committen.

## Aufgaben-Schema

`data.schema.json` validiert `tasks`. Ohne tatsächliche Aufgaben bleibt `tasks: []`. Jedes Task-Objekt benötigt:

- `type`: `"google_identity"`, `"upload_ok"` oder `"other"`.
- `title`: Text mit mindestens einem Zeichen außer Leerraum.
- `status`: `"pending"` oder `"done"`.
- Optional `link`: absolute HTTP(S)-Adresse.
- Optional `id`: eindeutiger, stabiler Text, empfohlen für die Zuordnung bei parallelen Änderungen.

Weitere Agent-Felder sind erlaubt und bleiben erhalten. Das Panel dokumentiert Entscheidungen; es startet weder Uploads noch Änderungen an Buffer/Studio. Religiöse Content-Regeln bleiben unverändert.
