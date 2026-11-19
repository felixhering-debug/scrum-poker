# Scrum Poker

Seite zur Aufwandsschätzung von User Stories im agilen Team, ohne Konten und ohne eigenen Server.
Statische Seite (GitHub Pages) plus Firebase Realtime Database für die Live-Synchronisierung.

## Funktionen
- Raum erstellen, Link oder Code teilen, mit Namen beitreten
- Verdeckte Kartenwahl: Die Stimme liegt bis zum Aufdecken im privaten Bereich der Datenbank (nur du kannst sie lesen)
- Aufdecken per Knopf oder automatisch, Durchschnitt, Median, Verteilung, „Einigkeit“
- Story-Liste mit Endergebnis und Summe
- Decks: Fibonacci, modifiziertes Fibonacci, T-Shirt-Größen, Zweierpotenzen
- Zuschauer-Modus, Hell/Dunkel

## Einrichtung (einmalig, ca. 10 Minuten)

### 1. Firebase-Projekt anlegen
1. https://console.firebase.google.com → „Projekt hinzufügen“ (Google Analytics kann aus bleiben).
2. **Build → Authentication → Los geht’s → Anmeldemethode → Anonym → aktivieren.**
3. **Build → Realtime Database → Datenbank erstellen**, Standort z. B. Belgien (europe-west1), „Im gesperrten Modus starten“.
4. Reiter **Regeln**: Inhalt von `database.rules.json` einfügen und **Veröffentlichen**.
5. **Projekteinstellungen (Zahnrad) → Allgemein → Meine Apps → Web-App (`</>`)** hinzufügen. Dort steht ein `firebaseConfig`-Block.

### 2. Konfiguration eintragen
Die Werte aus dem `firebaseConfig`-Block in `config.js` übernehmen (inklusive `databaseURL`). Committen und pushen.

### 3. Veröffentlichen mit GitHub Pages
Repo → **Settings → Pages → Source: Deploy from a branch → Branch `main`, Ordner `/ (root)`**. Nach ca. einer Minute ist die Seite unter `https://<name>.github.io/<repo>/` erreichbar. Diesen Link ans Team geben.

### 4. Domain für die Anmeldung freigeben
Firebase → **Authentication → Einstellungen → Autorisierte Domains**: `<name>.github.io` hinzufügen.

## Grenzen
- Alle, die den Raumcode kennen, können beitreten und Stories ändern (wie beim Vorbild).
- Räume werden nicht automatisch gelöscht; alte Räume kannst du in der Firebase-Konsole unter Realtime Database → `rooms` entfernen.
- Kostenlos im Spark-Tarif, für Teamgrößen völlig ausreichend.
- Ohne eingetragene Konfiguration läuft ein Demo-Modus (nur Tabs im selben Browser).

## Lokal ausprobieren
`python3 -m http.server 8000` im Ordner starten und http://localhost:8000 öffnen (Module laden nicht über `file://`).
