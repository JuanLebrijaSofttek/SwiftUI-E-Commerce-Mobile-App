# Swiftui EccomerceCons Constitution

## Core Principles

### I. Reactive Observability & State Management
All business logic MUST reside in `@Observable` classes marked with `@MainActor`. Views MUST remain purely declarative and only describe UI for a given state. Property wrappers MUST be used according to their specific purpose: `@State` for local view-owned state, `@Binding` for mutable child-to-parent communication, and `@Environment` for shared dependencies. Legacy patterns such as `ObservableObject`, `@StateObject`, and `@ObservedObject` are strictly prohibited.

### II. Atomic View Composition
Views MUST be small, single-responsibility units. Complex UIs MUST be built through composition rather than inheritance or large monolithic bodies. The `var body` property MUST NOT contain heavy computation or imperative logic; all data transformations SHOULD be pre-computed in the ViewModel or handled via computed properties. Views MUST use stable, unique identifiers in `ForEach` structures to ensure efficient rendering and prevent diffing bugs.

### III. Comprehensive Type Safety (Non-Negotiable)
The application MUST be crash-free. Force unwrapping (`!`), force casting (`as!`), and implicitly unwrapped optionals (`Type!`) are strictly forbidden. Developers MUST use `guard let`, `if let`, or nil coalescing to handle optionals safely. Similarly, `try!` MUST NOT be used; all errors MUST be handled at the action layer using `do-catch` blocks or `try?` with appropriate user feedback (alerts or inline messages).

### IV. Clean Logic & Algorithmic Efficiency
Code MUST be written for clarity and performance. Nested ternaries and nested `switch` statements are prohibited to keep cognitive complexity low. High-efficiency methods MUST be preferred over manual iteration; specifically, `first(where:)` MUST be used instead of `filter().first`. Functions MUST NOT return constants where a static property would suffice, and functions with identical implementations MUST be refactored to eliminate redundancy.

### V. Security-First Architecture
Cryptographic integrity is mandatory. Only robust encryption (e.g., AES) and hashing algorithms (e.g., SHA-256, SHA-512) MAY be used. Legacy or weak algorithms, including DES, 3DES, MD5, and SHA-1, are strictly prohibited. Hard-coded credentials or keys MUST NOT exist in the codebase. All network and data-sensitive operations MUST be isolated from the UI layer.

## Development & Complexity Standards

### Complexity & Refactoring
- **Function Limits**: Functions exceeding a high cognitive complexity score or a cyclomatic complexity threshold MUST be refactored into smaller sub-functions.
- **File Integrity**: Each file SHOULD define exactly one primary type (class, struct, or enum). Extensions for that specific type MAY reside in the same file.
- **Tuple Constraints**: Tuples MUST NOT exceed two elements; use a named `struct` for larger data groups to improve maintainability and readability.
- **Clean Syntax**: Semicolons are prohibited. Trailing closure syntax MUST be used when a closure is the final argument, except when multiple function-type parameters would make the call ambiguous.

### Naming & Style
- **Naming Conventions**: `struct` and `enum` names MUST use PascalCase. Enum members, variables, and function names MUST use camelCase.
- **Identifier Hygiene**: Backticks around symbol names are prohibited. Identifiers MUST be renamed to avoid using reserved keywords.
- **Numeric Literals**: Underscores MUST be used to improve the readability of large numeric literals (e.g., `1_000_000`).
- **Standard Operators**: Standard operator precedence and associativity MUST NOT be modified. Custom operators MUST be surrounded by whitespace in their definitions.

## UI & Layout Standards

### Declarative Styling
- **Modifier Order**: Modifiers MUST be applied in a consistent sequence: Layout (frame, padding) -> Style (foreground, background, font) -> Behavior (onTap, onAppear).
- **Adaptive Layouts**: Layouts MUST be adaptive. Use `Spacer` and `frame(maxWidth: .infinity)` over fixed sizes. `GeometryReader` SHOULD be used sparingly and only when relative coordinate space is required.
- **Centralized Constants**: Magic numbers and hardcoded strings are prohibited. All colors, spacing, fonts, and strings MUST be centralized in enums or static properties.

### Animation & Navigation
- **Explicit Animation**: Animations MUST be explicit using `.animation(_, value:)` or `withAnimation {}`. Implicit animations are prohibited as they lead to unpredictable UI states.
- **State-Driven Navigation**: Navigation MUST be driven by state or enums using `NavigationStack` and `navigationDestination`. Inline `NavigationLink` logic is discouraged.

## Governance

### Compliance & Enforcement
All pull requests MUST be verified against this constitution. Code reviews MUST prioritize the removal of force-unwraps, the reduction of function complexity, and the adherence to the `@Observable` architectural pattern. Any deviation from these principles MUST be documented with a technical justification and approved by the lead architect.

### Amendments
This constitution supersedes all other documentation regarding project style and architecture. Amendments require a formal proposal, a migration plan for existing code, and ratification by the core development team.

**Version**: 1.0.0 | **Ratified**: 2024-05-22 | **Last Amended**: 2024-05-22