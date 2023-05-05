# CoolGo: Cool Compiler using Go Language

## Context Free Grammar
```ebnf
Program -> (Statment)*

Statment -> LetStatement | ReturnStatement | ExpressionStatement

LetStatement -> LET Identifier ASSIGN Expression SEMICOLON? 
ReturnStatement -> RETURN Expression 
ExpressionStatement -> Expression 
Expression ->   FunctionExpression |
                CallExpression     | 
                IfExpression       | 
                PrefixExpression   | 
                InfixExpression    | 
                TRUE               | 
                FALSE              | 
                (Expression) 

FunctionExpression -> FUNCTION LPAREN Parameters RPAREN LBRACE BlockStatment RBRACE
Parameters -> Identifier (COMMA Identifier)* | epsilon
BlockStatement -> (Statement)*

CallExpression -> Idenitifer RPAREN Arguments LPAREN
Arguments -> Expression (COMMA Expression)* | epsilon

IfExpression -> IF LPAREN Expression RPAREN LBRACE BlockStatement RBRACE (ELSE LBRACE BlockStatement RBRACE)?

PrefixExpression -> INT | Identifier | [MINUS BANG] Expression
InfixExpression -> Expression [PLUS MINUS ASTERISK SLASH EQ NOT_EQ LT GT] Expression

Identifier -> [a-zA-Z][a-zA-Z]*
INT -> [1-9][0-9]*

// Keywords
LET -> "let"
FUNCTION -> "fn"
RETURN -> "return"
IF -> "if"
ELSE -> "else"
TRUE -> "true"
FALSE -> "false"

// Operators
EQ -> "=="
ASSIGN -> "="
LT -> "<"
GT -> ">"
NOT_EQ -> "!="
PLUS -> "+"
MINUS -> "-"
ASTERISK -> "*"
SLASH -> "/"
BANG -> "!"

// Delimiters
COMMA -> ","
SEMICOLON -> ";"
LPAREN -> "("
RPAREN -> ")"
LBRACE -> "{"
RBRACE -> "}"

WS -> [\t\r\n ]
```

## Parsing
The parsing is done in top-down parsing, left-to-right fashion.
Examples:
```rust
let x = 2 * 3 + 4;
```

### Output
#### 1. Lexical Analysis
```bash
{Type:LET Literal:let}
{Type:IDENT Literal:x}
{Type:= Literal:=}
{Type:INT Literal:2}
{Type:* Literal:*}
{Type:INT Literal:3}
{Type:+ Literal:+}
{Type:INT Literal:4}
{Type:; Literal:;}
```

#### 2. Parsing
```rust
let x = ((2 * 3) + 4);
```

## To run the project
1. Make sure you have go installed
2. Run `go run .`, and you're good to go :smile: :tada: