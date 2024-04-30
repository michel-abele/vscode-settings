[<< Start page](https://github.com/michel-abele/vscode-settings)

# Settings for the Live Sass Compiler

## `liveSassCompile.settings.formats`

Enables different formats to be saved in multiple locations.

| Setting | Type | Default | Notes |
| :------ | :--- | :------ | :---- |
| `format` | expanded `expanded` or compressed `compressed` | `expanded` | output style of the generated file |
| `extensionName` | file extension as a string `string` | `.css` | the extension appended to the output file must end with ".css" |
| `savePath` | memory path as a string `string?` | `null` | `/` path from the root directory of the workspace, `~/` path relative to the Sass/SCSS file |
| `savePathReplacementPairs` | `Record<string, string>?` | `null` | replaces parts of the path relative to the Sass/SCSS file and saves the CSS file there |
| `generateMap` | `boolean?` | `null` | creates a map at format level or prevents it from being created, overwrites the key `liveSassCompile.settings.generateMap` |

### Examples

```json
{
    "liveSassCompile.settings.formats":
    [

        // default - saves the CSS file in the same directory as the Sass/SCSS file
        // source file: layout.scss
        {
            "format": "expanded",
            "extensionName": ".css",
            "savePath": null,
            "savePathReplacementPairs": null
        },
        // target file: layout.css


        // save CSS file compressed
        // source file: layout.scss
        {
            "format": "compressed",
            "extensionName": ".min.css"
        },
        // target file: layout.min.css


        // you can also use it to extend the file name
        // source file: layout.scss
        {
            "extensionName": "-minimal.css"
        }
        // target file: layout-minimal.css


        // storage path from the root directory of the workspace
        // source path: /.scss/layout.scss
        {
            "format": "expanded",
            "extensionName": ".css",
            "savePath": "/public/lib/css",
        },
        // target path: /public/lib/css/layout.css


        // storage path relative to the Sass/SCSS file
        // source path: /.scss/layout.scss
        {
            "format": "expanded",
            "extensionName": ".css",
            "savePath": "~/../public/lib/css",
        },
        // target path: /public/lib/css/layout.css


        // save under the same path, but with changes (root is the root directory of the workspace)
        // source path: /.scss/public/lib/css/layout.scss
        {
            "format": "expanded",
            "extensionName": ".css",
            "savePathReplacementPairs": { "/.scss": "" }
        }
        // target path: /public/lib/css/layout.scss


        // change subdirectory
        // source path: /assets/scss/layout.scss
        {
            "savePathReplacementPairs": { "/scss/": "/styles/" }
        }
        // target path: /assets/styles/layout.css


        // replacement with relative path
        // source path: /src/.scss/layout.scss
        {
            "savePath": "~/..",
            "savePathReplacementPairs": { "/src/.scss/": "/lib/css/" }
        }
        // target path: /lib/css/layout.css


        // replace from multiple source paths
        // source path 1: /scss/layout.scss
        // source path 2: /framework/framework.scss
        {
            "savePathReplacementPairs":
            {
                "/scss/": "/public/lib/css/",
                "/framework/": "/public/lib/css/"
            }
        }
        // target path 1: /public/lib/css/layout.css
        // target path 2: /public/lib/css/framework.css

    ]
}
```

## `liveSassCompile.settings.excludeList`

Excludes files and directories from compilation. The default value is `null`.

### Examples

```json
{
    "liveSassCompile.settings.excludeList":
    [

        // directory with all subdirectories
        "/.vscode/**",

        // all files except file-1.scss and file-2.scss
        "/.scss/*[!(file-1|file-2)].scss",

        // with regular expressions
        "/.scss/[a-z]+-[0-9]+.scss"

    ]
}
```

## `liveSassCompile.settings.includeItems`

Compiles only the specified files and excludes all others. The default value is `null`.

### Examples

```json
{
    "liveSassCompile.settings.includeItems":
    [
        "/.scss/file-1.scss",
        "/.scss/file-2.scss"
    ]
}
```

## `liveSassCompile.settings.partialsList`

Defines the partial files to be compiled and their storage location. The default value is `null`.

### Examples

```json
{
    "liveSassCompile.settings.partialsList":
    [

        // all Sass and SCSS partial files in each directory
        "/**/_*.s[ac]ss",

        // all Sass partial files in a specific directory
        "/.sass/**/_*.sass",

        // all SCSS partial files in a specific directory
        "/.scss/**/_*.scss"
    ]
}
```

## `liveSassCompile.settings.generateMap`

Creates an accompanying map file for each compiled file. Overridden by `generateMap` in `liveSassCompile.settings.formats`. The value is `true` or `false`, the default value is `true`.

### Examples

```json
{
    "liveSassCompile.settings.generateMap`": true
}
```

## `liveSassCompile.settings.autoprefix`

Automatically set autoprefixes for unsupported CSS properties (for example, for `transform` the property `-ms-transform` is also added). Uses the browser list of the Browserslist project to determine browser compatibility. The value is `true`, `false` or a `string`, the default value is `defaults`.

- a `string` overwrites the standard browser to add prefixes for it
- with `false` the autoprefixer is deactivated
- with `true` the autoprefixer either searches for:
    - of the file ".browserslistrc" or,
    - after `"browserslist": [ string ]` in the file package.json
    - if neither is found, the autoprefixer uses the "default settings"

### Examples

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

The autoprefixer automatically finds the target browser properties when a ".browserslistrc" is added to the "/.vscode" directory.

#### Examples

```txt
last 2 version
> 1%
not dead
```

### package.json

The autoprefixer automatically finds the target browser properties when a "package.json" is added to the "/.vscode" directory.

#### Examples

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

### Browser-List

[Browserslist-Projekt](https://browsersl.ist/)

The browser and Node.js version is specified by the following queries (case-insensitive):

- `defaults` - default browser of the "Browserslist" (`> 0.5%, last 2 versions, Firefox ESR, not dead`)
- according to usage statistics:
    - `> 5%` - browser versions selected based on global usage statistics (operators: `<`, `>=` or `<=`)
    - `> 5% in US` - uses usage statistics for the USA (two-digit country code according to ISO-3161-1 Alpha-2)
    - `cover 99.5%` - the most common browsers that provide coverage
    - `cover 99.5% in US` - the most popular browsers that provide coverage in the USA (two-digit country code according to ISO-3161-1 Alpha-2)
- the latest versions
    - `last 2 versions` - the last two versions of any browser
    - `last 2 Chrome versions` - the last two versions of the Chrome browser
- specific browser
    - `Chrome 32` - only the version of the Chrome browser
    - `Firefox > 20` - all versions of the Firefox browser that are higher than version 20
    - `Edge 20-30` - all versions of the Edge browser that are in the version range
    - `Firefox` - the latest version of the Firefox browser
- Period
    - `since 2015` - all browser versions since 2015
    - `last 2 years` - all browser versions of the last two years
- `dead` - Browser without official support or updates for 24 months
- Node.js versions:
    - `node 10` - the latest versions of Node.js 10.x.x
    - `last 2 node versions` - the last two versions of Node.js
    - `current node` - Node.js version currently used by "Browserslist"
    - `maintained node versions` - all Node.js versions that are still maintained by the Node.js Foundation

A query can be denied with a `not` in front of it, for example interpreted as `not dead`: only browsers with official support and current updates.

## `liveSassCompile.settings.showOutputWindowOn`

Defines the logging level from which errors/messages are to be displayed in the output window. The default value is 'Information'.

- `None` - almost no output:
    - if the directory in `liveSassCompile.settings.forceBaseDirectory` is not found or is invalid
- `Error` - compilation error output:
    - error output of `None`
    - if an error or @error occurs in the code
    - if the autoprefixer is faulty or an invalid setting is passed for the browser list
    - if the saving of a file fails
- `Warning` - uncritical problems:
    - error output of `Error`
    - problems with workspace folders
- `Information` - output file information:
    - error output of `Warning
    - when compilation starts
    - when files are created
    - when the monitoring status is changed
- `Debug` - output information for troubleshooting:
    - error output of `Information
    - details of why the files are not compiled
    - details of the files that were processed
- `Trace` - output information on all problems that have occurred:
    - error output from 'Debug
    - many details on the progress of the individual sub-processes

### Examples

```json
{
    "liveSassCompile.settings.showOutputWindowOn": "Debug"
}
```

## `liveSassCompile.settings.watchOnLaunch`

Defines whether the "Live Sass Compiler" should start monitoring directly after the program start or only when it is activated manually. Values are `true` or `false`, the default value is `false`.

### Examples

```json
{
    "liveSassCompile.settings.watchOnLaunch": true
}
```

## `liveSassCompile.settings.compileOnWatch`

Defines whether the "Live Sass Compiler" should compile all files when it starts monitoring. Values are `true` or `false`, the default value is `true`.

### Examples

```json
{
    "liveSassCompile.settings.compileOnWatch": false
}
```

## `liveSassCompile.settings.forceBaseDirectory`

Specifies a subdirectory in which to search. Improves the performance of the compiler if a directory is specified that only contains Sass/SCSS files. No Sass/SCSS files are monitored/compiled outside this directory. The value is `null` or a `string`, the default value is `null`.

If the path is not found or is a file, an error is output. If the path is incorrect, nothing is found or compiled.

This setting affects the root path for `liveSassCompile.settings.includeItems` and `liveSassCompile.settings.excludeList`. A setting to `/assets`, for example, means that both are set relative to `/assets` and not to `/` (root directory of the workspace).

### Examples

```json
{
    "liveSassCompile.settings.forceBaseDirectory": "/.scss/"
}
```

## `liveSassCompile.settings.rootIsWorkspace`

Instructs the compiler that a leading slash `/` is relative to the root directory of the workspace and not to the root directory of the drive. The value is `true` or `false`, the default value is `false`.

### Examples

```json
{
    "liveSassCompile.settings.rootIsWorkspace": true
}
```

## `liveSassCompile.settings.showAnnouncements`

Displays the system message or blocks this when a new version is/was installed. The value is `true` or `false`, the default value is `true`.

### Examples

```json
{
    "liveSassCompile.settings.showAnnouncements": 
}
```
