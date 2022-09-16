# datalist-css: HTML5 datalist CSS styling

This JavaScript module allows you to style HTML5 `<datalist>` and child `<option>` elements using standard CSS. Load `demo.html` to view the demonstration page.

HTML5 `<datalist>` elements cannot be styled. To achieve it, this 1.5Kb script overrides the browser's default behavior; *the `<datalist>` effectively becomes a `<div>`*. It's little different to using a JavaScript-based autocomplete control since all display and input handling must be managed manually.

This script was primarily modified for personal use, so there might be better solutions to this issue like accessible custom autocompletes.

This is a forked version of the original with some slight differences:
- Improved accessibility by having tab behave like in the default `<datalist>`.
- Added listeners to the parent container of the datalist to handle closing of the `<datalist>` when clicking somewhere else in the page and when tabbing out of it.


## Usage

Load the script anywhere in your HTML page as an ES6 module:

```html
<script type="module" src="[path_to_library]/dist/datalist-css.min.js"></script>
```

Create a wrapper element and a standard text `<input>` immediately followed by a `<datalist>` containing one or more `<option>` elements, e.g.

```html
<div class="datalist-wrapper">
  <label for="browser">browser:</label>
  <input list="browserdata" id="browser" name="browser" size="50" autocomplete="off" />

  <datalist id="browserdata">
    <option>Brave</option>
    <option>Chrome</option>
    <option>Edge</option>
    <option>Firefox</option>
    <option>Internet Explorer</option>
    <option>Opera</option>
    <option>Safari</option>
    <option>Vivaldi</option>
    <option>other</option>
  </datalist>
</div>
```

Note:

1. The input's `list` attribute must reference the `id` of the `<datalist>`.
1. Use `autocomplete="off"` to ensure the input does not show previously values entered by the user.
1. Only the `<option>value</option>` format can be used (`<option value="value" />` is an empty element which cannot be styled).

Add CSS to style all `<datalist>` and `<option>` elements, e.g.

```css
datalist {
  position: absolute;
  top: calc(100% + 2px);
  max-height: 200px;
  border: 2px solid black;
  border-radius: 4px;
  overflow-y: auto;
}

datalist option {
  font-size: 14px;
  padding: 4px 8px;
  cursor: pointer;
}

datalist option:hover, datalist option:focus {
  color: #fff;
  background-color: #036;
  outline: 0 none;
}
```


## Building

The minified script is built using [Rollup.js](https://rollupjs.org/) and [Terser](https://terser.org/). Install globally:

```bash
npm install -g rollup rollup-plugin-terser
```

If not done already, set `NODE_PATH` to the `npm` root folder so global modules can be used within any project directory, e.g.

```bash
export NODE_PATH=$(npm root --quiet -g)
```

Build using:

```bash
npm run build
```
