# Code Commenting Standards

## 1. Objective

Generate comprehensive, professional, senior-engineer-level comments for all source code.

Comments must prioritize:

* Maintainability
* Readability
* Knowledge transfer
* Long-term support
* Understanding of business logic and technical intent

The goal is that a developer unfamiliar with the project can understand the purpose, behavior, constraints, assumptions, and reasoning behind the code without reverse-engineering the implementation.

---

# 2. File Header Requirements

Immediately below the package declaration, add a file-level documentation block.

```java
/**
 * Purpose:
 * <Detailed description of the file's responsibility and role in the system>
 *
 * Owner:
 * <TO_BE_FILLED>
 *
 * Version:
 * <Version number>
 */
```

### Requirements

* Explain why the file exists.
* Explain what business or technical problem it solves.
* Describe major responsibilities.
* Do not simply restate the class name.
* Minimum 3–5 meaningful sentences.
* Use professional technical language.
* Avoid generic descriptions.

---

# 3. Ownership and Versioning

Every file must contain:

```text
Owner:
P.B.R. - https://github.com/PBR208/

Version:
1.0
```

### Rules

* Never invent an owner.
* Always use the placeholder when an owner is not provided.
* Use Semantic Versioning whenever possible (`MAJOR.MINOR.PATCH`).

---

# 4. Terminology Rules

## pAttribute Convention

The prefix `p` indicates a passed attribute (input parameter).

### Examples

```java
String pUserId;
int pRetryCount;
```

Documentation must describe:

* Purpose
* Expected value
* Constraints
* Nullability

### Example

```java
@param pUserId
Unique identifier of the user. Must not be null or empty.
```

---

# 5. Line-by-Line Commenting

Every executable line of code must be commented.

### Example

```java
// Retrieve user information from the persistence layer
User user = repository.findById(pUserId);

// Validate the retrieved user object before processing
validateUser(user);
```

### Requirements

* Explain intent, not syntax.
* Explain why the operation is performed.
* Explain business reasoning when applicable.
* Avoid redundant comments.

### Bad Example

```java
// Set value to 5
int count = 5;
```

### Good Example

```java
// Initialize retry counter with the maximum allowed retry attempts
int retryCount = 5;
```

---

# 6. Class Documentation

Every class, interface, enum, and record must contain a documentation block.

### Include

* Responsibility
* Scope
* Dependencies
* Thread-safety considerations
* Lifecycle information
* Architectural role

### Example

```java
/**
 * Service responsible for processing customer orders.
 *
 * Coordinates validation, pricing, and persistence operations.
 * Acts as the primary entry point for order creation workflows.
 */
```

---

# 7. Method Documentation

Every method must contain a complete documentation block.

### Template

```java
/**
 * Brief summary.
 *
 * Detailed explanation of:
 * - Purpose
 * - Business context
 * - Processing steps
 * - Assumptions
 * - Side effects
 *
 * @param ...
 * @return ...
 * @throws ...
 */
```

### Requirements

* Minimum 2–3 meaningful sentences.
* Explain business intent.
* Explain technical intent.
* Explain non-obvious implementation decisions.

---

# 8. @param Requirements

Every parameter must be documented.

### Must Include

* Purpose
* Expected values
* Valid ranges
* Nullability
* Special behavior
* Business significance when applicable

### Example

```java
@param pTimeoutSeconds
Maximum time in seconds before the operation is aborted.
Must be greater than zero.
```

---

# 9. @return Requirements

Every return value must be documented.

### Must Explain

* Meaning of the returned value
* Success conditions
* Failure conditions
* Nullability
* Business implications

### Example

```java
@return
The persisted customer entity including generated identifiers.
Returns null only when persistence is disabled by configuration.
```

---

# 10. @throws Requirements

Every possible exception must be documented.

### Example

```java
@throws IllegalArgumentException
Thrown when pUserId is null or empty.
```

### Rules

* Explain why the exception occurs.
* Explain triggering conditions.
* Explain impact where relevant.

---

# 11. Variable Documentation

Important variables must be documented.

### Explain

* Why the variable exists
* Expected contents
* Lifecycle
* Scope of use

### Example

```java
// Stores the timestamp of the last successful synchronization
LocalDateTime lastSyncTimestamp;
```

---

# 12. Business Logic Documentation

Whenever business rules are implemented, explain:

* Why the rule exists
* Regulatory requirements
* Product requirements
* Impact of changing the rule

### Example

```java
// Regulatory requirement: customers under 18 cannot create investment accounts
if (customerAge < 18)
```

---

# 13. Complex Logic Documentation

For:

* Algorithms
* Calculations
* Decision trees
* Nested conditions
* State transitions

Provide:

* High-level explanation
* Inputs
* Outputs
* Assumptions
* Expected outcome

### Example

```java
/*
 * Pricing calculation:
 * 1. Determine base product price.
 * 2. Apply customer-specific discounts.
 * 3. Apply regional tax adjustments.
 * 4. Round according to financial standards.
 */
```

---

# 14. Null Handling Documentation

Whenever null checks exist, explain why.

### Example

```java
// Defensive validation because upstream systems may omit this value
if (customer == null)
```

Never leave null handling unexplained.

---

# 15. Logging Documentation

Log statements should be documented whenever their purpose is not obvious.

### Explain

* Why the log exists
* Monitoring purpose
* Operational value
* Troubleshooting value

### Example

```java
// Log external service response time for SLA monitoring
logger.info(...)
```

---

# 16. TODO Documentation

Every TODO must follow the format:

```java
// TODO [Owner]: Description of work required.
```

### Example

```java
// TODO [PlatformTeam]: Replace temporary cache implementation with Redis integration.
```

---

# 17. Magic Numbers

Never leave unexplained numeric literals in code.

### Bad Example

```java
if (retryCount > 5)
```

### Good Example

```java
// Maximum retry attempts permitted by integration requirements
if (retryCount > MAX_RETRY_ATTEMPTS)
```

---

# 18. Architectural Documentation

When a class participates in a larger architecture, explain:

* Its architectural role
* Upstream dependencies
* Downstream consumers
* Integration points

---

# 19. Performance-Critical Code

Document:

* Performance considerations
* Complexity concerns
* Caching strategies
* Optimization rationale

### Example

```java
// Cache lookup used to avoid repeated database access during batch processing
```

---

# 20. Security Documentation

Whenever security-related code is encountered, explain:

* Security purpose
* Threat being mitigated
* Validation requirements
* Compliance considerations

### Example

```java
// Validate ownership to prevent unauthorized access to customer records
```

---

# 21. Concurrency Documentation

Whenever multithreading or asynchronous processing exists, document:

* Thread-safety assumptions
* Synchronization strategy
* Potential race conditions
* Locking rationale

---

# 22. API Documentation

For external APIs and integrations, document:

* External system purpose
* Expected response behavior
* Error handling strategy
* Retry considerations

---

# 23. Comment Quality Standards

Comments must:

* Explain intent
* Explain business reasoning
* Explain technical reasoning
* Explain assumptions
* Explain constraints
* Explain side effects
* Explain risks
* Use complete sentences
* Use professional English
* Be understandable by a new team member

Comments must NOT:

* Repeat code literally
* State obvious syntax
* Use informal language
* Use jokes or sarcasm
* Use vague descriptions
* Use placeholders such as "magic happens here"
* Use "self-explanatory"
* Use "obvious"

---

# 24. Senior Engineer Expectations

The AI must document code as if:

* Performing a formal code review
* Preparing the codebase for long-term maintenance
* Supporting future developers with no project knowledge
* Preserving architectural context
* Preserving business context
* Reducing the need to inspect implementation details

When uncertain, provide more context rather than less while remaining concise, precise, and technically accurate.

---

# 25. Final Rule

When generating comments:

1. Explain **what** the code does.
2. Explain **why** it exists.
3. Explain **when** it is used.
4. Explain **how** it affects the system.
5. Explain any assumptions, constraints, risks, and side effects.

The generated documentation must reflect the standards and expectations of a senior software engineer maintaining an enterprise-grade codebase.
