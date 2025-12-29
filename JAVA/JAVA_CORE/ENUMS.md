# Enums in Java

Enums (short for "enumerations") in Java are a special data type that enables a variable to be a set of predefined constants. They are used to represent a fixed set of related values in a type-safe manner.

## Defining an Enum

```java
public enum Day {
    SUNDAY,
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY
}
```

Internally it creates a final Day class that extends `java.lang.Enum`.

`ordinal()` method returns the position of each enum constant (starting from 0).

`valueOf(String name)` method returns the enum constant with the specified name, or throws an IllegalArgumentException if no such constant exists, what it does is compare the given string with the names of the enum constants.

`values()` method returns an array containing all the enum constants in the order they are declared.

Methods can also be defined within an enum.

```java
public enum Day {
    SUNDAY,
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY;

    public boolean isWeekend() {
        return this == SUNDAY || this == SATURDAY;
    }
}
```

fields and constructors can also be defined within an enum.

Custom constructor
eg 
SUNDAY("Sun"), MONDAY("Mon")...

We can also do switch case on enums.
i.e.

```java
String res=switch(day) {
    case MONDAY -> "Start of the work week";
    case FRIDAY -> "End of the work week";
    case SATURDAY, SUNDAY -> "It's weekend!";
    default -> "Midweek day";
};
```

