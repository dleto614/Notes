---
Name: Extractify
Platform: N/a
tags:
  - Golang
  - infosec
---
Github: https://github.com/SharokhAtaie/extractify

Install: `go install github.com/SharokhAtaie/extractify@latest`

### Usage:

```bash
cat urls.txt | extractify -all
```

Pipe urls from a file to the tool and run everything.

------
### Help :

```bash
Usage:
  extractify [flags]

Flags:
INPUTS:
   -u, -url string   URL for scanning
   -l, -list string  List of URLs for scanning
   -f, -file string  Local file data for scanning

EXTRACTS:
   -es, -secrets     Extract secrets (default)
   -ee, -endpoints   Extract endpoints 
   -eu, -urls        Extract urls
   -ea, -all         Extract all

OTHERS:
   -fe, -filter-extension string[]  list of extensions svg,png (comma-separated) (default ["svg", "png", "jpg", "jpeg"])
   -H, -header string  Set custom header
   -v, -verbose        Verbose mode
   -t, -threads        Number of threads to use (default 5)
```