# base
Base files we use to configure our repositories

## Install

### Install the appropriate editor plugins

#### VSCode

- Formatting / Linting
    - https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig
    - https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint
    - https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode
    - https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint
    - https://marketplace.visualstudio.com/items?itemName=timonwong.shellcheck
    - https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint
- Sharing
    - https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare-pack
- Languages
    - https://marketplace.visualstudio.com/items?itemName=ms-vscode.Go
    - https://marketplace.visualstudio.com/items?itemName=vsmobile.vscode-react-native

Customise your eslint configuration with the following from @balupton's [configuration file](https://github.com/balupton/dotfiles/blob/master/.scripts/users/balupton/vscode/settings.json)

``` json
{
	"editor.detectIndentation": false,
	"editor.formatOnSave": true,
	"editor.insertSpaces": false,
	"editor.renderControlCharacters": true,
	"editor.renderIndentGuides": true,
	"eslint.alwaysShowStatus": true,
	"eslint.autoFixOnSave": true,
	"eslint.enable": true,
	"eslint.run": "onType",
	"files.trimTrailingWhitespace": true,
	"html.format.enable": true,
	"json.format.enable": true,
	"prettier.semi": false,
	"prettier.singleQuote": true,
	"prettier.useTabs": true,
	"typescript.format.enable": true,
	"typescript.suggest.completeFunctionCalls": true,
	"typescript.tsdk": "./node_modules/typescript/lib",
	"typescript.updateImportsOnFileMove.enabled": "always",
	"typescript.validate.enable": true,
	"markdownlint.config": {
		"MD007": {
			"indent": 4
		},
		"MD012": false,
		"MD022": false,
		"MD030": false,
		"MD032": false,
		"MD034": false
	},
	"eslint.validate": [
		"javascript",
		"javascriptreact",
		"typescript",
		"typescriptreact"
	],
	"eslint.options": {
		"ignorePattern": "**/*.d.ts"
	},
	"[json]": {
		"editor.defaultFormatter": "esbenp.prettier-vscode"
	},
}
```

#### GoLand

- Formatting / Linting
    - https://plugins.jetbrains.com/plugin/10456-prettier
    - https://www.jetbrains.com/help/go/configuring-code-style.html#editorconfig

### Download

Use [HTTPie](https://httpie.org/) via the Terminal to download the appropraite base files:

``` shell
# for all projects
http -d https://raw.githubusercontent.com/textileio/base/master/.editorconfig
http -d https://raw.githubusercontent.com/textileio/base/master/.gitignore

# for web projects (projects that are mostly html/javascript/typescript)
http -d https://raw.githubusercontent.com/textileio/base/master/.eslintignore
http -d https://raw.githubusercontent.com/textileio/base/master/.prettierignore
```

### Setup

#### On Go/Java Projects

On go projects we want to run prettier on everything, but ignore the errors.

``` bash
npx prettier --write "./**" 2> /dev/null || true
```

#### On Web Projects

Uninstall the old dependencies:

``` bash
rm tslint.json
npm uninstall tslint tslint-react
```

Install the dependencies:

``` bash
# javascript/typescript/react projects
npm i -D prettier eslint eslint-config-bevry eslint-config-prettier eslint-plugin-prettier
    
# typescript projects
npm i -D @typescript-eslint/eslint-plugin @typescript-eslint/parser

# react projects
npm i -D eslint-plugin-react eslint-plugin-react-hooks @types/react
```

Add the eslint/prettier script to say `package.json:scripts` as `build` or `lint` or whatever.

``` bash
eslint --fix --ext .mjs,.js,.jsx,.ts,.tsx .
```

Add the following to `package.json` which enables our rules:

``` json
{
  "eslintConfig": {
    "extends": [
      "bevry"
    ],
    "parserOptions": {
      "ecmaVersion": 6,
      "sourceType": "module",
      "ecmaFeatures": {
        "jsx": true
      }
    }
  },
  "prettier": {
    "semi": false,
    "singleQuote": true
  }
}
```

For typescript projects, you may wish to add the following to make the rules more compatible with typescript conventions:

``` json
{
  "eslintConfig": {
    "rules": {
      "no-undefined": 0,
      "default-case": 0
    }
  }
}
```

## About

Refer to these discussion threads:

- [Add an `.editorconfig` to each repository #3
](https://github.com/textileio/meta/issues/3)
- [Adopt prettier on all repositories #4](https://github.com/textileio/meta/issues/4)
- [Convert TSLint to ESLint #35](https://github.com/textileio/meta/issues/35)
- [Adopt shellcheck for linting all bash/shell scripts #5](https://github.com/textileio/meta/issues/5)
- [Adopt awesome-travis/surge to deploy repositories to static hosting #6](https://github.com/textileio/meta/issues/6)

Inspired by [bevry/base](https://github.com/bevry/base)
