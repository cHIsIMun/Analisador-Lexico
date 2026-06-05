# Lexical Analyzer

🇺🇸 English | 🇧🇷 [Português](README.md)

> An educational lexical analyzer (tokenizer) in Python for a micro-language, based on regular expressions with named groups.

## Overview

This project implements a didactic **lexical analyzer** that tokenizes a **simplified language**, classifies identifiers, builds a **symbol table**, and reports lexical errors. The approach is based on **a single regex with named groups** (`(?P<NAME>...)`), iterated with `finditer()` — no explicit automaton/DFA.

It is a clear example of the **first stage of a compiler** (lexical analysis).

## The recognized language

| Category | Tokens |
|----------|--------|
| Keywords | `while`, `do` |
| Identifiers | `i`, `j` (intentionally restricted, for teaching) |
| Numbers | integers (digit sequences) |
| Operators | `<`, `+`, `=` |
| Terminator | `;` |
| Invalid | any unrecognized character raises a lexical error |

Example of valid input:

```
while i < 10;
j = i + 5;
```

## Project structure

| File | Responsibility |
|------|----------------|
| `tokens.py` | Defines `token_specs` (name/regex pairs) and compiles the global regex |
| `lexer.py` | `lex(code)` function: iterates matches, classifies tokens, builds the symbol table |
| `output_handler.py` | Serializes the result to JSON |
| `main.py` | CLI (argparse): reads the file, calls `lex()`, writes output, prints errors |

## Running

```bash
python main.py file.code
```

Replace `file.code` with the path to the source you want to analyze. Output is a JSON file with the list of `tokens` (each with `token`, `identificacao`, `tamanho`, `posicao [line, column]`) and the symbol table. Lexical errors are listed with their position.

## Status and limitations

Works as a didactic demonstration of the lexical pipeline. Being intentionally minimal:

- Identifiers limited to `i` and `j`; no support for strings, comments, or floating-point numbers.
- Line-number tracking is incomplete (the counter does not advance on line breaks within the skip rule).
- The output filename in code (`saída.json`) differs from the historically mentioned `output.json`.
- No automated tests.

## License

This project does not yet declare a license. Until one is added, all rights are reserved by the author.
