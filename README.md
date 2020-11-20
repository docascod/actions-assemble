# A github action for creating professional documents

This action assemble generated documents(PDF) from markdown, reStructuredText or asciidoctor.
Based on [docsAsCode](https://github.com/docascod/DocsAsCode).

## Inputs

### `sources`

**Required** Location of PDFs files in github repository. Default: repo´s root.

## Environment variables

### `DEFAULT_DESTINATION`

Location to output PDF files. Default: source dir

### `DEFAULT_NAME`

Name for the generated PDF. Default: out.pdf

## Example usage with result in artifact

```yml
on:
  push:
    paths: 
      - 'Example/*.pdf'
jobs:
  assemble_pdf:
    runs-on: ubuntu-latest
    name: A job to test this action
    env:
      DEFAULT_DESTINATION: 'Example/build/'
      DEFAULT_NAME: book.pdf
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Assemble
        uses: ./
        with:
          sources: 'Example/*.pdf'
      - name: Publish
        uses: actions/upload-artifact@v2
        with:
          path: ${{ env.DEFAULT_DESTINATION }}/book.pdf
```

NOTE: upload-artifact action always compress result before upload.
