# String Compression GitHub Action

Compress or decompress arbitrary strings using Node.js `zlib` algorithms (`brotli`, `gzip`, `deflate`, `deflate-raw`) via a lightweight composite action powered by `actions/github-script`. Defaults to Brotli.

## Inputs

| Input | Default | Description |
|-------|---------|-------------|
| `data` | (required) | String to transform |
| `mode` | `compress` | `compress` or `decompress`. |
| `algorithm` | `brotli` | One of `brotli`, `gzip`, `deflate`, `deflate-raw`. |
| `input_encoding` | `utf8` | Encoding of provided `data`: `utf8`, `base64` |
| `output_encoding` | `base64` (for compress) | Encoding of result: `utf8`, `base64` |

## Outputs

| Output | Description |
|--------|-------------|
| `result` | Transformed string in `output_encoding` |

## Usage - Compress

```yaml
name: demo-compress
on: [push]
jobs:
  compress:
    runs-on: ubuntu-latest
    steps:
    - name: Compress a string (brotli)
        uses: ubiquity/compress-action
        id: br
        with:
          data: "The quick brown fox jumps over the lazy dog"
          mode: compress
          algorithm: brotli
          input_encoding: utf8
          output_encoding: base64
      - name: Show outputs
        run: |
          echo "Compressed (base64): ${{ steps.br.outputs.result }}"
```

## Usage - Decompress

```yaml
name: demo-decompress
on: [push]
jobs:
  decompress:
    runs-on: ubuntu-latest
    steps:
    - name: Decompress previously compressed base64
        uses: ubiquity/compress-action
        id: br
        with:
          data: YOUR_BASE64_COMPRESSED_STRING
          mode: decompress
          algorithm: brotli
          input_encoding: base64
          output_encoding: utf8
      - name: Show result
        run: |
          echo "Decompressed: ${{ steps.br.outputs.result }}"
```
