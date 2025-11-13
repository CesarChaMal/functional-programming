# CLAUDE.md - AI Assistant Guide for Functional Programming in Java

## Repository Overview

This is an educational repository for learning **Functional Programming in Java** (Java 8+), based on the book "Functional Programming in Java - Harnessing the Power of Java 8 Lambda Expressions" by Venkat Subramaniam. The repository contains exercises and solutions organized by session/chapter.

**Primary Purpose:** Educational practice exercises for a reading group studying functional programming concepts in Java.

**Reference Book:** Available at `/book/Pragmatic.Bookshelf.Functional.Programming.In.Java.Mar.2014.ISBN.1937785467.pdf`

**Presentation Materials:** https://drive.google.com/drive/folders/0B6lcgX18hF6BRTdoVEhxX0s0YW8?usp=sharing

---

## Project Structure

### Build System
- **Build Tool:** Gradle 2.1
- **Java Version:** 1.8 (Java 8)
- **Group:** cegeka
- **Version:** 1.0-SNAPSHOT

### Directory Layout

```
functional-programming/
├── README.md                    # Project overview and session list
├── build.gradle                 # Root Gradle configuration
├── settings.gradle              # Module definitions
├── gradlew / gradlew.bat        # Gradle wrapper scripts
├── .gitignore                   # Git ignore patterns
├── book/                        # Reference book PDF
└── practice/                    # All exercise and solution modules
    ├── session-1-start/         # Hello, Lambda Expressions (exercises)
    ├── session-1-final/         # Hello, Lambda Expressions (solutions)
    ├── session-2-start/         # Using Collections (exercises)
    ├── session-2-final/         # Using Collections (solutions)
    ├── session-3-start/         # Strings, Comparators and Filters (exercises)
    ├── session-3-final/         # Strings, Comparators and Filters (solutions)
    ├── session-5-start/         # Working with Resources (exercises)
    ├── session-5-final/         # Working with Resources (solutions)
    ├── session-6-start/         # Being Lazy (exercises)
    ├── session-6-final/         # Being Lazy (solutions)
    └── session-7-final/         # Optimizing Recursions (solutions)
```

### Session Topics

1. **Session 1:** Hello, Lambda Expressions
2. **Session 2:** Using Collections
3. **Session 3:** Strings, Comparators and Filters
4. **Session 4:** Designing with Lambda Expressions (not present in code)
5. **Session 5:** Working with Resources
6. **Session 6:** Being Lazy
7. **Session 7:** Optimizing Recursions

**Note:** Session 4 does not have corresponding code modules. Session 7 only has `-final` (solutions).

---

## Module Structure Pattern

Each session follows a consistent structure:

### Start Modules (Exercises)
```
session-X-start/
└── src/
    ├── main/java/sessionX/exercise/
    │   ├── entity/              # Domain models (Employee, Genre, etc.)
    │   └── business_logic/      # Business logic classes (exercises)
    └── test/java/sessionX/exercise/
        └── business_logic/      # JUnit tests
```

### Final Modules (Solutions)
```
session-X-final/
└── src/
    ├── main/java/sessionX/solution/
    │   ├── entity/              # Domain models
    │   ├── business_logic/      # Business logic classes (solutions)
    │   ├── api/                 # API/utility classes (when applicable)
    │   └── stream_logic/        # Stream-related logic (when applicable)
    └── test/java/sessionX/solution/
        ├── business_logic/      # JUnit tests
        └── stream_logic/        # Stream logic tests (when applicable)
```

---

## Code Conventions

### Package Naming
- **Exercises:** `sessionX.exercise.*`
- **Solutions:** `sessionX.solution.*`
- **Subpackages:** `entity`, `business_logic`, `stream_logic`, `api`

### Class Design Patterns

#### 1. Entity Classes (POJOs)
- **Immutable fields** with getters
- **Builder pattern** for object construction (nested static builder class)
- **Equals and hashCode** implementations
- Example: `Employee`, `Genre` (enum)

```java
public class Employee {
    private String firstName;
    private String lastName;
    // ... other fields

    public static class EmployeeBuilder {
        public static EmployeeBuilder employee() { ... }
        public EmployeeBuilder withFirstName(String firstName) { ... }
        public Employee build() { ... }
    }
}
```

#### 2. Business Logic Classes
- **Functional programming approach** using Java 8 Streams API
- Methods accepting `List<T>` and returning transformed results
- Use of lambda expressions, method references, and Stream operations
- Common patterns:
  - `stream()` → `map()` → `collect()`
  - `stream()` → `filter()` → `collect()`
  - `stream()` → `reduce()` / `average()` / `sum()`

#### 3. Exercise Structure
- Methods contain **TODO comments** with hints
- Empty method bodies or `return null;` placeholders
- Tests are fully implemented to validate solutions

### Testing Conventions

#### Test Framework
- **JUnit 4.12** for test execution
- **AssertJ 3.2.0** for fluent assertions

#### Test Structure
```java
@Test
public void givenCondition_whenAction_thenExpectedResult() {
    // Arrange
    List<Employee> employees = asList(...);

    // Act
    List<Employee> result = new EmployeeManagement().method(employees);

    // Assert
    assertThat(result).isEqualTo(expected);
}
```

#### Test Data Creation
- Use **builder pattern** for test objects
- **Static imports** for cleaner test code:
  ```java
  import static session2.solution.entity.Employee.EmployeeBuilder.employee;
  import static java.util.Arrays.asList;
  import static org.assertj.core.api.Assertions.assertThat;
  ```

---

## Dependencies

From `build.gradle`:
```gradle
dependencies {
    compile 'org.assertj:assertj-core:3.2.0'
    compile 'junit:junit:4.12'
}
```

**Note:** Both dependencies are marked as `compile` (should be `testCompile` in modern Gradle, but this is an older configuration).

---

## Development Workflows

### Working with Exercises

1. **Navigate to a start module:**
   ```bash
   cd practice/session-X-start
   ```

2. **Locate TODO comments** in the code (usually in `business_logic` classes)

3. **Run tests** to see failing tests:
   ```bash
   ./gradlew :practice:session-X-start:test
   ```

4. **Implement solutions** using functional programming techniques:
   - Lambda expressions
   - Method references
   - Stream API operations (map, filter, reduce, collect)
   - Optional handling

5. **Verify with tests** until all pass

6. **Compare with final module** to see reference solutions

### Adding New Sessions

1. **Create directory structure:**
   ```bash
   mkdir -p practice/session-X-start/src/{main,test}/java/sessionX/exercise/{entity,business_logic}
   mkdir -p practice/session-X-final/src/{main,test}/java/sessionX/solution/{entity,business_logic}
   ```

2. **Update `settings.gradle`:**
   ```gradle
   include 'practice:session-X-start',
           'practice:session-X-final'
   ```

3. **Follow existing package and naming conventions**

4. **Ensure tests are comprehensive** before marking as final

### Running Tests

```bash
# Run all tests
./gradlew test

# Run tests for specific module
./gradlew :practice:session-2-final:test

# Clean and build
./gradlew clean build
```

**Note:** Gradle wrapper may not work in sandboxed environments without internet access.

---

## Key Functional Programming Concepts

Based on the codebase, the following Java 8 functional programming patterns are demonstrated:

### 1. Lambda Expressions
```java
employees.stream()
    .forEach(employee -> System.out.println(employee.getName()));
```

### 2. Method References
```java
employees.stream()
    .forEach(this::printReportLine);
```

### 3. Stream Transformations
```java
employees.stream()
    .map(employee -> {
        employee.setSalary(increaseAmount(employee.getSalary(), percentage));
        return employee;
    })
    .collect(Collectors.toList());
```

### 4. Stream Filtering
```java
employees.stream()
    .filter(employee -> employee.getGenre() == genre)
    .collect(Collectors.toList());
```

### 5. Stream Reductions
```java
employees.stream()
    .filter(employee -> employee.getFunction().equals(function))
    .mapToDouble(Employee::getSalary)
    .average()
    .orElse(0);
```

### 6. Lazy Evaluation
- Streams are lazily evaluated (Session 6 focus)
- Intermediate operations are not executed until terminal operation is called

### 7. Tail Call Optimization
- Recursion optimization techniques (Session 7 focus)
- `TailCalls` utility class for trampolining

---

## Common Patterns and Idioms

### Builder Pattern Usage in Tests
```java
Employee emp = employee()
    .withFirstName("John")
    .withLastName("Doe")
    .withFunction("Developer")
    .withSalary(1000.0)
    .withGenre(MALE)
    .build();
```

### Comparator Building
```java
Comparator<Employee> comparator = Comparator
    .comparing(Employee::getLastName)
    .thenComparing(Employee::getFirstName);
```

### Collecting Results
```java
// To List
.collect(Collectors.toList())

// To Map
.collect(Collectors.toMap(keyMapper, valueMapper))

// Grouping
.collect(Collectors.groupingBy(classifier))
```

---

## Git Workflow

### Current Branch
- Working branch: `claude/claude-md-mhxzvqy8x0oum7xu-01HqppCdPtci3chJthJ3W2AR`

### Ignored Files (from `.gitignore`)
```
.gradletasknamecache, .DS_Store, .idea, *.iml
target, .gradle, build, classes
work, .vagrant, .vertex
published-artifacts-*
```

### Commit Guidelines
- Use clear, descriptive commit messages
- Format: `SESSION-X: description` (e.g., "SESSION-6: add exercises and solutions for stream generation")
- Commit related changes together

---

## AI Assistant Guidelines

### When Analyzing Code
1. **Understand the session context** - Check which functional programming topic is being covered
2. **Identify if it's an exercise or solution** - Look at package name (`exercise` vs `solution`)
3. **Read the TODO comments** - They contain important hints and requirements
4. **Check the corresponding tests** - Tests define expected behavior

### When Implementing Solutions
1. **Use functional programming style** - Prefer streams and lambda expressions over loops
2. **Follow existing patterns** - Look at similar solutions in other sessions
3. **Keep code concise** - Functional code should be expressive and readable
4. **Use method references** when appropriate - They're cleaner than lambdas for simple cases
5. **Handle edge cases** - Use `orElse()`, `orElseGet()` for Optional handling

### When Adding Tests
1. **Follow naming convention:** `givenX_whenY_thenZ`
2. **Use AssertJ assertions** - More readable than JUnit assertions
3. **Use static imports** - Makes test code cleaner
4. **Create test data with builders** - Consistent with existing tests
5. **Test edge cases** - Empty lists, null values, boundary conditions

### When Refactoring
1. **Run tests first** - Ensure they pass before refactoring
2. **Maintain backward compatibility** - Don't change test expectations unless required
3. **Keep functional style** - Don't revert to imperative code
4. **Document complex operations** - Add comments for non-obvious stream chains

### Code Quality Standards
- **Java 8 features required** - This is a functional programming course
- **No raw types** - Use generics properly
- **Avoid side effects** - Prefer pure functions when possible
- **Immutability preferred** - Minimize mutable state
- **Stream operations should be readable** - Break complex chains into smaller methods

---

## Troubleshooting

### Gradle Issues
- **Wrapper fails:** Use local Gradle installation (`gradle` command)
- **Compilation errors:** Ensure Java 8+ is being used
- **Test failures:** Check if exercise methods are implemented

### Common Mistakes
1. **Using imperative loops instead of streams** - This defeats the learning purpose
2. **Modifying collections during iteration** - Use stream transformations instead
3. **Not handling Optional properly** - Always provide fallback with `orElse()`
4. **Forgetting to collect stream results** - Streams are lazy and need terminal operations

### Package Structure Errors
- Ensure package names match directory structure
- Exercise code goes in `sessionX.exercise.*`
- Solution code goes in `sessionX.solution.*`

---

## Resources

- **Book PDF:** `/book/Pragmatic.Bookshelf.Functional.Programming.In.Java.Mar.2014.ISBN.1937785467.pdf`
- **Presentations:** https://drive.google.com/drive/folders/0B6lcgX18hF6BRTdoVEhxX0s0YW8?usp=sharing
- **Java 8 Documentation:** https://docs.oracle.com/javase/8/docs/api/
- **Stream API Javadoc:** https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html

---

## Quick Reference

### File Locations
- **Entity classes:** `src/main/java/sessionX/{exercise|solution}/entity/`
- **Business logic:** `src/main/java/sessionX/{exercise|solution}/business_logic/`
- **Tests:** `src/test/java/sessionX/{exercise|solution}/`
- **Solutions:** Compare `-start` with `-final` modules

### Common Operations
```bash
# Run specific session tests
./gradlew :practice:session-2-final:test

# Build all modules
./gradlew build

# Clean build artifacts
./gradlew clean

# List all tasks
./gradlew tasks
```

---

## Version History

- **v1.0-SNAPSHOT** - Current version
- Educational repository for internal reading group
- Based on Java 8 (sourceCompatibility 1.8)

---

**Last Updated:** 2025-11-13
**Maintainer:** Cegeka Reading Group
**Purpose:** Educational exercises for functional programming in Java
