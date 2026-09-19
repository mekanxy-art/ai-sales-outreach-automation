# AI-Powered Sales Outreach Automation (n8n)

Ein n8n-Workflow, der personalisiertes B2B-Sales-Outreach End-to-End automatisiert: Du gibst ein Zielunternehmen ein, der Workflow übernimmt den Rest.

## Was der Workflow macht

1. **Manueller Trigger**: Du trägst den Namen oder die Website eines Zielunternehmens ein und startest den Workflow
2. **Kontaktrecherche**: Sucht passende Ansprechpartner über die Apollo-API (mit Fallback-Suche, falls die erste Suche keine Treffer liefert)
3. **KI-Auswahl**: Ein GPT-Modell wählt anhand eines strukturierten Prompts den besten Ansprechpartner (Rolle, Verfügbarkeit von E-Mail/Telefon)
4. **Website-Analyse**: Ruft die Zielwebsite per HTTP ab und extrahiert relevante Inhalte (Titel, Meta-Description, H1, Text)
5. **Personalisierte E-Mail-Generierung**: GPT erstellt sprachabhängig (DE/EN) Anrede, Betreff und einen individuellen Einleitungstext basierend auf echten Website-Inhalten
6. **Versand**: Verschickt die E-Mail automatisch über die Microsoft-Graph-API (Outlook)
7. **Antwort-Tracking**: Prüft in einem separaten Lauf, ob bereits eine Antwort eingegangen ist
8. **CRM-Update**: Schreibt Status und Ergebnisse automatisiert in eine Google-Sheets-Tabelle zurück

## Verwendete Technologien

- **n8n** (Workflow-Automatisierung)
- **OpenAI API** (GPT-Modell für Kontaktauswahl & Textgenerierung)
- **Apollo.io API** (Kontakt- und Firmenrecherche)
- **Microsoft Graph API** (Outlook-Integration für Versand & Antwort-Tracking)
- **Google Sheets API** (CRM-Anbindung, optional für Lead-Import)
- JSON-Verarbeitung, Konditionallogik, Datenbereinigung (JavaScript Code-Nodes)

## Hintergrund

Entstanden aus praktischer Vertriebsautomatisierung während einer Werkstudententätigkeit. Für dieses Repository wurden alle unternehmens- und personenbezogenen Daten (API-Keys, Kontaktdaten, Firmennamen) durch Platzhalter ersetzt.

## Setup

1. n8n-Instanz aufsetzen (Cloud oder self-hosted)
2. Workflow-JSON importieren
3. Eigene Credentials hinterlegen: OpenAI API Key, Apollo API Key, Google Sheets OAuth2, Microsoft Outlook OAuth2
4. Im Node "Edit Fields" den Ziel-Firmennamen/Website eintragen und Workflow manuell starten
