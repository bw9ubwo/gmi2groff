# gmi2groff README

`gmi2groff` is a command-line tool for converting text files formatted in the Gemini protocol into Groff documents, utilizing the MOM macro package. This enables the creation of high-quality, typeset documents in formats like PDF.

## Overview

- Converts Gemini text structure into professional Groff typesetting.
- Handles links to `.eps` image files and integrates them into the document.
- Offers customizable document settings through an optional configuration file.
- Supports an optional table of contents (TOC) with a single command.

## Prerequisites

Make sure the following are installed on your system:

- **Python 3**: Required to run the script.
- **Groff**: Necessary for processing `.mom` files.
- **Ghostscript**: Converts PostScript outputs to PDF.
- **A PDF viewer**: Such as Zathura, for viewing the resulting PDF document.

## Installation

1. **Clone the repository** to your local machine:
   ```bash
   git clone <repository-url>
   ```

## Usage

Execute the `gmi2groff` script using:

```bash
./gmi2groff <input_file> <output_file> [--settings <settings_file>] [--toc]
```

- `<input_file>`: The Gemini format text input file.
- `<output_file>`: The desired Groff output filename, typically `.ms`.
- `--settings <settings_file>`: (Optional) A file containing custom document settings.
- `--toc`: (Optional) A flag to include a table of contents in the output document.

### Image Handling

Links pointing to `.eps` images within the Gemini text are automatically processed. Include image links using:

```
=> /path/to/image.eps Image Description
```

The script converts these links to Groff's `.PDFPIC` commands, inserting the image into the document with the associated description.

### Full Command Example

To convert `letter.gmi` to a PDF with custom settings and a TOC:

1. Convert the Gemini file to Groff:
   ```bash
   gmi2groff letter.gmi output.mom --settings custom_settings.txt --toc
   ```

2. Convert Groff to PDF and view in zathura (PDF Viewer):
   ```bash
   groff -mom -mden output.ms -Tps -P-pa4 -Kutf8 > output.ps && ps2pdf output.ps output.pdf && rm output.ps && zathura output.pdf
   ```
   Personally, I don't use `pdfmom` because sometimes it produces different output. That's why I write a PS file first.

### Custom Settings File Example

Create a custom settings file to adjust typography and layout, like this:

```plaintext
.PRINTSTYLE TYPESET
.PAPER A4
.FAMILY T
.LS 20
.PT_SIZE 12
.COLUMNS 1 20p
.HEADING_STYLE 1 UNDERLINE
.HEADING_STYLE 2 BOLD
.HEADING_STYLE 3 ITALIC
.BLOCKQUOTE_INDENT 3m
.MARGIN LEFT 1.5i
.MARGIN RIGHT 1.5i
.FONT COLOR blue
```

## Features and Options

- **Automatic TOC**: Use the `--toc` flag for an automatically generated TOC positioned within the document.
- **Image Integration**: Seamlessly processes `.eps` links to include images.
- **Customizable Settings**: Define document appearance using a configuration file for personalized output.

## Conclusion

`gmi2groff` serves as an efficient bridge from Gemini protocol documents to high-fidelity Groff typesetting. By offering flexibility in customization and robust document processing capabilities, it is ideal for users looking to convert plaintext into well-formatted documents efficiently.

This README provides a comprehensive guide to get started with `gmi2groff`, offering detailed instructions and examples to enhance your document formatting tasks. For any issues or further details, explore the user community and additional resources related to the tool.
