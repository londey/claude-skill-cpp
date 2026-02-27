---
name: claude-skill-cpp
description: C++20 coding guidelines and conventions. Use when writing, reviewing, or refactoring C++ code. Covers naming, formatting, resource management, type safety, modern C++20 features, and design principles from the C++ Core Guidelines and Sean Parent's Better Code series.
user-invokable: false
---

# C++20 Programming Skill

When writing C++ code, follow these guidelines. Target **C++20** as the language standard.

## File Conventions

- Header files use the `.hpp` extension.
- Source files use the `.cpp` extension.
- Every `.hpp` must have a corresponding `.cpp` file, even if it would otherwise be empty. This ensures the header compiles independently and provides a place for future implementation.
- All headers use `#pragma once` as the include guard.
- Use the `.clang-format` file in this repository for all formatting. Run `clang-format` before committing.

## Naming Conventions

Follow Rust-style capitalization applied to C++:

| Element | Convention | Example |
|---|---|---|
| Classes, structs, enums | `UpperCamelCase` | `HttpRequest`, `FileReader` |
| Enum variants (scoped enums) | `UpperCamelCase` | `Success`, `NotFound` |
| Functions, methods | `snake_case` | `read_file()`, `is_empty()` |
| Variables, parameters | `snake_case` | `line_count`, `buffer_size` |
| Constants, `constexpr` values | `SCREAMING_SNAKE_CASE` | `MAX_SIZE`, `DEFAULT_PORT` |
| Namespaces | `snake_case` | `my_project`, `io` |
| Template parameters | `UpperCamelCase` | `T`, `Value`, `Allocator` |
| Macros (avoid when possible) | `SCREAMING_SNAKE_CASE` | `DEBUG_LOG` |

Acronyms in `UpperCamelCase` names are treated as a single word: `Http`, `Xml`, `Uuid` — not `HTTP`, `XML`, `UUID`.

Predicate functions use prefixes like `is_`, `has_`, `should_`.

## Formatting

All formatting is enforced by the `.clang-format` file in this repository. Key rules:

- **Indentation**: 4 spaces, no tabs.
- **Braces**: Opening brace on the same line (Attach/K&R style).
- **Line length**: 100 characters maximum.
- **Indent style**: Block indent, not visual indent.
- **Arguments**: One argument per line when wrapping is required.
- **Namespaces**: Do not indent namespace contents.
- **Access modifiers**: Outdented by one level (`public:` at column 0 inside class body).
- No spaces inside parentheses or angle brackets.

## C++ Core Guidelines

Follow the [C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines). Key principles:

### Resource Management
- Use RAII for all resource management. Resources are tied to object lifetimes.
- Use `std::unique_ptr` for exclusive ownership and `std::shared_ptr` for shared ownership.
- No owning raw pointers. Raw pointers may only be used as non-owning observers.
- No `malloc`/`free`. Use standard containers and smart pointers.

### Type Safety
- No C-style casts. Use `static_cast`, `dynamic_cast`, `const_cast`, or `reinterpret_cast` (sparingly).
- No raw C arrays. Use `std::array`, `std::vector`, or `std::span`.
- Use `std::span<T>` instead of `(pointer, count)` pairs at interface boundaries.
- Use scoped enums (`enum class`) instead of unscoped enums.

### Modern C++20 Features
- Use **concepts** to constrain templates instead of SFINAE or unconstrained templates.
- Use **range-for loops** and **ranges** over index-based iteration.
- Use **structured bindings** to unpack pairs, tuples, and structs.
- Use `std::optional` for values that may be absent and `std::variant` for type-safe unions.
- Use `std::format` for string formatting instead of string concatenation or streams.
- Use `constexpr` and `consteval` wherever possible for compile-time computation.

### Error Handling
- Prefer exceptions for error handling. Errors must not be silently ignored.
- Use RAII to ensure exception safety — destructors handle cleanup.

### Interfaces
- Keep function parameter lists short (fewer than four parameters).
- Avoid adjacent parameters of the same type that could be accidentally swapped.
- Use `override` and `final` explicitly on virtual functions.
- Prefer returning values over out-parameters.

## Sean Parent's Better Code Principles

Follow the principles from Sean Parent's [Better Code](https://sean-parent.stlab.cc/papers-and-presentations/) series:

### No Raw Loops
- Prefer algorithms from `<algorithm>` and C++20 ranges over hand-written loops.
- If a lambda is more than a simple composition of two functions, give it a name.
- A raw loop is acceptable when an algorithm would obscure intent — add a comment explaining why.

### No Raw Pointers
- Default to **value semantics**. Objects should behave like values: assignment copies, equality compares content.
- Use smart pointers only when ownership semantics require them.
- `shared_ptr` should not appear in interfaces — it is an implementation detail.

### No Raw Synchronization Primitives
- Do not use raw mutexes, locks, condition variables, or atomics directly.
- Use higher-level abstractions: task systems, futures with continuations, parallel algorithms.

### Design Principles
- **Value semantics over reference semantics**: values are easier to reason about locally.
- **Concept-based polymorphism**: prefer type erasure and concepts over deep inheritance hierarchies.
- **Composition over inheritance**: favor composing small, focused types.
- **Local reasoning**: design code so correctness can be verified without understanding the entire codebase.
- **Copy-on-write**: use it to give value semantics to types that would otherwise be expensive to copy.
