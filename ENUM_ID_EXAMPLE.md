# Enum ID reference example

```java
public enum Version {
    V1(1),
    V2(2);

    private static final List<Version> VALUES = List.of(Version.values());
    private static final Map<Integer, Version> MAP = VALUES.stream()
        .collect(Collectors.toUnmodifiableMap(Version::id, Function.identity()));

    private final int id;

    Version(int id) {
        this.id = id;
    }

    /**
     * Returns the stable numeric ID.
     */
    public int id() {
        return id;
    }

    /**
     * @throws IllegalArgumentException if the ID is unsupported
     */
    public static Version fromId(int id) {
        Version version = MAP.get(id);
        Preconditions.checkArgument(version != null, "Unsupported version ID: " + id);
        return version;
    }
}
```
