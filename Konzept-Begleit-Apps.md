# Konzept: Therapeutische Begleit-Apps als interaktive Geschichten

Eine wiederverwendbare Blaupause, um Apps wie „Wieder fliegen” für ähnliche Themen zu bauen.
Gedacht als Denk- und Bauanleitung — nicht als starres Schema.

-----

## 1. Die Grundidee in einem Satz

Eine evidenzbasierte psychologische Selbstregulations-Übung wird in eine
**herzerwärmende, durchgeführte Geschichte** eingebettet, sodass die Person im richtigen
Moment zur richtigen Übung geführt wird — ohne dass sich etwas nach „Therapie” anfühlt.

## 2. Warum das funktioniert

- **Narrativer Rahmen senkt Widerstand.** Eine Geschichte umgeht die Abwehr, die bei
  direkter „Übung jetzt!”-Aufforderung entsteht. Die Person identifiziert sich mit der
  Hauptfigur und erlebt deren Heilung mit.
- **Ein Begleiter erklärt das „Warum”.** Eine zweite Figur (hier: der Fuchs) erklärt in
  zwei, drei warmen Sätzen, weshalb eine Übung wirkt. Verstehen erhöht Vertrauen und
  Mitmachen — „das bringt wirklich was” statt „ich soll halt atmen”.
- **Zeitliche Führung = richtige Übung im richtigen Moment.** Kapitel sind an reale
  Momente gekoppelt (Abend, Morgen, Wartesituation, Auslöser-Moment, danach). Die Person
  muss nichts auswählen oder sich merken.
- **Werkzeug-Übergabe schafft Übertragbarkeit.** Schlüsselübungen werden der Person
  ausdrücklich „geschenkt” („das hast du jetzt immer bei dir”), damit sie sie auch ohne
  die App in der realen Welt nutzt.

## 3. Die wiederkehrenden Bausteine

### a) Zwei Figuren

- **Hauptfigur = die Nutzerin.** Hat ein Problem, das genau ihres spiegelt (Angst, Trauer,
  Erschöpfung, Selbstzweifel …). Erlebt im Verlauf eine glaubhafte, leise Heilung.
- **Begleiter = Seelenpartner / weise Stimme.** Führt, erklärt, beruhigt. Kann eine subtile,
  unbenannte Repräsentation einer realen, der Person nahestehenden Bezugsperson sein
  (so wird das Geschenk persönlich, ohne kitschig zu werden).
- Ein Symboltier/-bild der Person als Hauptfigur wählen (hier: Schmetterling = Heilung,
  Wiederfliegen). Das Symbol sollte etwas bedeuten, das die beschenkte Person kennt.

### b) Zeitlich getaktete Kapitel

Die Reise an den realen Ablauf des belastenden Ereignisses koppeln. Jedes Kapitel endet mit
einer klaren Ansage: was jetzt tun, wann das Buch wieder aufschlagen. Fortschritt speichern,
damit die Person beim nächsten Öffnen genau dort landet, wo es weitergeht.

### c) Übungen als „Stationen”

Pro Kapitel eine Übung, eingebettet in die Handlung. Immer:

- kurze Erzähl-Einleitung (Handlung führt zur Übung),
- Begleiter erklärt knapp das Warum,
- die interaktive Übung selbst,
- danach Bestätigung/Anker durch den Begleiter.

### d) Notfall-Zugang

Ein immer erreichbarer, ruhiger „es ist viel”-Knopf, der ohne Druck in eine
beruhigende Mini-Übung führt und danach an die Stelle zurückbringt, wo man war.

### e) Subtile Verbindung im Hintergrund

Leise „Hauche” (kurz eingeblendete Sätze) in Schlüsselmomenten, eine kaum sichtbare warme
Aura, ein Begleiter, der „immer mitläuft”. Nie ausgesprochen, nie benannt — fühlbar.

## 4. Sicherheits-Leitplanken (zwingend)

- **Regulieren, nicht prozessieren.** Keine Konfrontation mit dem Trauma, kein tiefes
  „Reinfühlen”, keine ungesteuerte bilaterale Stimulation. Alles bleibt im Wohlfühl-Fenster.
- **Immer überspringbar, nie Druck.** Kein Zwang, keine Timer-Hetze, kein „du musst”.
- **Weiche Formulierungen** bei heiklen Elementen (z. B. „ein Ort, der sich ein bisschen gut
  anfühlt — er muss nicht perfekt sein” statt absolutem „sicherer Ort”).
- **Kein Ersatz für Therapie.** Beim Verschenken klar sagen: warme Ergänzung, kein Ersatz
  für professionelle Hilfe/Notfallplan.
- **Bei Krisen-/Means-Themen** keine Methoden oder Details nennen.
- Wenn man beim Schreiben merkt, dass man eine Anfrage „passend zurechtbiegt”, ist das ein
  Stopp-Signal, kein Grund weiterzumachen.

## 5. Methoden-Werkzeugkasten (sanft nutzbar)

Aus **Somatic Experiencing:**

- Orientierung im Raum / 5-4-3-2-1 (zurück ins Jetzt, gegen Dissoziation & Grübeln)
- Sicherer/Wohlfühl-Ort als Ressource (am besten in Ruhe vorab etablieren)
- langsames Ausatmen (Vagus, Beruhigung)
- ruhiger Fokuspunkt (Blick führt das Nervensystem)

Aus **EMDR (entschärft):**

- bilaterale Stimulation rein zur Beruhigung — Augenfolgen (zügiger) ODER
  Butterfly Tapping (langsamer, Selbstberuhigung). Getrennt halten: andere Tempi/Zwecke.
- NIE mit Belastungsfokus, nie das Trauma anvisieren.

Weitere mögliche Bausteine für andere Themen: CFT (mitfühlende innere Stimme),
ACT (Akzeptanz, Werte), Schema-/IFS-Sprache (innere Anteile, sehr behutsam),
progressive Muskelentspannung, Dankbarkeits-/Ressourcenanker.

## 6. Gestaltung

- **Ton:** warm, gedeckt, erwachsen. Sprache der Zielperson (hier Deutsch).
- **Farben:** gedämpfte Pastelltöne, „edel gedruckt”, nicht bonbonbunt. CSS-Variablen.
- **Bilder:** einfache, handgezeichnet wirkende SVG-Linienillustrationen
  (`filter:url(#rough)` mit feTurbulence/feDisplacementMap). Wenige, warme Farben.
- **Pronomen/Genus** der Hauptfigur an die reale Person anpassen.
- Alles Persönliche an EINER Stelle im Code bündeln (Block „EINSTELLUNGEN”).

## 7. Technische Vorlage

- **Eine einzige offline-fähige `.html`** (kein externes Laden).
- `localStorage` immer in `try/catch`, mit `mem{}`-Fallback (sonst Start-Abbruch in
  In-App-Browsern).
- Fortschritt persistieren (erledigte Kapitel).
- Datenmodell wie in `CLAUDE.md` beschrieben: `CHAPTERS[].pages[]` mit Seitentypen
  story / fox / ex / rest; Übungen als einhängbare Module.
- Layout: `svh` statt `vh`; scrollender Lesebereich oben ausgerichtet; fixierte
  Button-Leiste mit `--banner`-Variable für Hosting-Banner.

## 8. Distribution (besonders iPhone)

- **Nicht** als lose Datei über Messenger an iPhones — iOS führt sie nicht aus
  (Quick-Look-Vorschau, Endungsverlust). Das ist eine Apple-Sperre, kein Code-Fehler.
- **Stattdessen als Link hosten** und den Link schicken: tiiny.host (gut am Handy),
  Netlify Drop (am Computer), GitHub Pages (dauerhaft), oder Claude-Artefakt „Veröffentlichen”.
- Empfängerin tippt den Link → öffnet im echten Browser → optional „Zum Home-Bildschirm
  hinzufügen” = App-Gefühl + offline.
- Hosting-Banner (Gratis-Tarife) per `--banner`-Reserve im Layout berücksichtigen.

## 9. Themen, auf die sich das übertragen lässt

Mit demselben Gerüst denkbar, jeweils Figur/Reise/Übungen anpassen:

- Prüfungs-/Auftrittsangst → Reise bis „auf die Bühne / in den Prüfungsraum”
- Panik in engen Räumen, Fahrstuhl, U-Bahn
- Einschlafhilfe / nächtliches Grübeln
- Trauerbegleitung (sehr behutsam, viel Ressourcenfokus)
- erste Tage nach einer schweren Diagnose / vor einer OP
- Trennungsangst von Kindern (kindgerecht, eigene Leitplanken!)
- Stress-/Reizüberflutung im Alltag (HSP)

Immer gilt: erst die realen Momente der Zielperson kartieren, dann pro Moment die passende
Regulationsübung wählen, dann die Geschichte darum erzählen.