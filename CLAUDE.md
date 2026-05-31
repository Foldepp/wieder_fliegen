# CLAUDE.md — Projekt „Wieder fliegen” (interaktives Begleitbuch)

Diese Datei gibt einer künftigen Claude-Session den nötigen Kontext, um an dieser
App weiterzuarbeiten oder eine ähnliche neu zu bauen. Bitte zuerst vollständig lesen.

> **Stand der Doku:** Diese Datei beschreibt die **tatsächliche finale `index.html`**
> (intern früher „Little Butterfly” genannt, jetzt einheitlich „Wieder fliegen”).
> Eine ältere, größere Konzeptversion mit Kapitel-/Modul-System existiert in diesem
> Repo NICHT — falls in alten Notizen davon die Rede ist, gilt diese Datei hier.

-----

## AUFTRAG / HOSTING (zuerst lesen)

Ziel: das Projekt dauerhaft auf **GitHub** sichern und über einen **dauerhaften
öffentlichen Link** verfügbar machen.

1. `index.html` ist bereits korrekt benannt — GitHub Pages liefert automatisch die
   Datei namens `index.html` aus.
1. `CLAUDE.md`, `README.md` und `Konzept-Begleit-Apps.md` bleiben als Doku/Kontext im Repo.
1. **GitHub Pages** aktivieren (Branch `main`, Ordner `/root`) und dem Nutzer den
   fertigen Link nennen (Form: `https://<user>.github.io/<repo>/`).
1. Inhaltlich nur ändern, was ausdrücklich gewünscht ist — die App ist fertig und
   durchgetestet. Designprinzipien und Sicherheits-Leitplanken (unten) immer respektieren.

> **Hinweis zum Layout:** Diese Version arbeitet vollflächig (`100dvh`, fixierte
> Buttonleiste unten) und reserviert KEINEN Platz für ein Hosting-Banner. Wenn später
> über einen Anbieter mit unterem Werbebanner (z. B. tiiny.host) gehostet wird, müsste
> man der `.bottom`-Leiste manuell etwas Abstand nach unten geben.

-----

## Was das hier ist

Eine einzelne, offline-fähige HTML-Datei (`index.html`), die als interaktives
Bilderbuch für Erwachsene funktioniert. Sie begleitet eine Person mit Flugangst
(Hintergrund: komplexe PTBS) durch eine ruhige, sinnbildliche Reise — vom Sitzen im
Gras über das Abheben bis zum Ankommen. Eingebettet sind — bewusst unbenannt —
beruhigende Elemente aus EMDR und Somatic Experiencing, verpackt als Geschichte über
einen Schmetterling (die Nutzerin) und einen Fuchs (ihr Seelenpartner, der sie führt).

Das Geschenk ist von einer dem Empfänger nahestehenden Person; die „verbundene Seele”
(der Fuchs) ist eine subtile, namenlose Repräsentation dieser Verbindung. Verbunden
sind beide durch einen **goldenen Faden** — Verbindung ohne Druck.

## Wichtigste Designprinzipien (nicht verletzen)

1. **Regulation statt Konfrontation.** Die App beruhigt, erdet, orientiert. Sie
   bearbeitet NICHT das Trauma. Bei komplexer PTBS kann zu schnelles „Reinspüren”
   oder unkontrollierte bilaterale Stimulation schaden. Alles bleibt im
   Wohlfühl-Fenster, alles ist überspringbar, nichts erzeugt Druck.
1. **Wahlfreiheit & sanfte Führung zugleich.** Die Nutzerin wird geführt (Seite für
   Seite), aber nichts zwingt sie. Der „Nur Faden”-Knopf ist immer erreichbar.
1. **Subtilität.** Die persönliche Verbindung (Fuchs) und die Methoden (EMDR/SE)
   werden nie benannt. Es soll sich „wahr” anfühlen, nicht therapeutisch oder konstruiert.
1. **Die Nutzerin ist „sie”.** Der Schmetterling ist grammatisch maskulin („der
   Schmetterling”), aber alle Pronomen sind weiblich. Der Fuchs ist „er”.
1. **Ton:** warm, gedeckt, erwachsen. Deutsch. Keine Kindersprache.

## Technische Eckpfeiler

- **Eine einzige `.html`-Datei**, kein externes Laden, voll offline-fähig.
- Reines HTML/CSS/JS in einer IIFE (`(() => { … })()`). Keine Frameworks, keine Build-Tools.
- **Kein `localStorage`, kein Fortschritt-Speichern** in dieser Version — die Reise
  ist kurz (7 Seiten) und wird in einem Zug gelesen. (Falls Persistenz gewünscht wird:
  immer in `try/catch` mit `mem{}`-Fallback, weil manche In-App-Browser schon beim
  bloßen Zugriff auf `localStorage` werfen.)
- Farbpalette als **CSS-Variablen im `:root`** (warmes Creme/Rosé/Pfirsich/Sky/Mint/
  Lavendel/Gold, Tinte/Soft als Textfarben, Fuchs-Orange).
- **Grafik ist reines CSS**, keine externen Bilder und keine SVG-Rauh-Filter: Schmetterling
  (zwei `.wing`, `.body`, `.antenna`), Fuchs (`.fox-head/-body/-tail` via `clip-path`),
  goldener `.thread`, treibende `.cloud`s, `.star`s und ein wandernder `.light-orb`.
- Höhen mit **`dvh`** (dynamic viewport height) und `env(safe-area-inset-*)` für iPhone-Notch.
- Responsiv über zwei Media-Queries: `max-height:700px` (kompakter) und `min-width:760px` (luftiger).

## Struktur der Geschichte (Datenmodell)

Die ganze Erzählung steckt in einem flachen Array `const pages = [ … ]`. Jede Seite:

```
{ chapter:'Kapitelüberschrift', line:'Erzähltext', fox:'Der Fuchs sagt: …',
  prompt:'Beschriftung der Halte-Geste', mode:'thread'|'space'|'light' }
```

- `chapter` — kleine Überschrift oben (Kapitelname)
- `line` — der große Erzählsatz
- `fox` — was der Fuchs auf dieser Seite sagt (Sprechblase unten)
- `prompt` — Text auf dem `gesture-pad` („Finger hier halten” o. Ä.)
- `mode` — steuert die Szene-Animation (siehe unten); wird als Klasse
  `book.mode-<mode>` gesetzt

Die 7 Seiten (in Reihenfolge):

1. **Der Garten am Rand des Himmels** (thread) — Ankommen, Flügel noch geschlossen.
1. **Der goldene Faden** (thread) — Verbindung ohne Druck.
1. **Der Wald der vielen Lichter** (space) — Reizüberflutung, Raum schaffen.
1. **Die Brücke der Schwelle** (thread) — der Übergang, langsam ist ein echtes Tempo.
1. **Der erste Auftrieb** (thread) — das Abheben; Ankerseite des „Nur Faden”-Knopfs.
1. **Das Licht zwischen links und rechts** (light) — ruhiges Augenfolgen (EMDR, entschärft).
1. **Der Ort, der bleibt** (thread) — Landung/Ankommen, der Faden bleibt.

## Die Mechanik (Übungen, unbenannt eingewoben)

- **Halte-Geste (`gesture-pad`):** Finger auf die Fläche legen und halten
  (`pointerdown`/`touchstart` → `startHold`). Dabei bekommt `.scene` die Klassen
  `holding active-motion` (Flügel öffnen sich, Faden pulsiert), und in `holdWords`
  zyklen alle ~950 ms die beruhigenden Worte aus `const words`
  (`"Finger." → "Sitz." → "Jetzt." → "Faden." → "Ich bin da."`). Loslassen → `stopHold`.
  Das ist die Erdungs-/Ressourcen-Geste (Somatic Experiencing): Verbindung + Jetzt.
- **`mode:'light'` (EMDR, entschärft):** ein einzelner `.light-orb` wandert langsam
  links↔rechts (CSS-Animation `travel`). Mit den AUGEN folgen, nichts „tun”. Bewusst
  ohne Belastungsfokus.
- **`mode:'space'`:** Szene für „den Raum wieder weit werden lassen” bei Reizflut.
- **„Nur Faden”-Knopf (`threadOnly` → `threadMode`):** der jederzeit erreichbare
  Ruhe-Anker. Springt direkt auf Seite 5 („Der erste Auftrieb”) mit der schlichten
  Botschaft „Finger. Sitz. Jetzt. Faden.” — das Äquivalent zum „es ist viel”-Moment.
- **Navigation:** `‹ / ›`-Buttons (`prev`/`next`), zusätzlich Pfeiltasten links/rechts;
  Punkt-Indikator (`.page-dots`) zeigt die aktuelle Seite.

## „Verbundene Seele” — wie subtil eingewoben

- Der Fuchs ist auf jeder Seite präsent (Szene unten) und spricht in jeder
  Fuchs-Sprechblase warm und erklärend.
- Der **goldene Faden** liegt sichtbar zwischen Schmetterling und Fuchs — „nicht um sie,
  sondern zwischen sie. Nichts zieht. Etwas bleibt.” Beim Halten pulsiert er stärker.
- Wiederkehrende leise Worte beim Halten: „Finger. Sitz. Jetzt. Faden. Ich bin da.”
- Schluss-Botschaft: „Der Faden bleibt. Nicht weil du ihn brauchst, sondern weil Liebe
  Wege merkt.” — NIE mit Namen, nie ausgesprochen. Fühlbar, nicht erklärt.

## Wichtige Funktionen im Code (alles in der IIFE)

- `buildStars()` — streut die `.star`-Punkte in die Szene.
- `buildDots()` — baut den Seiten-Indikator passend zur aktuellen `index`.
- `render()` — schreibt die aktuelle Seite (chapter/line/fox/prompt/counter), setzt
  `book.className = "book mode-<mode>"`, aktiviert/deaktiviert die Nav-Buttons.
- `go(delta)` — eine Seite vor/zurück (mit Clamping), stoppt laufendes Halten.
- `startHold(event)` / `stopHold()` — Halte-Geste an/aus (Klassen + Wort-Zyklus).
- `threadMode()` — der „Nur Faden”-Sprung auf die Anker-Seite (`index = 4`).

## Alles Persönliche an EINER Stelle

Der gesamte Text steckt im `const pages`-Array (chapter/line/fox/prompt) sowie im
`const words`-Array (die Halte-Worte). Dort wird angepasst, was inhaltlich/persönlich
geändert werden soll. Bewusst ohne Namen/Unterschrift gehalten.

## Layout / Distribution — schmerzhaft gelernte Lektionen

- **iPhone + Telegram/WhatsApp:** Eine lose `.html` lässt sich auf dem iPhone NICHT
  zuverlässig öffnen — iOS zeigt nur eine statische Vorschau (Quick Look), führt kein JS
  aus, und beim Speichern geht die `.html`-Endung oft verloren. Das ist eine Apple-Sperre,
  KEIN Code-Fehler. → **Lösung: über einen Link ausliefern.**
- **Empfohlener Weg:** als Link hosten (GitHub Pages für dauerhaft; Alternativen:
  Netlify Drop am Computer, tiiny.host, Artefakt „Veröffentlichen” in Claude).
  Link in Telegram schicken → ein Tipp → öffnet im echten Browser. Danach „Zum
  Home-Bildschirm hinzufügen” = App-Gefühl + offline.
- Die App ist vollflächig (`100dvh`), die Buttonleiste ist unten fixiert. Es ist KEIN
  Platz für ein Hosting-Banner reserviert (siehe Hosting-Hinweis oben).

## Sicherheits- / Sorgfaltshinweise

- Niemals zu echtem Trauma-Processing drängen. Kein Druck, kein „du musst”.
- Bei Means-Restriction / Krisen-Themen keine Methoden/Details nennen.
- Die App ist eine warme Ergänzung, KEIN Ersatz für Therapie/Notfallplan. Diesen Hinweis
  beim Verschenken mitgeben.
- Beim Verschicken einen entlastenden Satz mitgeben: „Nutz nur, was sich gut anfühlt.”
