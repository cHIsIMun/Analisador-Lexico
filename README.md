# Analisador Léxico

🇧🇷 Português | 🇺🇸 [English](README.en.md)

> Um analisador léxico (tokenizador) educacional em Python para uma micro-linguagem, baseado em expressões regulares com grupos nomeados.

## Visão geral

Este projeto implementa um **analisador léxico** didático que tokeniza uma **linguagem simplificada**, classifica identificadores, monta uma **tabela de símbolos** e reporta erros léxicos. A abordagem é baseada em **um único regex com grupos nomeados** (`(?P<NOME>...)`), iterado com `finditer()` — sem autômato/DFA explícito.

É um exemplo claro do **primeiro estágio de um compilador** (análise léxica).

## A linguagem reconhecida

| Categoria | Tokens |
|-----------|--------|
| Palavras-chave | `while`, `do` |
| Identificadores | `i`, `j` (intencionalmente restritos, para fins didáticos) |
| Números | inteiros (sequências de dígitos) |
| Operadores | `<`, `+`, `=` |
| Terminador | `;` |
| Inválido | qualquer caractere não reconhecido gera um erro léxico |

Exemplo de entrada válida:

```
while i < 10;
j = i + 5;
```

## Estrutura do projeto

| Arquivo | Responsabilidade |
|---------|------------------|
| `tokens.py` | Define `token_specs` (pares nome/regex) e compila o regex global |
| `lexer.py` | Função `lex(code)`: itera os matches, classifica tokens, monta a tabela de símbolos |
| `output_handler.py` | Serializa o resultado em JSON |
| `main.py` | CLI (argparse): lê o arquivo, chama `lex()`, grava a saída e imprime erros |

## Como executar

```bash
python main.py arquivo.code
```

Substitua `arquivo.code` pelo caminho do código-fonte a analisar. A saída é um JSON com a lista de `tokens` (cada um com `token`, `identificacao`, `tamanho`, `posicao [linha, coluna]`) e a `tabela de símbolos`. Erros léxicos são listados com sua posição.

## Estado e limitações

Funciona como demonstração didática do fluxo léxico. Por ser propositalmente reduzido:

- Identificadores limitados a `i` e `j`; sem suporte a strings, comentários ou números de ponto flutuante.
- O rastreamento de número de linha é incompleto (o contador não avança em quebras de linha dentro do *skip*).
- O nome do arquivo de saída no código (`saída.json`) difere do mencionado historicamente (`output.json`).
- Sem testes automatizados.

## Licença

Este projeto ainda não declara uma licença; até que uma seja adicionada, todos os direitos são reservados ao autor.
