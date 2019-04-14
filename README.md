# Go WASM

Trying out Go web assembly. [Go wiki
reference](https://github.com/golang/go/wiki/WebAssembly).

## Build

Copy required file from `GOROOT` if not provided.

```sh
cp "$(go env GOROOT)/misc/wasm/wasm_exec.js" .
```

Build the wasm code.

```sh
GOOS=js GOARCH=wasm go build -o lib.wasm
```

Start a web server (i.e. with `goexdec`) to get CORS and WASM download to work.

```sh
goexec 'http.ListenAndServe(":8080", http.FileServer(http.Dir(".")))'
```

If there are no blocking features file can be tested with node without a
browser.

```sh
GOOS=js GOARCH=wasm go run -exec="$(go env GOROOT)/misc/wasm/go_js_wasm_exec" .
```
