# echo. journal & language practice

Meine Motivation: Mentale Klarheit und Sprachbegeisterung vereinen.
Ich schreibe seit einem Jahr regelmäßig Tagebuch und habe dabei gemerkt, wie sehr mir das Festhalten meiner Gedanken hilft, den Kopf freizubekommen und neue Perspektiven zu gewinnen. Gleichzeitig interessiere ich mich nicht nur für Programmiersprachen, sondern auch für gesprochene Sprachen. Doch im Alltag bleibt oft wenig Zeit, beides konsequent zu verfolgen.

Genau hier setzt meine App-Idee an: echo. journal & language practice kombiniert das schnelle, unkomplizierte Festhalten von Einträgen mit dem spielerischen Lernen einer Fremdsprache. So möchte ich die Vorteile des Tagebuchschreibens – Klarheit, Reflexion, mentale Stärkung – mit dem Reiz des Sprachenlernens verknüpfen und Menschen eine einfache Möglichkeit bieten, beide Routinen gleichzeitig zu pflegen.

**echo. Schreiben, Lernen, Wachsen – jeden Tag.**

echo. journal & language practice ist eine App, die Menschen dabei unterstützt, gute Gewohnheiten wie Tagebuchschreiben und das Lernen von Fremdsprachen gleichzeitig zu etablieren. Sie richtet sich an alle, die **persönliche Reflexion** und **sprachliche Weiterentwicklung** in ihren Alltag integrieren möchten – auch wenn wenig Zeit zur Verfügung steht.

Die App schafft eine motivierende Umgebung, in der Nutzer ihre Gedanken festhalten und dabei spielerisch eine Fremdsprache lernen können. Was echo. besonders macht, ist die Kombination von intuitivem Tagebuchschreiben mit Echtzeit-Übersetzungen und einem KI-Assistenten, der als zukünftiges Ich personalisiert wird, um gezielt zu motivieren und zu unterstützen. So wird Lernen inspirierend, effizient und individuell.


## Design

| App Landing             | Sign In               | Onboarding             | Home List            |
|--------------------------|-----------------------|------------------------|----------------------|
| ![App Landing](./img/App%20Landing.png) | ![Sign In](./img/Sign%20In.png) | ![Onboarding](./img/echo%20onboarding.png) | ![Home List](./img/Home%20List.png) |
| New Entry               | PopUp Change/Delete | Language Picker        | Entry Translated     |
| ![New Entry](./img/New%20Entry.png) | ![PopUp Change/Delete](./img/PopUp%20Change%20Delete.png) | ![Language Picker](./img/Language%20Picker.png) | ![Entry Translated](./img/Entry%20translated.png) |
| Record Audio            | Entry from Audio     | Entry Inspiration      | PopUp Echo Message   |
| ![Record Audio](./img/Record%20Audio.png) | ![Entry from Audio](./img/Entry%20from%20Audio.png) | ![Entry Inspiration](./img/Echo%20Entry%20Inspiration.png) | ![PopUp Echo Message](./img/PopUp%20Echo%20Message.png) |


## Features

### Höchste Priorität (MVP)
- [x] Tagebuch Einträge Übersicht
- [x] Tagebuch Einträge Favoritenliste
- [x] Tagebuch Schreiben und speichern
- [x] Sprachübersetzung und Wörterbuchfunktion in relevante Sprachen
- [x] echo's inspirierende Schreibanregungen
- [x] Zielsprache auswählen und wechseln
- [x] User Profil und generelle Settings
### Mittlere Priorität
- [x] Echtzeit-Übersetzung
- [x] Text-zu-Sprache für gelernte Sprache
- [x] Voice to Text
- [x] Schreib-Statistik
- [x] Schreib-Tracker
- [x] TopWord-Identifikation und Übersetzung
### Niedrige Priorität
- [ ] Bilder aus Fotos einfügen
- [ ] Orte aus Maps einfügen
- [ ] Audio Records to Text
- [ ] Vokabel-Highlighting
+ siehe unten -> Ausblick


## Technischer Aufbau


#### Projektaufbau

	echo.journal/
	├── 1 Models/
	│   ├── JournalEntry.swift
	│   └── User.swift
	├── 2 ViewModels/
	│   └── JournalViewModel.swift
	├── 3 Views/
	│   ├── JournalListView.swift
	│   ├── JournalEntryView.swift
	│   └── LoginView.swift
	├── 4 Repositories/
	│   ├── JournalRepository.swift
	│   └── TranslationRepository.swift
	├── 5 Services/ 
	│   ├── FirebaseService.swift
	│   └── TranslationService.swift
	└── 6 Ressources & Config/
    	├── Assets
     	├── Plist
    	└── Localizable

	Der Datenfluss geht dabei typischerweise: View <-> ViewModel <-> Repository <-> Services <-> External APIs

##### 1. Models

Aufgabe: Definieren die Datenstrukturen/Objekte der App (z.B. JournalEntry, User)

Erste Structs: Tagebucheintrag (JournalEntry), Nutzerprofil (User), ggf. weitere: (Übersetzung (Translation), Schreibanregung (Prompt), ...).
 
##### 2. ViewModels

Aufgabe: Verwalten den UI-State und die UI-Logik, verbinden Views mit Repositories

Erste ViewModels:

- Tagebucheinträge anzeigen und verwalten (JournalViewModel: loadEntries(), addEntry(), deleteEntry()).
 
- ggf. weitere (Benutzerinformationen verwalten (UserViewModel: loadUser(), updateLanguage()), Texte übersetzen (TranslationViewModel: translateText()), Schreibanregungen laden (PromptViewModel: loadDailyPrompt()).

##### 3. Views

Aufgabe: Zeigen die UI an und nehmen User-Interaktionen entgegen

Erste Views:

- Eintragsübersicht (JournalListView),
 
- Detaileintrag neu/änderbar (JournalEntrylView),
 
- Login (LoginView),
 
- ggf. weitere (Sprache auswählen (LanguagePickerView), Einstellungen (SettingsView), ...).

##### 4. Repositories

Aufgabe: Implementieren die Business-Logik und koordinieren verschiedene Services

Erste Repos: 

- Einträge laden und speichern (JournalRepository: fetchEntries(), saveEntry(), deleteEntry()),
  
- Texte übersetzen (TranslationRepository: translateText()),
  
- ggf. weitere (Benutzerprofil verwalten (UserRepository: getUser(), updateUser()), Schreibanregungen bereitstellen (PromptRepository: getDailyPrompt(), fetchPrompts(), ...).

##### 5. Services

Aufgabe: Kümmern sich um die technische Kommunikation mit externen APIs/Systemen (Firebase, LibreTranslate)

Services:

- Firebase-Kommunikation (FirebaseService),
 
- LibreTranslateAPI-Docker-Container-Kommunikation (TranslationService).


#### Datenspeicherung

##### Welche Daten?

- Tagebucheinträge: Titel, Inhalt, Datum, Tags, Sprache, Übersetzungen.
 
- Benutzerprofile: Name, Zielsprache, Einstellungen.
 	
- Übersetzungen: Quelltext, Zieltext, Sprache.
   
- Schreibanregungen: Tägliche Inspirationen.

##### Wo und wie?

- Firebase: Hauptspeicherort für alle Daten.

- Warum Firebase? Echtzeit-Synchronisation zwischen Geräten. Skalierbarkeit und einfache Integration. Möglichkeit für späteren Offline-Support.

Swift Data wird derzeit nicht genutzt, kann ggf. später für einen Offline-Modus integriert werden.



#### API Calls

LibreTranslate API: Übersetzung von Texten in die Zielsprache. Übersetzen von Tagebucheinträgen und Bereitstellen von Synonymen/Definitionen.

Warum: Open-Source-Lösung ohne Lizenzkosten, sofern Selbst-gehostet. Unterstützt mehrere Sprachen.

**Extra Herausforderung:** Selbst-Hosten ist wegen der API notwendig, da die Nutzung über die LibreTranslate Server nicht kostenfrei ist! -- **Docker Container** 

Zukünftige API-Erweiterungen für bspw echos' KI-Funktionen können später ergänzt werden.


## Ausblick

1.	**Summaries & Reviews**
Automatisierte Wochen- oder Monatsrückblicke anhand der geschriebenen Einträge – so lassen sich persönliche Fortschritte im Journalen und Sprachenlernen übersichtlich nachvollziehen.

2.	**Community-Features**
Einbindung anderer Nutzer: Gemeinsame Journals, das Austauschen von Einträgen oder Feedback und damit ein soziales Element, das zusätzlich motiviert.

3.	**Echo-Assistent Customizing**
Das virtuelle Zukunfts-Ich lässt sich individuell anpassen und personalisieren: Nutzer können die Persönlichkeit, den Schreibstil oder sogar den Avatar ihres KI-Assistenten definieren.

