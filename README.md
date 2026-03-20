#  Support Ticket Workflow (n8n)

![n8n](https://img.shields.io/badge/n8n-Workflow-orange)
![MongoDB](https://img.shields.io/badge/Database-MongoDB-green)
![Status](https://img.shields.io/badge/status-inactive-lightgrey)
![License](https://img.shields.io/badge/license-MIT-blue)

Automatisierter Support-Ticket-Workflow für eingehende E-Mails mit
**n8n**, **Gmail** und **MongoDB**.

------------------------------------------------------------------------

##  Features

-    E-Mail Verarbeitung (Gmail Trigger)
-    Duplikaterkennung (`message_id`)
-    Ticket-Erstellung & Verwaltung
-    Automatische Klassifizierung
-    Priorisierung (Normal / High / Critical)
-    Speicherung in MongoDB
-    Auto-Response an Kunden

------------------------------------------------------------------------

##  Architektur

``` mermaid
flowchart LR
A[Gmail Trigger] --> B[Email Parsing]
B --> C{Duplicate?}
C -->|Yes| D[Ignore]
C -->|No| E{Existing Ticket?}
E -->|Yes| F[Update Ticket]
E -->|No| G[Create Ticket]
G --> H[Store in MongoDB]
F --> H
H --> I[Send Confirmation Email]
```

------------------------------------------------------------------------

##  Klassifizierung

### Kategorien

  Kategorie   Keywords                        Team
  ----------- ------------------------------- -------------
  Login       login, passwort, anmeldung      Support
  Lieferung   versand, paket, tracking        Logistik
  Zahlung     rechnung, paypal, kreditkarte   Buchhaltung
  Allgemein   fallback                        Support

### Priorität

  Keywords                     Priorität
  ---------------------------- -----------
  dringend, sofort, kritisch   High
  system down, totalausfall    Critical
  Standard                     Normal

------------------------------------------------------------------------

##  Datenmodell

### Tickets

-   ticket_id
-   customer_email
-   customer_name
-   subject
-   category
-   team
-   priority
-   status
-   created_at
-   updated_at
-   last_message_at

### Messages

-   ticket_id
-   message_id
-   body
-   subject
-   created_at

------------------------------------------------------------------------

##  Setup

``` bash
# Voraussetzungen
- n8n
- MongoDB
- Gmail OAuth2
```

### Schritte

1.  Workflow importieren
2.  Credentials setzen
3.  Gmail Trigger aktivieren
4.  Workflow starten

------------------------------------------------------------------------

##  Beispiel

``` text
Input: "Mein Login funktioniert nicht"
→ Kategorie: Login
→ Team: Support
→ Ticket wird erstellt
```

------------------------------------------------------------------------

## 🔌 Erweiterungen

-    AI Auto-Reply (OpenAI)
-    Analytics Dashboard
-    Slack Integration
-    Multi-language Support

------------------------------------------------------------------------

## 📄 Lizenz

MIT License

------------------------------------------------------------------------


