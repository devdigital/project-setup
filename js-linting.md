# JavaScript Linting

There are now many solutions for JavaScript linting - eslint is a very extensible, highly configurable plugin based linting engine. 
Standard is built on eslint, but is an opinionated set of pre-baked rules, you cannot override them.
Semistandard is a version of standard which has semi-colons for line endings.

The issues with standard and semi-standard is that neither allow trailing commas. 
If this isn't an issue for you, then I'd recommend not using eslint at all, and instead install the `standard` package.
However, I prefer trailing commas, so this means we need to use eslint directly. Fortunately, standard also comes with an eslint config.

The other issue is prettier - this is a new package which automatically formats your code to be the most readable. 
There are a few eslint rules though that conflict with prettier. Fortunately, there is an eslint config prettier project which turns off these conflicting rules.

Therefore, the recommendation is:
* If you are happy without trailing commas, use the `standard` package and don't use prettier. This is the easiest setup.
* If you wish to have trailing commas, and the ability to override other rules, use eslint with the standard and prettier configs. 

This is more effort, and requires a few more plugins and an `.eslintrc.json` file:

* yarn add `eslint` -D
* yarn add `babel-eslint` -D
* yarn add `prettier` -D
* yarn add `eslint-config-standard` -D
* yarn add `eslint-plugin-standard` -D
* yarn add `eslint-plugin-import` -D
* yarn add `eslint-plugin-promise` -D
* yarn add `eslint-plugin-node` -D
* yarn add `eslint-config-prettier` -D
* yarn add `eslint-plugin-prettier` -D 
* yarn add `eslint-plugin-flowtype` -D (if using Flow)
* yarn add `eslint-plugin-react` -D (if using React)

# .eslintrc.json

```json
{
  "extends": [
    "standard",
    "plugin:flowtype/recommended",
    "plugin:react/recommended",
    "prettier",
    "prettier/flowtype",
    "prettier/react"
  ],
  "plugins": [
    "flowtype",
    "react",
    "prettier"
  ],
  "parserOptions": {
    "ecmaVersion": 2016,
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "env": {
    "es6": true,
    "node": true
  },
  "rules": {
    "prettier/prettier": ["error", {
      "semi": false,
      "trailingComma": "es5",
      "singleQuote": true
    }],
    "no-console": 1
  }
}
```
