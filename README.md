# Meetup-Präsentation für Aam Digital

## Anleitung für das Template

### Getting Started

Die Präsentation basiert auf [`reveal.js`](https://github.com/hakimel/reveal.js/), einem Framework für Präsentationen in HTML und Markdown. Framework und Tooling können über `npm i` einfach installiert werden.

Bei der Benutzung sind zwei Befehle essentiell:
- `npm run serve`: Startet einen Entwicklungs-Server, sodass ihr die Präsentation im Browser sehen könnt, die ihr gerade in eurem Editor bearbeitet. Beinhaltet live-reload beim Speichern.
- `npm run deploy`: Die Präsentation wird auf GitHub Pages gehostet, sodass auch dritte ohne installierte Software die Präsentation sehen können: https://liwde.github.io/aam-presentation/. Der Deploy-Befehl aktualisiert diese Version, indem der aktuelle Stand der Präsentation auf den `gh-pages`-Branch des Repository committed und zur origin gepusht wird. Dazu muss der aufrufende Nutzer natürlich Schreibrechte haben.

### Grobstruktur

Die Grund-Struktur der Präsentation ist in der `index.html` enthalten. Im Prinzip ist dort aber nur ein Verweis auf die einzelnen Kapitel, die im Markdown-Format im Ordner `md/` hinterlegt sind. Das schien mir zur Strukturierung am sinnvollsten. Sollten wir aber kompliziertere Bedürfnisse haben, können wir auch einzelne Kapitel in HTML direkt in der `index.html` schreiben. Bilder kommen in den Ordner `img/`.

Als Design habe ich aktuell einfach das Theme `simple` gewählt. Es stehen prinzipiell auch noch andere zur Auswahl, die man [hier](https://revealjs.com/#/themes) ausprobieren kann. Wir können ja dann voten. In `style.css` können wir zudem eigene Zusatz-Styles ablegen, falls das nötig wird.

### Präsentationselemente

- Im einfachsten Fall schreibt ihr mit [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) in die Dateien.
- **Folienüberschriften** würde ich immer als h2 (`##`) setzen, Abschnittsfolien mit h1 (`#`).
- **Folientrenner** in Markdown ist `---`, umgeben mit einer Leerzeile. Zudem hat revel.js eine vertikale Navigation ("Abstieg in Details"). Der Trenner dazu ist `----`.
- **Speaker Notes**: Um Notizen für den Präsentator zu geben, kann eine Leerzeile und der Text `Notes:` ins Markdown geschrieben werden. Ab der Zeile danach bis zum nächsten Folientrenner dürfen dann Notizen stehen.
- **Styling** geht auch in Markdown. Ihr könnt CSS-Klassen annotieren, aber auch die reveal.js-spezifischen `data-`-Attribute; sowohl für das vorangegangene Element als auch die ganze Folie:
    - `- Item 1 <!-- .element: class="fragment" data-fragment-index="2" -->`
    - `<!-- .slide: data-background="#ff0000" -->`
- **Einblendungseffekte** gehen über sogenannte [Fragments](https://github.com/hakimel/reveal.js/#fragments). In der Doku stehen Details, aber im Grunde ist es super einfach (wie oben schon im Beispiel dargestellt) ins Markdown einbindbar.

### Shortcuts während der Präsentation

- Mausrad, Pfeiltasten: Folien weiterblättern
- <kbd>F</kbd>: Öffne Vollbildansicht
- <kbd>O</kbd>: Öffne Übersichtsseite
- <kbd>S</kbd>: Öffne Speaker-Popup mit Notizen usw.
