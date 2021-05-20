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

### Editions and bindings

Each book lists an array of editions identified by a binding. 

#### Edition front matter

```yaml
title: "L.A. Confidential"
description: "_L.A. Confidential_ is an epic crime novel that stands as a steel-edged time capsule—Los Angeles in the 1950s, a remarkable era defined in dark shadings."
editions:
- binding: paperback
  isbn: 9780446674249
  date: 1997-09-01T15:53:00.000Z
  publisher: Grand Central Publishing
  cover_image: /uploads/la_confidential_cover.jpg
- binding: ebook
  isbn: 9781455528745
  asin: B00AMILAEK
  publisher: Grand Central Publishing
```

#### Available Bindings

- harcover
- paperback
- audiobook
- ebook

### Buylinks

The module sports a sophisticated Buylink generator which relies on retailers IDs and edition bindings.
Here are the current available retailers, their ids, the bindings they sell, and the expected edition's data for link generation

##### Your Independent Bookstore
  - id: bookshop
  - expect: ISBN
  - type: hardcover, paperback
##### Barnes & Noble
  - id: barnesandnoble
  - expect: ISBN
  - type: hardcover, paperback
##### Barnes & Noble Nook
  - id: barnesandnoble_nook
  - expect: ISBN
  - type: ebook
##### Libro
  - id: libro
  - expect: ISBN
  - type: audiobook

##### Amazon
  - id: amazon
  - expect: ISBN or ASIN
  - type: hardcover, paperback
##### Amazon Audible
  - id: amazon_audible
  - expect: ASIN
  - type: audiobook
##### Amazon Kindle
  - id: amazon_kindle
  - expect: ASIN
  - type: ebook
##### Apple Books
  - id: apple_books
  - expect: `apple_books_url` key on the edition
  - type: ebook

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

#### retailers

The retailers config key allows users to overwrite the default list of retailers to limit, order or overwrite labels:

```yaml
# config.yaml's retailers example and defaults
params:
  tnd_books:
  - id: barnesandnoble
    label: Barnes & Noble
  - id: barnesandnoble_nook
    label: Barnes & Noble Nook
  - id: amazon
    label: Amazon
  - id: amazon_audible
    label: Amazon Audible
  - id: amazon_kindle
    label: Amazon Kindle
  - id: apple_books
    label: "Apple Books"
```

## Excerpts page

The module can help create a page for a book excerpt whose content file contains the `excerpt` key.
To add those pages to project you should:

1. Add a cascade key to assign the output format to all books:
```yaml
# content/book/_index.md
---
title: Books
# First make sure the cascade is not inherited by the section itself.
ouputs:
  - HTML
# Add children ouputs through cascade.
cascade:
  outputs:
    - HTML
    - tnd_books_excerpt
```


By default the excerpt will live at `/books/{:slug}/excerpt/`.


## theNewDynamic

This project is maintained and love by [thenewDynamic](https://www.thenewdynamic.com).