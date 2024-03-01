[Startseite](https://github.com/michel-abele/vscode-settings)

# Einstellungen für den Live Sass Compiler

## `liveSassCompile.settings.formats`

Ermöglicht das Speichern unterschiedlicher Formate, an mehreren Orten.

| Einstellung | Type | Standard | Anmerkungen |
| :---------- | :--- | :------- | :---------- |
| `format` | erweitert `expanded` oder komprimiert `compressed` | `expanded` | Ausgabestil der erzeugten Datei |
| `extensionName` | Dateierweiterung als Zeichenkette `string` | `.css` | die an die Ausgabedatei angehängte Endung muss mit ".css" enden |
| `savePath` | Speicherpfad als Zeichenkette `string?` | `null` | `/` Pfad vom Wurzelverzeichnis des Arbeitsbereichs (Workspace), `~/` Pfad relativ zur Sass/SCSS-Datei |
| `savePathReplacementPairs` | `Record<string, string>?` | `null` | ersetzt Teile des Pfads relativ zur Sass/SCSS-Datei und speichert dort die CSS-Datei |
| `generateMap` | `boolean?` | `null` | erstellt k/eine Map auf Formatebene, überschreibt den Schlüssel `liveSassCompile.settings.generateMap` |

### Beispiele

```json
{
    "liveSassCompile.settings.formats":
    [

        // Standard - speichert die CSS-Datei im selben Verzeichnis wie die Sass/SCSS-Datei
        // Quelldatei: layout.scss
        {
            "format": "expanded",
            "extensionName": ".css",
            "savePath": null,
            "savePathReplacementPairs": null
        },
        // Zieldatei: layout.css


        // CSS-Datei komprimiert speichern
        // Quelldatei: layout.scss
        {
            "format": "compressed",
            "extensionName": ".min.css"
        },
        // Zieldatei: layout.min.css


        // man kann auch den Dateinamen damit erweitern
        // Quelldatei: layout.scss
        {
            "extensionName": "-minimal.css"
        }
        // Zieldatei: layout-minimal.css


        // Speicherpfad vom Wurzelverzeichnis des Arbeitsbereichs
        // Quellpfad: /.scss/layout.scss
        {
            "format": "expanded",
            "extensionName": ".css",
            "savePath": "/public/lib/css",
        },
        // Zielpfad: /public/lib/css/layout.css


        // Speicherpfad relativ zur Sass/SCSS-Datei
        // Quellpfad: /.scss/layout.scss
        {
            "format": "expanded",
            "extensionName": ".css",
            "savePath": "~/../public/lib/css",
        },
        // Zielpfad: /public/lib/css/layout.css


        // unter gleichem Pfad, aber mit Veränderungen, speichern (Wurzel ist das Wurzelverzeichnis des Arbeitsbereichs)
        // Quellpfad: /.scss/public/lib/css/layout.scss
        {
            "format": "expanded",
            "extensionName": ".css",
            "savePathReplacementPairs": { "/.scss": "" }
        }
        // Zielpfad: /public/lib/css/layout.scss


        // Unterverzeichnis ändern
        // Quellpfad: /assets/scss/layout.scss
        {
            "savePathReplacementPairs": { "/scss/": "/styles/" }
        }
        // Zielpfad: /assets/styles/layout.css


        // Ersetzung mit relativen Pfad
        // Quellpfad: /src/.scss/layout.scss
        {
            "savePath": "~/..",
            "savePathReplacementPairs": { "/src/.scss/": "/lib/css/" }
        }
        // Zielpfad: /lib/css/layout.css


        // Ersetzen aus mehreren Quellpfaden
        // Quellpfad 1: /scss/layout.scss
        // Quellpfad 2: /framework/framework.scss
        {
            "savePathReplacementPairs":
            {
                "/scss/": "/public/lib/css/",
                "/framework/": "/public/lib/css/"
            }
        }
        // Zielpfad 1: /public/lib/css/layout.css
        // Zielpfad 2: /public/lib/css/framework.css

    ]
}
```

## `liveSassCompile.settings.excludeList`

Schließt Dateien und Verzeichnisse vom kompilieren aus. Der Standardwert ist `null`.

### Beispiele

```json
{
    "liveSassCompile.settings.excludeList":
    [

        // Verzeichnis mit allen Unterverzeichnissen
        "/.vscode/**",

        // alle Dateien außer datei-1.scss und datei-2.scss
        "/.scss/*[!(datei-1|datei-2)].scss",

        // mit regulären Ausdrücken
        "/.scss/[a-z]+-[0-9]+.scss"

    ]
}
```

## `liveSassCompile.settings.includeItems`

Kompiliert nur die angegebenen Dateien und schließt alle anderen aus. Der Standardwert ist `null`.

### Beispiele

```json
{
    "liveSassCompile.settings.includeItems":
    [
        "/.scss/datei-1.scss",
        "/.scss/datei-2.scss"
    ]
}
```

## `liveSassCompile.settings.partialsList`

Definiert die zu kompilierenden Teildateien und deren Ablageort. Der Standardwert ist `null`.

### Beispiele

```json
{
    "liveSassCompile.settings.partialsList":
    [

        // alle Sass- und SCSS-Teildateien in jedem Verzeichnis
        "/**/_*.s[ac]ss",

        // alle Sass-Teildateien in einem bestimmten Verzeichnis
        "/.sass/**/_*.sass",

        // alle SCSS-Teildateien in einem bestimmten Verzeichnis
        "/.scss/**/_*.scss"
    ]
}
```

## `liveSassCompile.settings.generateMap`

Erstellt eine begleitende Map-Datei für jede kompilierte Datei. Wird von `generateMap` in `liveSassCompile.settings.formats` überschrieben. Der Wert ist `true` oder `false`, der Standardwert ist `true`.

### Beispiele

```json
{
    "liveSassCompile.settings.generateMap`": true
}
```

## `liveSassCompile.settings.autoprefix`

Automatisches setzen von Autoprefixes für nicht unterstützte CSS-Eigenschaften (für `transform` wird zum Beispiel auch die Eigenschaft `-ms-transform` hinzugefügt). Verwendet die Browser-Liste des Projekts "Browserslist" für die Bestimmung der Browser-Kompatibilität. Der Wert ist `true`, `false` oder ein `string`, der Standardwert ist `defaults`.

- ein `string` überschreibt die Standard-Browser um Präfixe dafür hinzuzufügen
- bei `false` wird der Autoprefixer deaktiviert
- bei `true` sucht der Autoprefixer entweder nach:
    - der Datei ".browserslistrc" oder,
    - nach `"browserslist": [ string ]` in der Datei package.json
    - wenn keines von beiden gefunden wird, verwendet der Autoprefixer die "Standardeinstellungen"

### Beispiele

```json
{
    "liveSassCompile.settings.autoprefix":
    [
        "last 2 version",
        "> 1%",
        "not dead"
    ]
}
```

### .browserslistrc

Der Autoprefixer findet die Ziel-Browser-Eigenschaften automatisch, wenn eine ".browserslistrc" dem Verzeichnis "/.vscode" hinzugefügt wird.

#### Beispiele

```txt
last 2 version
> 1%
not dead
```

### package.json

Der Autoprefixer findet die Ziel-Browser-Eigenschaften automatisch, wenn eine "package.json" dem Verzeichnis "/.vscode" hinzugefügt wird.

#### Beispiele

```json
{
    "browserslist":
    [
        "last 2 version",
        "> 1%",
        "not dead"
    ]
}
```

### Browser-Liste

[Browserslist-Projekt](https://browsersl.ist/)

Die Browser- und Node.js-Version wird durch folgende Abfragen angegeben (Groß- und Kleinschreibung wird nicht berücksichtigt):

- `defaults` - Standardbrowser der "Browserslist" (`> 0.5%, last 2 versions, Firefox ESR, not dead`)
- nach Nutzungsstatistiken:
    - `> 5%` - Browser-Versionen, die anhand der globalen Nutzungsstatistiken ausgewählt werden (Operatoren: `<`, `>=` oder `<=`)
    - `> 5% in US` - verwendet Nutzungsstatistiken für die USA (zweistelliger Ländercode nach ISO-3161-1 Alpha-2)
    - `cover 99.5%` - die gängigsten Browser, die eine Abdeckung bieten
    - `cover 99.5% in US` - die gängigsten Browser, die in den USA eine Abdeckung bieten (zweistelliger Ländercode nach ISO-3161-1 Alpha-2)
- die letzten Versionen
    - `last 2 versions` - die letzten zwei Versionen beliebiger Browser
    - `last 2 Chrome versions` - die letzten zwei Versionen des Chrome-Browser
- bestimmter Browser
    - `Chrome 32` - nur die Version des Chrome-Browser
    - `Firefox > 20` - alle Versionen des Firefox-Browser, die höher als die Version 20 sind
    - `Edge 20-30` - alle Versionen des Edge-Browser, die sich im Versionsbereich befinden
    - `Firefox` - die letzte Version des Firefox-Browser
- Zeitraum
    - `since 2015` - alle Browser-Versionen seit 2015
    - `last 2 years` - alle Browser-Versionen der letzten zwei Jahre
- `dead` - Browser ohne offiziellen Support oder Updates seit 24 Monaten
- Node.js-Versionen:
    - `node 10` - die neuesten Versionen von Node.js 10.x.x
    - `last 2 node versions` - die letzten zwei Versionen von Node.js
    - `current node` - Node.js-Version, die derzeit von "Browserslist" verwendet wird
    - `maintained node versions` - alle Node.js-Versionen, die noch von der Node.js Foundation gepflegt werden

Mit einem `not` vorangestellt kann man eine Abfrage verneinen, zum Beispiel gedeutet `not dead`: nur Browser mit offiziellen Support und aktuellen Updates.

## `liveSassCompile.settings.showOutputWindowOn`

Legt die Protokollierungsstufe fest, ab der Fehler/Meldungen im Ausgabefenster anzeigt werden sollen. Der Standardwert ist `Information`.

- `None` - fast keine Ausgabe:
    - wenn das Verzeichnis in `liveSassCompile.settings.forceBaseDirectory` nicht gefunden wird oder ungültig ist
- `Error` - Kompilierungsfehler ausgegeben:
    - Fehlerausgabe von `None`
    - wenn ein Fehler oder @error in im Code auftritt
    - wenn der Autoprefixer fehlerhaft ist oder eine ungültige Einstellung für die Browser-Liste übergeben wird
    - wenn das Speichern einer Datei fehlschlägt
- `Warning` - unkritische Probleme ausgeben:
    - Fehlerausgabe von `Error`
    - Probleme mit Arbeitsbereichsordnern
- `Information` - Dateiinformationen ausgeben:
    - Fehlerausgabe von `Warning`
    - wenn die Kompilierung beginnt
    - wenn Dateien erzeugt wurden
    - wenn der Überwachungsstatus geändert wird
- `Debug` - Informationen für die Fehlersuche ausgeben:
    - Fehlerausgabe von `Information`
    - Angaben darüber, warum die Dateien nicht kompiliert werden
    - Details zu den Dateien, die verarbeitet wurden
- `Trace` - Informationen zu allen aufgetretenen Problemen ausgeben:
    - Fehlerausgabe von `Debug`
    - viele Details zum Fortschritt der einzelnen Teilprozesse

### Beispiele

```json
{
    "liveSassCompile.settings.showOutputWindowOn": "Debug"
}
```

## `liveSassCompile.settings.watchOnLaunch`

Legt fest, ob der "Live Sass Compiler" direkt nach dem Programmstart die Überwachung starten soll, oder erst wenn er händisch aktiviert wird. Werte sind `true` oder `false`, der Standardwert ist `false`.

### Beispiele

```json
{
    "liveSassCompile.settings.watchOnLaunch": true
}
```

## `liveSassCompile.settings.compileOnWatch`

Legt fest, ob der "Live Sass Compiler" alle Dateien kompilieren soll, wenn er mit der Überwachung beginnt. Werte sind `true` oder `false`, der Standardwert ist `true`.

### Beispiele

```json
{
    "liveSassCompile.settings.compileOnWatch": false
}
```

## `liveSassCompile.settings.forceBaseDirectory`

Legt ein Unterverzeichnis fest, in dem gesucht werden soll. Verbessert die Leistung des Compilers, wenn ein Verzeichnis angegeben wird, dass nur Sass/SCSS-Dateien enthält. Außerhalb dieses Verzeichnisses werden keine Sass/SCSS-Dateien überwacht/kompiliert. Der Wert ist `null` oder ein `string`, der Standardwert ist `null`.

Wenn der Pfad nicht gefunden wird oder eine Datei ist, wird ein Fehler ausgegeben. Wenn der Pfad falsch ist, wird nichts gefunden oder kompiliert.

Diese Einstellung wirkt sich auf den Wurzelpfad für `liveSassCompile.settings.includeItems` und `liveSassCompile.settings.excludeList` aus. Eine Einstellung zum Beispiel auf `/assets`, bedeutet, dass beide relativ `/assets` und nicht zu `/` (Wurzelverzeichnis des Arbeitsbereichs) ansetzen.

### Beispiele

```json
{
    "liveSassCompile.settings.forceBaseDirectory": "/.scss/"
}
```

## `liveSassCompile.settings.rootIsWorkspace`

Weist den Compiler an, dass ein führender Schrägstrich `/` relativ zum Wurzelverzeichnis des Arbeitsbereichs und nicht zum Wurzelverzeichnis des Laufwerks ist. Der Wert ist `true` oder `false`, der Standardwert ist `false`.

### Beispiele

```json
{
    "liveSassCompile.settings.rootIsWorkspace": true
}
```

## `liveSassCompile.settings.showAnnouncements`

Zeigt die Systemmeldung an oder blockiert dies, wenn eine neue Version installiert wird/wurde. Der Wert ist `true` oder `false`, der Standardwert ist `true`.

### Beispiele

```json
{
    "liveSassCompile.settings.showAnnouncements": 
}
```
