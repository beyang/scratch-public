# (WIP) Sixteen awesome things you can do in Sourcegraph

Sourcegraph is a code intelligence platform that helps you grok code and improves your day-to-day productivity, as well as assist you with some of those bigger dragons you face from time to time—large refactors, code health initiatives, and security remediations.

This 10-minute interactive guide provides a quick dive into some of the coolest things you can do.

## 1. Find an error message across millions of repositories

```sourcegraph
At least one model must be passed to register
```

## Scope the search to just PyPI packages

```sourcegraph
repo:^python/ At least one model must be passed to register
```

## Search for secrets and security anti-patterns:

![](https://user-images.githubusercontent.com/1646931/184546102-f8c794e6-629f-4df8-8975-ebae29e4e4de.gif)

```sourcegraph
// RSA private key
-----BEGIN RSA PRIVATE KEY----- or

// SSH (DSA) private key
-----BEGIN DSA PRIVATE KEY----- or

// SSH (EC) private key
-----BEGIN EC PRIVATE KEY----- or

// PGP private key block
-----BEGIN PGP PRIVATE KEY BLOCK----- or

// AWS API Key
((?:A3T[A-Z0-9]|AKIA|AGPA|AIDA|AROA|AIPA|ANPA|ANVA|ASIA)[A-Z0-9]{16})

repo:^github.com/

// Filter out any files you don't want
-file:(index.html|sourcegraph-console-query.txt|README.md|bookmarklet.js)

patterntype:regexp
case:yes 
```

## Find functions that provide auth in Go

```sourcegraph
go auth middleware func type:symbol patterntype:lucky
```

In the above search, we specified `patterntype:lucky` to tell Sourcegraph to intelligently interpret our fuzzy search query. `patterntype:lucky` is the default search type in Sourcegraph, so can just type whatever comes to mind into that search box and Sourcegraph will handle the rest.

On the other hand, when you really want to very precisely define what you're looking for, you can use `patterntype:regex` or `patterntype:standard`.

## Search patterns in code *without* regex

```sourcegraph
fmt.Errorf(":[_]", :[[_]], :[[_]]) patterntype:structural 
```

Regex syntax can be unwieldy and it isn't expressive enough to describe balanced parens and quotes, so Sourcegraph supports [Comby](https://comby.dev/), a more intuitive pattern matching syntax.

Compare the above search for `fmt.Errorf` invocations with 3 arguments to a regex-based search that can only approximate the results set:

```sourcegraph
fmt.Errorf\("[^"]+", ("?[^"\)]+"?|\w+), ("?[^"\)]+"?|\w+)\) patterntype:regexp
```

## See all recent commits authored by Linus Torvalds

```sourcegraph
type:diff author:"Linus Torvalds"
```

## See all recent Linus commits that mention "bug fix"

```sourcegraph
type:commit author:"Linus Torvalds" fix bug patterntype:regexp
```

## Search multiple revisions simultaneously

```sourcegraph
repo:^github\.com/torvalds/linux$@master:v5.19:v5.18 Signal .+ caused a tool exit, line .+ patterntype:regexp 
```

## Search across the same revision across multiple repositories

```sourcegraph
repo:^github.com/gorilla/@v1.0.0 test
```

If you consistently search identical versions across multiple repositories, [create a search context](https://sourcegraph.com/contexts/new) as a shorthand you can reuse yourself and share with others.

## Learn by example


In the code snippet below, hover over `NewFileTransport` and click "Find references".

https://sourcegraph.com/github.com/golang/go/-/blob/src/net/http/filetransport.go?L30

Sourcegraph displays not just local references, but also external references, also known as "xrefs", from upstream dependencies:

<a href="https://sourcegraph.com/github.com/golang/go@3486735bf2ca08dcd84bb820fdcb0dea8102cf82/-/blob/src/net/http/filetransport.go?L30:6&subtree=true#tab=references">
  <img src="https://user-images.githubusercontent.com/1646931/187709192-05070843-0faa-495f-993a-fc5fdcca4b59.png" width="75%" />
</a>

## Find implementations globally

https://sourcegraph.com/github.com/golang/go/-/blob/src/net/http/server.go?L86

## Go-to-def across dependency boundaries

## Automate large-scale changes

## Review code with code navigation

## Track status of big refactors and migrations

## Analyze code quality

# How to start using Sourcegraph
