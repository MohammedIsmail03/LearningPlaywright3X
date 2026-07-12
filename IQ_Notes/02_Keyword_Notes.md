# JavaScript Keywords

## Example File: `02_Keywords.js`

```js
class Robot {
  static count = 0;
  constructor(name) {
    this.name = name;
    Robot.count++;
  }
  async greet() {
    if (this.name) {
      return `Hello, I am ${this.name}`;
    } else {
      throw new Error("No name set");
    }
  }
}

export default Robot;
```

---

## What Is a Keyword?

A **keyword** is a word reserved by the JavaScript language spec. It has special meaning to the parser/engine and **cannot be used as a variable, function, or class name** (e.g. `let const = 5;` throws `SyntaxError`).

---

## Comparison Table — All JS Keywords by Category

| Category               | Keywords                                                              | Reserved? | Example Use                                  |
|-------------------------|------------------------------------------------------------------------|-----------|-----------------------------------------------|
| **Declaration**         | `var`, `let`, `const`, `function`, `class`                            | ✅ Always | `const x = 1;`                                |
| **Control Flow**        | `if`, `else`, `switch`, `case`, `default`, `break`, `continue`        | ✅ Always | `if (x) {} else {}`                           |
| **Loops**                | `for`, `while`, `do`, `in`, `of`                                       | ✅ Always | `for (const k in obj) {}`                     |
| **Functions/Return**    | `function`, `return`, `yield`, `async`, `await`                       | ✅ Always | `async function f() { await g(); }`           |
| **Error Handling**      | `try`, `catch`, `finally`, `throw`                                    | ✅ Always | `try {} catch (e) {}`                         |
| **Classes/OOP**         | `class`, `extends`, `super`, `static`, `new`, `this`                  | ✅ Always | `class B extends A { constructor(){super();} }` |
| **Modules**              | `import`, `export`, `default`, `from`, `as`                           | ✅ Always | `import x from "./x.js";`                     |
| **Operators (word-form)** | `typeof`, `instanceof`, `in`, `delete`, `void`, `new`                | ✅ Always | `typeof x === "string"`                       |
| **Literals**             | `true`, `false`, `null`                                                | ✅ Always | `let x = null;`                               |
| **Misc/Legacy**          | `debugger`, `with`, `void`                                             | ✅ Always | `debugger;`                                   |
| **Strict-mode reserved** | `implements`, `interface`, `package`, `private`, `protected`, `public`, `enum` | ⚠️ Reserved but unused in current spec | future-proofing only |
| **Contextual (not fully reserved)** | `let`, `static`, `async`, `await`, `get`, `set`, `of`, `from`, `as`, `yield` | ⚠️ Depends on context | `let` is fine as a property name: `obj.let = 1` |

---

## How It Works for Our Example

### 1. Declaration keywords
```js
class Robot {
  static count = 0;
```
`class` declares a blueprint. `static` attaches `count` to the class itself, not to instances.

### 2. Constructor + `this`
```js
constructor(name) {
    this.name = name;
    Robot.count++;
}
```
`this` refers to the instance being built. `constructor` is a reserved method name inside a `class` body (not a general keyword, but has special meaning there).

### 3. Async + control flow + error handling
```js
async greet() {
    if (this.name) {
      return `Hello, I am ${this.name}`;
    } else {
      throw new Error("No name set");
    }
}
```
`async` marks the method as promise-returning. `if/else` branches. `return` exits with a value. `throw` raises an error that a caller must `try/catch`.

### 4. Module keyword
```js
export default Robot;
```
`export` exposes the class to other files; `default` marks it as the file's primary export.

---

## Keyword Processing Pipeline (Visual)

```
┌─────────────────┐      ┌──────────────────────┐      ┌─────────────────────┐
│   Source Code   │ ───► │   Lexer/Tokenizer     │ ───► │   Parser (AST)      │
│  (raw .js text) │      │ splits into tokens    │      │ builds syntax tree  │
│                 │      │ keywords flagged as   │      │ keywords become     │
│                 │      │ reserved token type   │      │ AST node types      │
└─────────────────┘      └──────────────────────┘      └─────────────────────┘
                                                                   │
                                                                   ▼
                                                     ┌─────────────────────────┐
                                                     │ Engine (V8) executes    │
                                                     │ per keyword semantics:  │
                                                     │ class → prototype setup │
                                                     │ try/catch → exception   │
                                                     │ async → microtask queue │
                                                     └─────────────────────────┘
```

---

## Quick Rule of Thumb

| If you want to...                          | Reach for keyword(s)             |
|---------------------------------------------|-----------------------------------|
| Declare a variable that can change           | `let`                             |
| Declare a variable that can't be reassigned  | `const`                           |
| Define reusable behavior                     | `function`, `class`               |
| Branch logic                                 | `if / else`, `switch`             |
| Repeat work                                  | `for`, `while`, `do`              |
| Handle failures                              | `try / catch / finally`, `throw`  |
| Share code across files                      | `import`, `export`                |
| Wait on a Promise                            | `async`, `await`                  |
| Check a type at runtime                      | `typeof`, `instanceof`            |

---

> **TL;DR:** JS keywords are the ~35 reserved words (`if`, `for`, `class`, `const`, `try`, `async`, etc.) the parser treats as syntax, not identifiers. They split into always-reserved (can never be a variable name) and contextual (reserved only in certain positions, like `let` or `async`). Every keyword maps to one job: declare, branch, loop, handle errors, define classes, or move data between modules.
