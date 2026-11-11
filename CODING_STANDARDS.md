# Coding standards

## Java code style

* Add short, human-readable Javadoc to every test method.
* One-line comments should start with //, not /\*\* ... \*/.
* No need to check each argument/variable using Objects.requireNonNull
* Use multiline Javadoc blocks when code documentation is needed.
* Format Stream API chains with each call after the stream source on a new line, indented by four spaces. Include terminal operations and chained calls on their results, even when the chain would fit on one line.

```java
modules.stream()
    .filter(ServiceModule.class::isInstance)
    .map(ServiceModule.class::cast)
    .findFirst()
    .orElseGet(ServiceModule::new);
```

## Object construction

Keep ordinary object construction direct. Do not add defensive `try`/`catch` blocks
around constructors or factory calls solely to close or free previously created
objects if construction fails. Do not catch `RuntimeException` or `Error` for this
purpose by default.

Cleanup for an explicit lifecycle operation that can fail after resources become
active, such as a startup connectivity check, is a separate concern.

## Enum IDs

Give enums explicit IDs when used in configuration or encoded data; never use `ordinal()`.
Implement `fromId()` with an immutable lookup map built once from those IDs.
Reject duplicate and unknown IDs. See the [enum ID reference example](ENUM_ID_EXAMPLE.md).
