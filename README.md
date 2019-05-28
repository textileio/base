# base
Base files we use to configure our repositories

## Install

Use [HTTPie](https://httpie.org/) via the Terminal to download the base files:

``` shell
# for all projects
http -d https://raw.githubusercontent.com/textileio/base/master/.editorconfig
http -d https://raw.githubusercontent.com/textileio/base/master/.gitignore

# for projects that have javascript/typescript/html
http -d https://raw.githubusercontent.com/textileio/base/master/.eslintignore
http -d https://raw.githubusercontent.com/textileio/base/master/.prettierignore

#  open the package.json and copy the relevant parts
open https://github.com/textileio/base/blob/master/package.json
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
