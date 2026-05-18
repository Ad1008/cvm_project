# CVM++ Project Report

## 1. Project Overview
CVM++ is a custom-built, stack-based virtual machine and compiler designed to demonstrate the fundamentals of programming language implementation. It translates a high-level, C-like scripting language into a proprietary bytecode format, which is then executed by the Virtual Machine.

## 2. Architecture
The project is divided into four main modules:

### 2.1 Lexer (Lexical Analysis)
The Lexer takes raw source code as input and breaks it down into a stream of **Tokens**. It handles whitespace, comments, and recognizes keywords (`let`, `if`, `while`, `print`, `input`), identifiers, numeric literals, and operators.

### 2.2 Parser (Syntax Analysis)
The Parser consumes the token stream and builds an **Abstract Syntax Tree (AST)** using the Recursive Descent parsing technique. Each node in the AST represents a language construct, such as a statement or an expression. This ensures the source code follows the defined grammar.

### 2.3 Compiler (Bytecode Generation)
The Compiler traverses the AST and "flattens" it into a sequence of **Bytecode Instructions**. It manages a constant pool for literals and keeps track of local variables. It also handles jump patching for control flow structures like `if` and `while`.

### 2.4 Virtual Machine (Execution Engine)
The VM is a stack-based engine that executes the compiled bytecode. It maintains an **Instruction Pointer (IP)**, a data stack for computations, and a storage for local variables. It implements a dispatch loop that processes each OpCode and performs the corresponding operation.

## 3. Language Grammar
The language supports:
- **Variable Declaration:** `let <id> = <expr>;`
- **Assignment:** `<id> = <expr>;`
- **Arithmetic:** `+`, `-`, `*`, `/`
- **Comparison:** `==`, `<`
- **Control Flow:**
  - `if (condition) { ... } else { ... }`
  - `while (condition) { ... }`
- **I/O:**
  - `print <expr>;`
  - `let x = input;` (takes integer input)

## 4. Instruction Set Architecture (ISA)
| OpCode | Description |
| :--- | :--- |
| `CONSTANT` | Pushes a constant from the pool onto the stack. |
| `ADD`, `SUB`, `MUL`, `DIV` | Performs binary arithmetic. |
| `EQUAL`, `LESS` | Performs comparison operations. |
| `PRINT` | Pops and prints the top value of the stack. |
| `GET_LOCAL`, `SET_LOCAL` | Reads/Writes to local variable storage. |
| `JUMP`, `JUMP_IF_FALSE` | Forward branching for conditions and jumps. |
| `LOOP` | Backward jump for loops. |
| `INPUT` | Blocks for user input and pushes result to stack. |
| `HALT` | Terminates the VM. |

## 5. Implementation Details
- **Language:** C++17
- **Memory Management:** Used `std::unique_ptr` for AST nodes to ensure automatic memory cleanup.
- **Data Structures:** `std::vector` for the bytecode chunk and stack; `std::map` for symbol table (local variables).
- **Extensibility:** The modular design allows for easy addition of new OpCodes or language features.

## 6. Conclusion
CVM++ successfully implements a functional compiler and VM from scratch. It provides a robust foundation for understanding how high-level languages are transformed and executed at a lower level.
