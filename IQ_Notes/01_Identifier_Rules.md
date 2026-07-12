# JavaScript Identifier Rules

## Example File: `03_Identifer_Rules.js`

```js
var a = 10;
console.log(a);

var $ = 10;
var _a = 23;
var pp = 34;

var ab123 = 23;
// var 45 = 34;
var _ = 10;

var Name = "pramod";
var name = "Amit";

// var pramod dutta = "hello";
var pramod_dutta = "hello";
var pramod$dutta = "hello";
var pramodu1232 = "hello";
```

---

## What Is an Identifier?

An **identifier** is the name given to a variable, function, class, or property. JS enforces strict rules on what characters are legal — break them and you get a `SyntaxError` before the code even runs.

---

## Comparison Table — Allowed vs Not Allowed

| Rule                                      | Allowed ✅                          | Not Allowed ❌                     | Why                                                        |
|--------------------------------------------|--------------------------------------|--------------------------------------|-------------------------------------------------------------|
| **First character**                       | letter, `_`, or `$`                 | a digit                              | `var 45 = 34;` → parser reads `45` as a number literal      |
| **Remaining characters**                  | letters, digits, `_`, `$`           | spaces, hyphens, most symbols        | `var pramod dutta` is parsed as two separate tokens         |
| **Case sensitivity**                      | `Name` and `name` are two variables | assuming they're the same           | JS is case-sensitive end to end                             |
| **Reserved keywords**                     | `total`, `data1`                    | `var`, `class`, `if`, `return`, etc. | Keywords are reserved by the language spec (see keyword notes) |
| **Spaces / hyphens**                      | use `_` or camelCase instead         | `first-name`, `first name`           | `-` is parsed as subtraction; space breaks the token          |
| **Special symbols**                       | `_` and `$` only                    | `@`, `#`, `%`, `!`, etc.             | Only `_` and `$` are legal identifier symbols in JS          |
| **Unicode**                                | `café`, `π` (technically valid)      | emoji in most engines                | JS identifiers follow the Unicode ID_Start/ID_Continue spec  |
| **Length**                                 | practically unlimited                 | —                                     | No hard limit, but keep it readable                          |

---

## How It Works for Our Example

### 1. Valid starts: letter, `_`, `$`
```js
var a = 10;
var $ = 10;
var _a = 23;
```
`$` and `_` are the only non-letter characters legal as the **first** character of an identifier — jQuery (`$`) and private/internal vars (`_a`) both lean on this.

### 2. Digits allowed, but never first
```js
var ab123 = 23;
// var 45 = 34;   // ❌ SyntaxError: Unexpected number
```
Digits are fine *after* the first character, never as the first character.

### 3. Case sensitivity
```js
var Name = "pramod";
var name = "Amit";
```
`Name` and `name` are two completely different bindings — no collision, no warning.

### 4. Spaces break identifiers, underscores don't
```js
// var pramod dutta = "hello";   // ❌ SyntaxError
var pramod_dutta = "hello";      // ✅
var pramod$dutta = "hello";      // ✅
```
A space splits one identifier into two illegal tokens. `_` and `$` are the only "joiners" JS understands inside a name.

---

## Naming Conventions (Case Styles) — from `04_Identifer_Rues_Part2.js`

| Convention                 | Example                          | Used for                                |
|------------------------------|-----------------------------------|-------------------------------------------|
| **camelCase**                | `let userName = "..."`           | variables, functions (JS standard)        |
| **PascalCase**                | `let UserProfile = "..."`        | classes, constructors                     |
| **snake_case**                | `let user_name = "..."`          | rare in JS; common in Python/Ruby         |
| **SCREAMING_SNAKE_CASE**      | `const MAX_SIZE = 100;`          | constants                                 |
| **Hungarian Notation**        | `let strName`, `let bActive`     | legacy style, type-prefixed (avoid today) |

```js
let userName = "camelCase";
let UserProfile = "PascalCase";
let user_name = "snake_case";
const MAX_SIZE = 100;
let strName = "string prefix"; // Hungarian, old-school
```

---

## Identifier Validation Pipeline (Visual)

```
┌──────────────────┐     ┌────────────────────┐     ┌──────────────────────┐
│  Read first char  │ ──► │ letter / _ / $ ?    │ ──► │ Read remaining chars │
│                    │     │ NO → SyntaxError    │     │ letters/digits/_/$ ? │
└──────────────────┘     └────────────────────┘     │ NO → SyntaxError      │
                                                        └──────────────────────┘
                                                                   │
                                                                   ▼
                                                     ┌─────────────────────────┐
                                                     │ Is it a reserved         │
                                                     │ keyword (if/class/...)? │
                                                     │ YES → SyntaxError        │
                                                     │ NO  → Valid identifier   │
                                                     └─────────────────────────┘
```

---

## Quick Rule of Thumb

| If you want to...                          | Do this                              |
|-----------------------------------------------|-----------------------------------------|
| Name a normal variable/function               | `camelCase`                             |
| Name a class                                    | `PascalCase`                            |
| Name a constant that never changes             | `SCREAMING_SNAKE_CASE`                  |
| Join two words without breaking the identifier | use `_` or camelCase, never a space or `-` |
| Mark something "private"/internal by convention | prefix with `_`                        |

---

> **TL;DR:** A JS identifier must start with a letter, `_`, or `$`, then any mix of letters/digits/`_`/`$`. No spaces, no hyphens, no leading digits, no reserved keywords. It's case-sensitive, so `Name` ≠ `name`. Convention layers on top of the hard rules: camelCase for variables/functions, PascalCase for classes, SCREAMING_SNAKE_CASE for constants.
