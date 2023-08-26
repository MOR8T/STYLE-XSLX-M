# style-xlsx-m

## ℹ️ About

Style-xlsx-m is a custom [XLSX](https://www.npmjs.com/package/xlsx) (SheetJs) version library with styling from [xlsx-js-style](https://www.npmjs.com/package/xlsx-js-style)


## 🔌 Installation

Install [npm](https://www.npmjs.org/package/style-xlsx-m):

```sh
npm install style-xlsx-m
```

Install [yarn](https://www.npmjs.org/package/style-xlsx-m):

```sh
yarn add style-xlsx-m
```

Install browser:

```html
<script src="dist/xlsx.js"></script>
```

## 🗒 Core API

-   Refer to the [SheetJS](https://sheetjs.com/) documentation for core API reference
-   Current version of sheetjs used: **0.18.5**
-   Over time, will be added new and customized features.


## 🗒 What did I add
-- 1 When you use read or readFile (second put type:'file') your file style-xlsx-m get cells style.

### read or readFile

```js
// STEP 1
const workbook = XLSX.readFile('./example.xlsx',{ cellStyles: true, bookVBA: true });

// STEP 2
let worksheet = [
  "!col":[ { wpx: 10 }, { wpx: 15 }, { wpx:30 } ]
  "!row":[ { hpx: 10 }, { hpx: 15 }, { hpx:30 } ]
  { v: "line\nbreak", t: "s" },
	{ v: "Courier: 24", t: "s" },
	{ v: 45, t: "n" },
	{ v: 2023, t: "n" },
];

// STEP 3
XLSX.utils.book_append_sheet(workbook, worksheet, false, false, sheetname);

// STEP 4
XLSX.writeFile(wb, "style-xlsx-m-example.xlsm");
```

 -- Step 1:
 './excample.xlsx' - is a path to your excel file.
 Second property is a option { cellStyle: true } for get cells style (but now can't get in xls format).

 -- Step 2:
 Create data rows worksheet 

 -- Step 3:
 Get workbook data with style and set workbook.Sheets.sheetname to worksheet

 -- Step 4: 
 Save your file (xlsm and xls are format for save macros)


## 🗒 Style API
-- Method to export file in excel with style get from [xlsx-js-style](https://www.npmjs.com/package/xlsx-js-style) (only function writeFile)

### Cell Style Example

```js
// STEP 1: Create a new workbook
const wb = XLSX.utils.book_new();

// STEP 2: Create data rows and styles
let row = [
  { v: "line\nbreak", t: "s", s: { alignment: { wrapText: true } } },
	{ v: "Courier: 24", t: "s", s: { font: { name: "Courier", sz: 24 } } },
	{ v: "fill: color", t: "s", s: { fill: { fgColor: { rgb: "E9E9E9" } } } },
	{ v: "bold & color", t: "s", s: { font: { bold: true, color: { rgb: "FF0000" } } } },
];

// STEP 3: Create worksheet with rows; Add worksheet to workbook
const ws = XLSX.utils.aoa_to_sheet([row]);
XLSX.utils.book_append_sheet(wb, ws, "readme demo");

// STEP 4: Write Excel file to browser
XLSX.writeFile(wb, "xlsx-js-style-demo.xlsx");
```

### Cell Style Properties

-   Cell styles are specified by a style object that roughly parallels the OpenXML structure.
-   Style properties currently supported are: `alignment`, `border`, `fill`, `font`, `numFmt`.

| Style Prop  | Sub Prop       | Default     | Description/Values                                                                                |
| :---------- | :------------- | :---------- | ------------------------------------------------------------------------------------------------- |
| `alignment` | `vertical`     | `bottom`    | `"top"` or `"center"` or `"bottom"`                                                               |
|             | `horizontal`   | `left`      | `"left"` or `"center"` or `"right"`                                                               |
|             | `wrapText`     | `false`     | `true` or `false`                                                                                 |
|             | `textRotation` | `0`         | `0` to `180`, or `255` // `180` is rotated down 180 degrees, `255` is special, aligned vertically |
| `border`    | `top`          |             | `{ style: BORDER_STYLE, color: COLOR_STYLE }`                                                     |
|             | `bottom`       |             | `{ style: BORDER_STYLE, color: COLOR_STYLE }`                                                     |
|             | `left`         |             | `{ style: BORDER_STYLE, color: COLOR_STYLE }`                                                     |
|             | `right`        |             | `{ style: BORDER_STYLE, color: COLOR_STYLE }`                                                     |
|             | `diagonal`     |             | `{ style: BORDER_STYLE, color: COLOR_STYLE, diagonalUp: true/false, diagonalDown: true/false }`   |
| `fill`      | `patternType`  | `"none"`    | `"solid"` or `"none"`                                                                             |
|             | `fgColor`      |             | foreground color: see `COLOR_STYLE`                                                               |
|             | `bgColor`      |             | background color: see `COLOR_STYLE`                                                               |
| `font`      | `bold`         | `false`     | font bold `true` or `false`                                                                       |
|             | `color`        |             | font color `COLOR_STYLE`                                                                          |
|             | `italic`       | `false`     | font italic `true` or `false`                                                                     |
|             | `name`         | `"Calibri"` | font name                                                                                         |
|             | `strike`       | `false`     | font strikethrough `true` or `false`                                                              |
|             | `sz`           | `"11"`      | font size (points)                                                                                |
|             | `underline`    | `false`     | font underline `true` or `false`                                                                  |
|             | `vertAlign`    |             | `"superscript"` or `"subscript"`                                                                  |
| `numFmt`    |                | `0`         | Ex: `"0"` // integer index to built in formats, see StyleBuilder.SSF property                     |
|             |                |             | Ex: `"0.00%"` // string matching a built-in format, see StyleBuilder.SSF                          |
|             |                |             | Ex: `"0.0%"` // string specifying a custom format                                                 |
|             |                |             | Ex: `"0.00%;\\(0.00%\\);\\-;@"` // string specifying a custom format, escaping special characters |
|             |                |             | Ex: `"m/dd/yy"` // string a date format using Excel's format notation                             |

### `COLOR_STYLE` {object} Properties

Colors for `border`, `fill`, `font` are specified as an name/value object - use one of the following:

| Color Prop | Description       | Example                                                         |
| :--------- | ----------------- | --------------------------------------------------------------- |
| `rgb`      | hex RGB value     | `{rgb: "FFCC00"}`                                               |
| `theme`    | theme color index | `{theme: 4}` // (0-n) // Theme color index 4 ("Blue, Accent 1") |
| `tint`     | tint by percent   | `{theme: 1, tint: 0.4}` // ("Blue, Accent 1, Lighter 40%")      |

### `BORDER_STYLE` {string} Properties

Border style property is one of the following values:

-   `dashDotDot`
-   `dashDot`
-   `dashed`
-   `dotted`
-   `hair`
-   `mediumDashDotDot`
-   `mediumDashDot`
-   `mediumDashed`
-   `medium`
-   `slantDashDot`
-   `thick`
-   `thin`

**Border Notes**

Borders for merged areas are specified for each cell within the merged area. For example, to apply a box border to a merged area of 3x3 cells, border styles would need to be specified for eight different cells:

-   left borders (for the three cells on the left)
-   right borders (for the cells on the right)
-   top borders (for the cells on the top)
-   bottom borders (for the cells on the left)

## 🙏 Thanks

This project is a fork of [SheetJS/sheetjs](https://github.com/sheetjs/sheetjs) combined with code and documentation from
[xlsx-js-style](https://www.npmjs.com/package/xlsx-js-style) (by [brentely](https://www.npmjs.com/~brentely)).

All projects are under the Apache 2.0 License

-   [sheetjs](https://github.com/SheetJS/sheetjs)
-   [js-xlsx](https://github.com/protobi/js-xlsx)
-   [sheetjs-style](https://www.npmjs.com/package/sheetjs-style)
-   [sheetjs-style-v2](https://www.npmjs.com/package/sheetjs-style-v2)
-   [xlsx-js-style](https://www.npmjs.com/package/xlsx-js-style)

## 🔖 License

Please consult the attached [LICENSE](https://github.com/MOR8T/STYLE-XSLX-M/main/LICENSE) file for details. All rights not explicitly
granted by the Apache 2.0 License are reserved by the Original Author.