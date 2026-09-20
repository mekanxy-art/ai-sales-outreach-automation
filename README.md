[README.md](https://github.com/user-attachments/files/32440909/README.md)
# 🤖 AI-Powered Sales Outreach Automation (n8n)

![n8n](https://img.shields.io/badge/n8n-Workflow-orange)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Personal%20Project-lightgrey)

Ein n8n-Workflow, der personalisiertes B2B-Sales-Outreach End-to-End automatisiert: Du gibst ein Zielunternehmen ein, der Workflow übernimmt Kontaktrecherche, Textgenerierung, Versand und Antwort-Tracking.

> ⚠️ Alle unternehmens- und personenbezogenen Daten (API-Keys, Kontaktdaten, Firmennamen, Credential-IDs) wurden für dieses Repository durch Platzhalter ersetzt.

---

## Inhaltsverzeichnis

- [Features](#features)
- [Wie es funktioniert](#wie-es-funktioniert)
- [Verwendete Technologien](#verwendete-technologien)
- [Setup](#setup)
- [Nutzung](#nutzung)
- [Hinweis zur Ausführbarkeit](#hinweis-zur-ausführbarkeit)
- [Hintergrund](#hintergrund)

---

## Features

- 🔎 Manuelle Eingabe eines Zielunternehmens als einziger nötiger Startpunkt
- 🧠 KI-gestützte Auswahl des besten Ansprechpartners (Rolle, E-Mail-/Telefon-Verfügbarkeit)
- 🌐 Automatische Website-Analyse zur Personalisierung der Erstansprache
- ✍️ Sprachadaptive Textgenerierung (Deutsch/Englisch) basierend auf realen Website-Inhalten
- 📧 Automatischer Versand über Microsoft Outlook (Graph API)
- 📬 Antwort-Tracking: prüft automatisiert, ob bereits eine Reaktion eingegangen ist
- 📊 Rückschreiben aller Ergebnisse in eine Google-Sheets-CRM-Tabelle

## Wie es funktioniert

1. **Manueller Trigger** — Firmenname oder Website wird im Node "Edit Fields" eingetragen, Workflow wird gestartet
2. **Kontaktrecherche** — Primäre Apollo-API-Suche nach relevanten Rollen (z. B. Head of E-Commerce, CRM Manager); Fallback-Suche nach Founder/CEO/Managing Director, falls die erste Suche keine Treffer liefert
3. **KI-Auswahl** — Ein GPT-Modell bewertet die gefundenen Kontakte anhand eines strukturierten Prompts und wählt den fachlich passendsten Ansprechpartner mit verfügbarer E-Mail
4. **Website-Analyse** — Die Zielwebsite wird per HTTP-Request abgerufen; Titel, Meta-Description, H1 und Fließtext werden extrahiert
5. **Sprach- und Textgenerierung** — Ein Scoring-System (DACH-Signale wie `.de`/`.at`/`.ch`, "GmbH", Länderfeld etc.) bestimmt die Sprache; GPT erstellt darauf basierend Anrede, Betreff und einen personalisierten Einleitungstext ohne erfundene Fakten
6. **Versand** — Die fertige E-Mail wird über die Microsoft-Graph-API direkt an den Kontakt verschickt
7. **Antwort-Tracking** — Ein separater Lauf prüft über die Outlook-API, ob bereits eine Antwort im Postfach eingegangen ist
8. **CRM-Update** — Status (z. B. "Reachout gemacht", "Antwort erhalten") wird automatisiert in Google Sheets zurückgeschrieben

## Verwendete Technologien

| Technologie | Zweck |
|---|---|
| **n8n** | Workflow-Automatisierungsplattform |
| **OpenAI API** | Kontaktauswahl & personalisierte Textgenerierung |
| **Apollo.io API** | Kontakt- und Firmenrecherche |
| **Microsoft Graph API** | Outlook-Versand & Antwort-Tracking |
| **Google Sheets API** | CRM-Anbindung |
| JavaScript (Code-Nodes) | JSON-Verarbeitung, Konditionallogik, Datenbereinigung |

## Setup

1. n8n-Instanz aufsetzen (Cloud oder self-hosted)
2. Workflow-JSON importieren
3. Eigene Credentials hinterlegen:
   - OpenAI API Key
   - Apollo API Key
   - Google Sheets OAuth2
   - Microsoft Outlook OAuth2
4. Platzhalter im Workflow durch eigene Werte ersetzen (`YOUR_APOLLO_API_KEY`, `YOUR_GOOGLE_SHEET_ID`, `YOUR_CREDENTIAL_ID`)
5. Workflow im n8n-Editor öffnen, um die Node-Struktur und Logik einzusehen (Ausführung erfordert eigene Zugänge, siehe unten)

## Nutzung

Im Node **"Edit Fields"** den Ziel-Firmennamen oder die Website eintragen, Workflow manuell ausführen — der Rest läuft automatisch durch.

## Hinweis zur Ausführbarkeit

Dieser Workflow ist eine **n8n-Konfigurationsdatei**, kein eigenständiges Programm. Um ihn selbst auszuführen, benötigst du:

- eine n8n-Instanz (Cloud oder self-hosted)
- eigene API-Zugänge zu OpenAI, Apollo.io, Google Sheets und Microsoft Outlook

Aus Datenschutzgründen sind in diesem Repository keine aktiven Zugänge oder Live-Demos hinterlegt. Der Workflow wurde produktiv im Vertriebsalltag eingesetzt und ist hier ausschließlich als technisches Showcase der Logik und Integration hinterlegt.

## Hintergrund

Entstanden aus praktischer Vertriebsautomatisierung während einer Werkstudententätigkeit. Dieses Repository dient als technisches Showcase-Projekt zur Demonstration von API-Integration, KI-gestützter Automatisierung und Workflow-Orchestrierung.

---

*Persönliches Projekt — lizenziert unter der MIT-Lizenz, siehe [LICENSE](./LICENSE).*
