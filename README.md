# Books Hugo Module

(intro)

## Requirements

Requirements:
- Go 1.14
- Hugo 0.61.0


## Installation

If not already, [init](https://gohugo.io/hugo-modules/use-modules/#initialize-a-new-module) your project as Hugo Module:

```
$: hugo mod init {repo_url}
```

Configure your project's module to import this module:

```yaml
# config.yaml
module:
  imports:
  - path: github.com/theNewDynamic/hugo-module-tnd-books
```

## Usage

### Some Partial/Feature

#### Examples

### Settings

Settings are added to the project's parameter under the `tnd_books` map as shown below.

```yaml
# config.yaml's example and defaults
params:
  tnd_books:
    authors_key: authors
    date_format: January 2, 2006
    default_author: false
```

#### authors_key (default: authors)

Direct the Front Matter key used to store the list of authors as content files.

#### default_author (default: false)

If set, Books without any Front Matter "authors" will resolve to use this content file as author. This is useful for author site where most books are written by the same author.

#### date_format (default: January 2, 2006)

Whenever the module templates is printing dates, this format in [Go Layout string](https://gohugo.io/functions/format/#gos-layout-string) will will be used.


## theNewDynamic

This project is maintained and love by [thenewDynamic](https://www.thenewdynamic.com).