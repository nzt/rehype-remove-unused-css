# Rehype remove unused css

Rehype plugin to remove unused stylesheet with uncss

## Installation

    npm install rehype-remove-unused-css

## Usage

Say `example.html` looks as follows;

```html
<html>
    <head>
        <style>
            .one {
                font-size: 1em;
            }
            .two {
                font-size: 2em;
            }
        </style>
    </head>
    <body>
        <p class="one">example</p>
    </body>
</html>
```

...and `example.js` like this:

```javascript
const vfile = require("to-vfile")
const report = require("vfile-report")
const unified = require("unified")
const rehype = require("rehype-parse")
const stringify = require("rehype-stringify")
const removeUnusedCss = require("rehype-remove-unused-css")

unified()
    .use(rehype)
    .use(removeUnusedCss)
    .use(stringify)
    .processSync(vfile.readSync("example.html"), (err, file) => {
        console.error(report(err || file))
        console.log(String(file))
    })
```

Now, running `node example` yields:

```html
<html>
    <head>
        <style>
            .one {
                font-size: 1em;
            }
        </style>
    </head>
    <body>
        <p class="one">example</p>
    </body>
</html>
```

## API

### `rehype().use(removeUnusedCss[, options])`

Remove unused stylesheet.

- `options` is same as options of [uncss](https://github.com/uncss/uncss)

### Security

Use of rehype-remove-unused-css should be safe to use as JSDOM should be safe to use. When in doubt, use rehype-sanitize.

### License

MIT &copy; TANIGUCHI Masaya
