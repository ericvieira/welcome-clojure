# CLAUDE.md - AI Assistant Guide for welcome-clojure

## Project Overview

**welcome-clojure** is a learning project inspired by WTTD (Welcome to the Django - a popular Brazilian Python/Django tutorial) designed to teach Clojure programming fundamentals through practical examples and exercises.

**Project Type**: Clojure learning/educational project
**Language**: Clojure (JVM-based Lisp dialect)
**Status**: Early stage/initialization
**Primary Goal**: Learn Clojure fundamentals through structured exercises

## Repository Structure

### Current Structure
```
welcome-clojure/
├── .git/                 # Git version control
├── .gitignore           # Git ignore patterns for Clojure projects
└── README.md            # Project introduction (Portuguese)
```

### Expected Future Structure
```
welcome-clojure/
├── src/                 # Source code directory
│   └── welcome/         # Main namespace directory
│       └── core.clj     # Main application code
├── test/                # Test directory
│   └── welcome/         # Test namespace directory
│       └── core_test.clj # Test files
├── resources/           # Resources (config, data files)
├── doc/                 # Documentation
├── deps.edn             # Clojure CLI dependencies (recommended)
│   OR
├── project.clj          # Leiningen project file (alternative)
├── .gitignore          # Ignore patterns
└── README.md           # Project documentation
```

## Clojure Project Conventions

### Build Tools

Clojure projects typically use one of two main build tools:

1. **Clojure CLI + tools.deps** (Modern, recommended)
   - Configuration file: `deps.edn`
   - Command: `clj` or `clojure`
   - Simpler, more composable approach

2. **Leiningen** (Traditional, widely used)
   - Configuration file: `project.clj`
   - Command: `lein`
   - More features out of the box, plugin ecosystem

### Namespace Conventions

- Source files live in `src/` directory
- File paths mirror namespace structure
- Example: `welcome.core` → `src/welcome/core.clj`
- Namespaces use hyphens, files use underscores for multi-word names
  - Namespace: `welcome-clojure.utils` → File: `src/welcome_clojure/utils.clj`

### Code Style

1. **Indentation**: 2 spaces (never tabs)
2. **Line length**: Typically 80-100 characters
3. **Naming conventions**:
   - `kebab-case` for functions and variables
   - `PascalCase` for protocols and records
   - `*earmuffs*` for dynamic vars
   - `?` suffix for predicates (e.g., `empty?`, `nil?`)
   - `!` suffix for functions with side effects
4. **Parentheses**: Don't add unnecessary whitespace inside parens
   - Good: `(defn hello [name] (str "Hello " name))`
   - Bad: `( defn hello [ name ] ( str "Hello " name ) )`

## Development Workflow

### Setting Up a New Project

When setting up this project for development, follow these steps:

1. **Choose a build tool**:
   ```bash
   # For Clojure CLI (recommended)
   # Create deps.edn with basic structure

   # For Leiningen
   # Create project.clj with basic structure
   ```

2. **Create directory structure**:
   ```bash
   mkdir -p src/welcome test/welcome resources
   ```

3. **Create main namespace** (`src/welcome/core.clj`):
   ```clojure
   (ns welcome.core)

   (defn -main
     "Application entry point"
     [& args]
     (println "Welcome to Clojure!"))
   ```

### Common Development Tasks

#### Running the REPL
```bash
# Clojure CLI
clj

# Leiningen
lein repl
```

#### Running Tests
```bash
# Clojure CLI
clojure -X:test

# Leiningen
lein test
```

#### Running the Application
```bash
# Clojure CLI
clojure -M -m welcome.core

# Leiningen
lein run
```

### REPL-Driven Development

Clojure development is typically REPL-driven:

1. Start a REPL session
2. Load your namespace: `(require '[welcome.core :as core] :reload)`
3. Test functions interactively: `(core/some-function args)`
4. Make changes to code
5. Reload: `(require 'welcome.core :reload)`
6. Repeat

## Key Conventions for AI Assistants

### When Adding New Features

1. **Always use proper namespace declarations**:
   ```clojure
   (ns welcome.feature
     (:require [clojure.string :as str]
               [welcome.utils :as utils]))
   ```

2. **Create corresponding test files**:
   - Source: `src/welcome/feature.clj`
   - Test: `test/welcome/feature_test.clj`

3. **Use docstrings for public functions**:
   ```clojure
   (defn greet
     "Greets a person by name.

     Parameters:
     - name: String representing the person's name

     Returns: Greeting string"
     [name]
     (str "Hello, " name "!"))
   ```

### Code Quality

1. **Avoid Java interop unless necessary**: Prefer idiomatic Clojure
2. **Use built-in functions**: Clojure has rich core library
3. **Immutability first**: Avoid mutable state unless essential
4. **Pure functions**: Separate pure logic from side effects
5. **Small, focused functions**: Unix philosophy - do one thing well

### Testing Conventions

Use `clojure.test` (built-in testing framework):

```clojure
(ns welcome.core-test
  (:require [clojure.test :refer [deftest is testing]]
            [welcome.core :as core]))

(deftest test-greet
  (testing "Greeting function"
    (is (= "Hello, World!" (core/greet "World")))))
```

### Error Handling

1. **Use exceptions for exceptional cases**
2. **Return nil or special values for expected failures**
3. **Consider using `ex-info` for rich error data**:
   ```clojure
   (throw (ex-info "Invalid input"
                   {:type :validation-error
                    :input input-value}))
   ```

### Dependencies

When adding dependencies:

1. **deps.edn format**:
   ```clojure
   {:deps {org.clojure/clojure {:mvn/version "1.11.1"}
           compojure/compojure {:mvn/version "1.7.0"}}}
   ```

2. **project.clj format**:
   ```clojure
   :dependencies [[org.clojure/clojure "1.11.1"]
                  [compojure "1.7.0"]]
   ```

## Git Workflow

### Branch Naming
- Feature branches: `feature/description`
- Bug fixes: `fix/description`
- Learning exercises: `exercise/topic-name`
- AI-assisted branches: `claude/session-id` (auto-generated)

### Commit Messages
Use clear, descriptive commit messages in Portuguese or English:
- Good: "Adiciona função para calcular fatorial"
- Good: "Add factorial calculation function"
- Bad: "update"

### Before Committing
1. Ensure code runs without errors
2. Run tests if they exist: `lein test` or `clojure -X:test`
3. Check for syntax errors in REPL
4. Format code properly (2-space indentation)

## Common Clojure Patterns

### Data Transformation
```clojure
;; Threading macros for readability
(-> data
    (filter pred)
    (map transform)
    (reduce combine))

;; Or thread-last
(->> collection
     (filter even?)
     (map #(* % 2))
     (take 10))
```

### Destructuring
```clojure
;; Vector destructuring
(let [[first second & rest] [1 2 3 4 5]]
  ...)

;; Map destructuring
(let [{:keys [name age]} person]
  ...)
```

### Higher-Order Functions
```clojure
;; Use built-ins: map, filter, reduce, etc.
(map inc [1 2 3])  ;; => (2 3 4)
(filter even? [1 2 3 4])  ;; => (2 4)
(reduce + [1 2 3 4])  ;; => 10
```

## Learning Resources

For this educational project, consider these topics:

1. **Basics**: Functions, data structures (lists, vectors, maps, sets)
2. **Functional Programming**: Higher-order functions, immutability
3. **Sequences**: Lazy evaluation, sequence operations
4. **Namespaces**: Code organization, requiring dependencies
5. **Destructuring**: Elegant parameter handling
6. **Macros**: Code that writes code (advanced)
7. **Concurrency**: Atoms, refs, agents (when needed)

## Project-Specific Notes

### Language
The README is in Portuguese, suggesting the target audience may be Portuguese speakers (likely Brazilian, given WTTD reference). Consider:
- Documentation can be in Portuguese
- Comments can be in Portuguese
- But code (function names, variables) should still follow English conventions when possible

### WTTD Inspiration
WTTD (Welcome to the Django) follows a practical, hands-on approach:
- Build real applications while learning
- Incremental complexity
- Test-driven development
- Best practices from the start

Apply these principles to Clojure learning.

## Troubleshooting

### Common Issues

1. **"Could not find or load main class"**
   - Check namespace matches file path
   - Ensure proper `-main` function definition

2. **"Unable to resolve symbol"**
   - Check namespace requires
   - Verify function is public (not private with `defn-`)

3. **"ClassNotFoundException"**
   - Dependency not in classpath
   - Check deps.edn or project.clj

4. **Stack overflow errors**
   - May need `recur` for tail recursion
   - Consider lazy sequences

## AI Assistant Guidelines

When working on this project:

1. **Start simple**: This is a learning project, prioritize clarity over cleverness
2. **Explain your code**: Add comments and docstrings liberally
3. **Show alternatives**: When appropriate, show different ways to solve problems
4. **Follow conventions**: Stick to Clojure community standards
5. **Test your code**: Create tests for new functionality
6. **Build incrementally**: Small steps, ensuring each works before moving on
7. **Use idiomatic Clojure**: Embrace functional programming paradigms

### Before Making Changes

1. Check if build configuration exists (deps.edn or project.clj)
2. Verify directory structure is in place
3. Ensure dependencies are properly specified
4. Test in REPL if possible

### After Making Changes

1. Verify code loads without errors
2. Run tests if they exist
3. Provide examples of how to use new functionality
4. Update documentation as needed

## Quick Reference

### File Extensions
- `.clj` - Clojure source files (JVM)
- `.cljs` - ClojureScript source files (JavaScript)
- `.cljc` - Cross-platform Clojure code
- `.edn` - Extensible Data Notation (config/data files)

### REPL Commands
```clojure
(doc function-name)     ; Show documentation
(source function-name)  ; Show source code
(dir namespace)         ; List namespace contents
(require 'ns :reload)   ; Reload namespace
```

### Special Forms
```clojure
def        ; Define a var
defn       ; Define a function
let        ; Local bindings
if         ; Conditional
do         ; Execute multiple expressions
fn         ; Anonymous function
```

---

**Last Updated**: 2025-11-14
**Project Status**: Initialization phase
**Next Steps**: Create basic project structure and first learning exercises
