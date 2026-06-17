# Plume
Lightweight programming language

## Safety

### Definitions

- **Type Safety**: The _values_ are always valid.
- **Memory Safety**: The _references_ are always valid.
- **Thread Safety**: Correctness (including Type and Memory Safety) is always maintained when _distributing_ execution.

### Implementation

#### First Approximation

- Type Safety:
    - Baseline:
        - **Always initialize variables with valid values before use.**
    - Invariants:
        - **Always verify that values are valid before and after performing operations on them, and handle them when they're not.**
        - _No conversion between types._
- Memory Safety:
    - **A reference is a type of value, so the same applies from Type Safety.**
    - Invariants:
        - _No null references._
        - _No pointer arithmetics._
    - Dynamics:
        - **Stack Allocation:**
            - **Never escape object's scope.**
        - _No heap allocation._
- Thread Safety:
    - _No distributed execution._

#### Second Approximation

- Type Safety:
    - Invariants:
        - **Always preserve the relevant information semantics when converting between types.**
- Memory Safety:
    - Invariants:
        - **Always check for null references.**
        - **Always check boundaries / Never do arbitrary pointer arithmetics.**
        - **Never convert other types of value to references.**
    - Dynamics:
        - **Heap Allocation:**
            - _Never free / deallocate._

#### Third Approximation

- Memory Safety:
    - Dynamics:
        - Heap Allocation:
            - **UML Class Diagram Instance-Level Relationships -> Reference Type:**
                - **Composition -> Strong Reference:**
                    - **Owning reference -> Controls object lifecycle.**
                - **Association / Aggregation -> Weak Reference:**
                    - **Non-owning reference -> Doesn't control object lifecycle.**
            - **If there are multiple strong (owning) references:**
                - **(Weighted) reference counting of strong references (weak references are not counted).**
            - **If there are any weak (non-owning) references:**
                - **Both strong and weak references are (random) generational references.**
