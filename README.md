# stylelint-wrap-rem-on-px

A stylelint rule to enforce the usage of custom scss rem function over px units.It can also be used to migrate a project that uses px to use rem.


```css
width: 8px; // error -> can be autofixed to width: rem(8);
height: rem(1.5); // ok
border: 1px solid #000000; // ok
border: 2px solid #000000; // error -> can be autofixed to width: 0.125rem;
@media (max-width: 768px) { display: none }; // ok
background-image: url('https://exapmle.com?size=500pxX500px'); // ok
```

## Installation

```
npm install stylelint-wrap-rem-on-px --save-dev
```
OR
```
yarn add -D stylelint-wrap-rem-on-px --save-dev
```

## Usage

Add it to your stylelint config

```javascript
// .stylelintrc
{
  "plugins": [
    "stylelint-wrap-rem-on-px"
  ],
  "rules": {
    // Declare the rule
    "wrap-rem-on-px/wrap-rem-on-px": true,
    // Declaring the rule with default values is equivalent to:
    // "wrap-rem-on-px/wrap-rem-on-px": [true, { "ignore": "1px", "ignoreFunctions": ["url"] , "ignoreAtRules": ["media"], fontSize: 16 }],
  }
}
```

### SCSS Custom rem function
Add this to your scss code

```
$body-size: 16;

@function rem($value) {
  $new-value: calc($value / $body-size * 1rem);

  @return $new-value;
}
```

## Options

### ignore: Item[]

ignore value check.

Valid value of Item: `propertyName` | `'1px'` | `'${propertyName} 1px'`

Default: ["1px"]

### ignoreFunctions: string[]

ignore check for functions.

Default: ["url"]

### ignoreAtRules: string[]

ignore check for @ rules.

Default: ["media"]

### AutoFixing
This plugin supports auto-fixing. Simply run stylelint with the --fix option. The plugin will then replace all px occurrences with rem.
