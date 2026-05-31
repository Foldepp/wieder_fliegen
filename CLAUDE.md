# CLAUDE.md — Projekt „Wieder fliegen” (interaktives Begleitbuch)

Diese Datei gibt einer künftigen Claude-Session den nötigen Kontext, um an dieser
App weiterzuarbeiten oder eine ähnliche neu zu bauen. Bitte zuerst vollständig lesen.

-----

## AUFTRAG AN CLAUDE CODE (zuerst lesen)

Der Nutzer möchte dieses Projekt dauerhaft auf **GitHub** sichern und über einen
**dauerhaften öffentlichen Link** verfügbar machen. Konkret:

1. Lege ein neues GitHub-Repository an (z. B. `wieder-fliegen`).
1. Benenne die mitgelieferte `Wieder_fliegen.html` in **`index.html`** um (oder
   committe sie zusätzlich als `index.html`). GitHub Pages liefert automatisch die
   Datei namens `index.html` aus.
1. Lege auch `CLAUDE.md` und `Konzept-Begleit-Apps.md` mit ins Repo (Doku/Kontext).
1. Aktiviere **GitHub Pages** (Branch `main`, Ordner `/root`) und nenne dem Nutzer
   den fertigen Link (Form: `https://<user>.github.io/<repo>/`).
1. **WICHTIG — Banner-Anpassung:** GitHub Pages hat KEIN Werbebanner (anders als
   tiiny.host, wofür die App zuletzt gebaut wurde). Setze deshalb im CSS im `:root`
   den Wert `--banner:120px` auf `--banner:0px`. Dann sitzt die fixierte
   „weiter”-Leiste wieder bündig unten, ohne reservierten Banner-Abstand.
   (Falls später doch wieder über tiiny gehostet wird: zurück auf ~120px.)
1. Sonst inhaltlich NICHTS ändern — die App ist fertig und durchgetestet. Bitte die
   Designprinzipien und Sicherheits-Leitplanken weiter unten respektieren.

-----

-----

## Was das hier ist

Eine einzelne, offline-fähige HTML-Datei (`Wieder_fliegen.html`), die als
interaktives Bilderbuch für Erwachsene funktioniert. Sie begleitet eine Person mit
Flugangst (Hintergrund: komplexe PTBS) durch die Reise vom Vorabend bis nach der
Landung. Eingebettet sind — bewusst unbenannt — Übungen aus EMDR und Somatic
Experiencing, verpackt als Geschichte über einen Schmetterling (die Nutzerin) und
einen Fuchs (ihr Seelenpartner, der durch die Übungen führt und erklärt, warum sie wirken).

Das Geschenk ist von einer dem Empfänger nahestehenden Person; die „verbundene Seele”
(der Fuchs) ist eine subtile, namenlose Repräsentation dieser Verbindung.

## Wichtigste Designprinzipien (nicht verletzen)

1. **Regulation statt Konfrontation.** Die App beruhigt, erdet, orientiert. Sie
   bearbeitet NICHT das Trauma. Bei komplexer PTBS kann zu schnelles „Reinspüren”
   oder unkontrollierte bilaterale Stimulation schaden. Alles bleibt im
   Wohlfühl-Fenster, alles ist überspringbar, nichts erzeugt Druck.
1. **Wahlfreiheit & sanfte Führung zugleich.** Die Nutzerin wird geführt (sie weiß
   immer, welches Kapitel wann dran ist), aber nichts zwingt sie. „es ist viel” ist
   immer erreichbar.
1. **Subtilität.** Die persönliche Verbindung (Fuchs) und die Methoden (EMDR/SE)
   werden nie benannt. Es soll ssich „wahr” anfühlen, nicht therapeutisch oder
   konstruiert.
1. **Die Nutzerin ist „sie”.** Der Schmetterling ist grammatisch maskulin („der
   Schmetterling”), aber alle Pronomen sind weiblich. Der Fuchs ist „er”.
1. **Ton:** warm, gedeckt, erwachsen. Deutsch. Keine Kindersprache.

## Technische Eckpfeiler

- **Eine einzige `.html`-Datei**, kein externes Laden, voll offline-fähig.
- Kein `localStorage`-Zugriff ohne `try/catch` (manche In-App-Browser werfen sonst
  Fehler beim bloßen Zugriff → ganzer Start bricht ab). Es gibt ein `mem{}`-Fallback.
- Fortschritt wird unter `sf_done` gespeichert (erledigte Kapitel-IDs).
- Farbpalette als CSS-Variablen im `:root` (warmes Creme/Clay/Rosé/Mauve/Teal,
  „Anthropic-Homepage, nur femininer”).
- Handgezeichnet wirkende SVG-Illustrationen mit `filter:url(#rough)`
  (feTurbulence + feDisplacementMap). Alle in `const ILLUS = {…}`.
- Übungen sind „Module” (`#mod-breath`, `#mod-fly`, `#mod-here`, `#mod-still`,
  `#mod-haven`, `#mod-safe`, `#mod-tap`), die per `mountModule()` in die jeweilige
  Buchseite eingehängt werden.

## Struktur der Geschichte (Datenmodell)

Die ganze Erzählung steckt in `const CHAPTERS = [...]`. Jedes Kapitel:

```
{ id:'cN', icon:'🌙', when:'Wann im echten Leben', title:'…', pages:[ …Seiten… ] }
```

Seitentypen:

- `{t:'story', h:'<p>…</p>', img:'illusKey', soar:true?}` — Erzählung (optional Bild/Flug-Animation)
- `{t:'fox',   h:'…'}` — der Fuchs spricht (Sprechblase)
- `{t:'ex',    ex:'breath'|'fly'|'here'|'still'|'haven'|'safe'|'tap', lead:'…'}` — Übung
- `{t:'rest',  h:'…', last:true?}` — Kapitelende; sagt, was jetzt zu tun ist & wann wiederkommen

Reihenfolge entspricht dem echten Zeitverlauf:

1. 🌙 Der Abend davor — sicherer Ort + Atem (Einschlafen)
1. 🌅 Der Morgen — 5-4-3-2-1 Erden (als Werkzeug gg. Gedankenkarussell übergeben)
1. 🌫️ Im Gewimmel — ruhiger Punkt (Flughafen/Menschenmenge)
1. 🪶 Das Abheben — EMDR (Augenfolgen, zügig) + Butterfly Tapping (Werkzeug, langsam)
1. ☁️ Über den Wolken — „Worte, die mitfliegen”
1. 🌿 Die Landung — Abschluss, glückliches Wiedersehen

## Die Übungen (Mechanik)

- **breath** (Atem): Schmetterlingsflügel öffnen/schließen, 4 s ein / kurz halten / 6 s aus.
- **safe** (Sicherer Ort): geführte Vorstellung in 7 Schritten, durchtippen. Nur geführt,
  KEIN Texteingabefeld (bewusste Entscheidung).
- **here** (5-4-3-2-1): Sinne-Countdown, durchtippen. Wird als „behaltbares Werkzeug” übergeben.
- **still** (ruhiger Punkt): ruhiger, pulsierender Lichtpunkt zum Blick-Ausruhen.
- **fly** (EMDR): EIN wandernder Lichtpunkt links↔rechts, ~0,85 s, mit den AUGEN folgen.
  Wichtig: die früher vorhandenen zwei Tap-Felder wurden ENTFERNT (liefen nicht synchron).
- **tap** (Butterfly Tapping): zwei „Hände” leuchten abwechselnd, langsamer Takt ~1,1 s,
  Hände auf Schultern (überkreuzt) ODER Oimproberschenkel. Als Werkzeug „für wenn die Angst
  kommt” übergeben — bewusst getrennt von EMDR, weil anderes Tempo/Zweck.

## „Verbundene Seele” — wie subtil eingewoben

- Eröffnung: ein warmer Abend, der Fuchs wartet und „spürt, dass sie ihn heute braucht”.
- Durchgehend: der Fuchs läuft beim Flug unten am Boden mit, verliert sie nie aus dem Blick;
  über den Wolken sehen sie einander → „Ich bin nicht allein. Ich war es nie.”
- Leise „Hauche” (whisper()) in Schlüsselmomenten: „Ich bin hier.” / „Atme — ich halt dich.”
- Eine kaum sichtbare warme Aura (CSS, `auraPulse`) pulsiert im Hintergrund.
- NIE mit Namen, nie ausgesprochen. Der Empfänger soll es fühlen, nicht lesen.

## Wichtige Funktionen im Code

- `beginBook()` → `startIntro()` → Intro-Seiten → `openMap()`
- `openMap()` zeigt „Die Reise” (Kapitel-Übersicht); `suggestedChapter()` bestimmt das
  nächste offene Kapitel; das aktuelle leuchtet, erledigte haben ✓.
- `openChapter(i)` / `renderPage()` / `pageNext()` / `pagePrev()`
- `markDone(id)` & `markCurrentChapterDone()` — Kapitel gilt als erledigt, sobald die
  Übung gesehen/gemacht wurde (NICHT erst auf der letzten Seite — das war ein Bug).
  WICHTIG: `pageNext()` markiert bei `t:'ex'`; breath/here/fly markieren zusätzlich beim
  Abschluss, damit „Handy nach der Übung weglegen” (Abend) korrekt zählt.
- `sosOpen()` / `sosClose()` — der „es ist viel”-Ruhemoment (führt in Atem, kehrt zurück).
- `resetBook()` — setzt Fortschritt zurück, zurück aufs Cover.

## Layout / Distribution — schmerzhaft gelernte Lektionen

- **iPhone + Telegram/WhatsApp:** Eine lose `.html` lässt sich auf dem iPhone NICHT
  zuverlässig öffnen — iOS zeigt nur eine statische Vorschau (Quick Look), führt kein JS
  aus, und beim Speichern geht die `.html`-Endung oft verloren. Das ist eine Apple-Sperre,
  KEIN Code-Fehler. → **Lösung: über einen Link ausliefern.**
- **Empfohlener Weg:** als Link hosten (tiiny.host hat am iPhone gut funktioniert;
  Alternativen: Netlify Drop am Computer, GitHub Pages, Artefakt „Veröffentlichen” in Claude).
  Link in Telegram schicken → ein Tipp → öffnet im echten Browser. Danach „Zum
  Home-Bildschirm hinzufügen” = App-Gefühl + offline.
- **tiiny.host-Banner:** Die Gratis-Version blendet unten ein Banner ein. Deshalb sitzt die
  fixierte Button-Leiste (`.bottombar`) per `position:fixed; bottom:var(--banner)` ÜBER dem
  Banner. `--banner` (im `:root`) steuert den Abstand in EINER Zahl (aktuell 120px).
  Wenn ohne Banner gehostet wird, `--banner` auf 0 setzen.
- **`.book`** ist scrollbar und oben ausgerichtet (`justify-content:flex-start`), nicht
  zentriert — sonst quillt langer Inhalt oben UND unten raus und der Button verschwindet.
- Höhen mit `svh` (small viewport height) verwenden, nicht `vh`.

## Test-Schalter & aktueller Stand

`const SHOW_RESET` (im Block „EINSTELLUNGEN”) blendet einen schwebenden Test-„von vorn”-Knopf
ein. **Aktuell `false`.** Der dauerhafte „↺ Die Geschichte von vorn” steht ohnehin als
sichtbarer Button auf der Reise-Übersicht (Map) und ist für die Nutzerin gedacht.

`--banner` im `:root` steht aktuell auf **120px** (für tiiny.host-Banner). Für GitHub Pages
auf **0px** setzen (siehe Auftrag oben).

## Alles Persönliche an EINER Stelle

Im `<script>` ganz oben unter „EINSTELLUNGEN”: Titel, Untertitel, MESSAGES (Worte über den
Wolken), FOX_WHISPERS, CALM_FOX, SAFE_STEPS, sowie der Erzähltext in CHAPTERS. Bewusst ohne
Namen/Unterschrift gehalten.

## Sicherheits- / Sorgfaltshinweise

- Niemals zu echtem Trauma-Processing drängen. Kein Druck, kein „du musst”.
- Bei Means-Restriction / Krisen-Themen keine Methoden/Details nennen.
- Die App ist eine warme Ergänzung, KEIN Ersatz für Therapie/Notfallplan. Diesen Hinweis
  beim Verschenken mitgeben.
- Beim Verschicken einen entlastenden Satz mitgeben: „Nutz nur, was sich gut anfühlt.”