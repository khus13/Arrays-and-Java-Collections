# Arrays-and-Java-Collections
A set of information containing the proper usage, difference and distinctions regarding Arrays and Collections in Java

## Java Arrays & Collections - Quick Reference

Notes from CIS-2103: Arrays, ArrayList, HashSet, HashMap.

---

## 1. Arrays

Fixed-size, ordered, index-based. Can hold primitives (`int`, `double`) or objects.

### Creating

```java
// Approach 1: Empty slots (size upfront, filled with defaults)
String[] roster = new String[5];
int[] scores = new int[3];

// Approach 2: Instant initialization (size inferred)
String[] names = {"Ali", "Bob", "Cam"};
int[] luckyNums = {7, 99};
```

**Default values:** objects (`String`) = `null`, numbers (`int`) = `0`, `boolean` = `false`.

### Looping

```java
String[] names = {"Ali", "Bob"};

// Standard for-loop: use when you need the index
for (int i = 0; i < names.length; i++) {
    System.out.println(i + ": " + names[i]);   // 0: Ali, 1: Bob
}

// Enhanced for-each: use when you only need the values
for (String n : names) {
    System.out.println("Name: " + n);          // Name: Ali, Name: Bob
}
```

### Helper methods (`java.util.Arrays`)

| Task | Code | Result |
|---|---|---|
| Print an array | `Arrays.toString(new int[]{1, 2, 3})` | `[1, 2, 3]` |
| Sort | `Arrays.sort(new int[]{9, 1, 5})` | `[1, 5, 9]` |
| Fill with same value | `Arrays.fill(new int[3], 42)` | `[42, 42, 42]` |

### Common pitfalls

1. **Out of bounds (off-by-one):** `int[] arr = new int[3]; arr[3] = 99;` crashes. Valid indexes are 0, 1, 2.
2. **`length` vs `length()`:** arrays use the property `arr.length`. `arr.length()` is a compile error.
3. **Size is permanent:** you cannot add to an array once created. Use an `ArrayList` if you need to grow.

---

## 2. ArrayList - the growing line

Like a numbered line of students: when someone new arrives, the line stretches automatically.

```java
ArrayList<String> roster = new ArrayList<>();
roster.add("Ali");
roster.add("Bob");
roster.add("Cam");               // no crash, it grows
System.out.println(roster.get(2));          // Cam
System.out.println("Size: " + roster.size());
```

- Maintains insertion order
- Accessible by index
- Allows duplicates
- **Objects only** - use wrappers (`Integer`, not `int`)

### Array vs. ArrayList

| Feature | Array `[]` | ArrayList |
|---|---|---|
| Size | Fixed forever | Grows automatically |
| Write | `arr[0] = "Ali";` | `list.add("Ali");` |
| Read | `String s = arr[0];` | `String s = list.get(0);` |
| Get count | `arr.length` (property) | `list.size()` (method) |
| Primitives? | Yes (`int`, `double`) | No (objects only) |

---

## 3. HashMap — key/value lookups

```java
HashMap<String, String> students = new HashMap<>();
students.put("15101440", "Rannzel");
students.put("15101441", "Lim");
```

---

## 4. Choosing your structure

| Structure | Size | Ordered? | Duplicates? | Best used for |
|---|---|---|---|---|
| Array `[]` | Fixed | Yes (index) | Allowed | Fixed, known limits (e.g. days of week) |
| ArrayList | Grows | Yes (index) | Allowed | Dynamic lists, rankings |
| HashSet | Grows | No | **No** | Unique filters, memberships |
| HashMap | Grows | No | Keys: **No** | Lookups, dictionaries, registries |

---

## 5. Cheat sheet

```java
// Array (fixed size)
String[] arr = new String[5];
arr[0] = "Apple";
String s = arr[0];
int size = arr.length;            // property

// ArrayList (ordered, grows)
ArrayList<String> list = new ArrayList<>();
list.add("Apple");
String s = list.get(0);
int size = list.size();           // method

// HashSet (unique only)
HashSet<Integer> set = new HashSet<>();
set.add(10);                      // a second add(10) is ignored
boolean has = set.contains(10);
set.remove(10);

// HashMap (key/value)
HashMap<String, Double> map = new HashMap<>();
map.put("Gas", 3.50);
Double cost = map.get("Gas");
boolean has = map.containsKey("Gas");
```

---

## 6. Summary

**Top 3 takeaways**
- Arrays are fast and simple, but permanently fixed in size.
- Collections (List, Set, Map) grow dynamically.
- Generics (`<>`) enforce type safety for objects inside collections.

**Traps to avoid**
- Off-by-one errors (`arr.length` vs the last valid index, which is `length - 1`).
- Using primitives (`int`) instead of wrappers (`Integer`) in generics.
- Confusing `.length` (array) with `.size()` (collection).
