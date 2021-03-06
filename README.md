# tempura
A Fast and Flexible Template Fill CLI Tool.

[![](https://img.shields.io/badge/docker-ghcr.io%2Fkorosuke613%2Ftempura-blue)](https://github.com/users/korosuke613/packages/container/package/tempura) [![](https://img.shields.io/github/v/release/korosuke613/tempura)](https://github.com/korosuke613/tempura/releases) ![](https://img.shields.io/github/go-mod/go-version/korosuke613/tempura) [![codecov](https://codecov.io/gh/korosuke613/tempura/branch/main/graph/badge.svg?token=Qa6t43fPaf)](https://codecov.io/gh/korosuke613/tempura)

Enter the following information to output the text that fills the template.
- a template written in the format [text/template](https://golang.org/pkg/text/template)
- variables by JSON

## Install

### go install
```
go install github.com/korosuke613/tempura@latest
```

### docker
```
docker pull ghcr.io/korosuke613/tempura
```

### manual
Download from [Releases](https://github.com/korosuke613/tempura/releases).

## Getting Started
using binary
```
❯ tempura --input-string '{"Name": "John", "Message": "Good"}' --template-string 'Hello {{.Name}}, {{.Message}}'
Hello John, Good
```

or using docker

```
❯ docker run --rm ghcr.io/korosuke613/tempura --input-string '{"Name": "John", "Message": "Good"}' --template-string 'Hello {{.Name}}, {{.Message}}'
Hello John, Good
```


## Example

### input multiline template
```
❯ tempura \
 --input-string '{"Name": "John", "Message": "Good"}' \
 --template-string \
'Hello {{.Name}},
{{.Message}}'
Hello John,
Good
```

### read template and inputs
#### input
`input.json`
```json
{
  "Name": "John",
  "Message": "Good"
}
```

`template.tmpl`
```gotemplate
Hello {{.Name}},
{{.Message}}
```

#### output
```
❯ tempura -i input.json -t template.tmpl
Hello John,
Good
```

### output to file
```
❯ tempura -o ./output.txt
❯ cat ./output.txt
Hello John,
Good
```

### use Actions
https://golang.org/pkg/text/template/#hdr-Actions

#### input
`input.json`
```json
{
  "isTrue": true,
  "Cat": "cat"
}
```

`template.tmpl`
```gotemplate
{{if .isTrue}}isTrue is True!{{end}}

{{if .isFalse}}never{{else}}isFalse is False!{{end}}

{{if eq .Cat "cat"}}Cat: nyan{{end}}
```

#### output
```
❯ tempura
isTrue is True!

isFalse is False!

Cat: nyan
```

### Options
```
❯ tempura -h
A Fast and Flexible Template Fill CLI Tool built with love by korosuke613 in Go.

Usage:
  tempura [flags]

Flags:
  -h, --help                       help for tempura
  -i, --input-filepath string      input file name (default "input.json")
      --input-string string        input string
  -o, --output string              output file name
  -t, --template-filepath string   template file name (default "template.tmpl")
      --template-string string     template string
  -v, --version                    show version
```
