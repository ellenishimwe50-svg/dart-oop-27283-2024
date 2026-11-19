# Dart OOP Assignment: Kigali Bus Card

**Name:** Ishimwe Ellen
**Student ID:** 27283/2024

## My numbers

- D = 24, L = 4
- Starting balance = 1000 + (24 × 10) = 1240 RWF
- Bus fare = 200 + 24 = 224 RWF
- Student discount = 10 + 4 = 14%

## Output of main.dart

```
Error: name too short
Owner: Ellen | Balance: 1240 RWF
Owner: Ishimwe Ellen | Balance: 1240 RWF
Error: top-up must be 500 to 50000 RWF
Topped up 2000 RWF
Paid 224 RWF
Paid 224 RWF
Owner: Ishimwe Ellen | Balance: 2792 RWF
Student discount: 31 RWF
Paid 193 RWF
Owner: Ishimwe Ellen | Balance: 1047 RWF
Student card: 14% off
```

## Part 1: Why no setter for balance?

If there was a setter, anyone could write `card.balance = 999999` and give themselves free money. Without a setter, the balance can only change through `topUp` and `pay`, and both of them check the rules first. This keeps the money safe.

## Part 2: What does ~/ do?

`/` is normal division and gives a decimal number. `~/` is integer division: it divides and throws away the decimal part.

```dart
print(237 * 17 / 100);   // 40.29
print(237 * 17 ~/ 100);  // 40
```

In the student card, `~/` gives a whole number of RWF for the discount (no cents).

## Part 4: Bug table

| Bug | The line | Why it is wrong (your words) | Your fix |
|-----|----------|------------------------------|----------|
| 1 | `String _brand;` and `int _battery;` | The fields have no starting value, and Dart does not allow a non-nullable field to start empty. | `String _brand = '';` and `int _battery = 0;` |
| 2 | `SmartPhone(String brand, int battery, String system) {` | The child constructor does not build the parent Phone first, and Phone needs brand and battery. | Add `: super(brand, battery)` after the parameters. |
| 3 | `@override` above `void restart()` | `@override` only works if the parent has that method. Phone has no `restart`. | Remove `@override`. |
| 4 | `p.battery = 100;` | There is a getter for battery but no setter, so it cannot be assigned. | Add `set battery(int value)` that accepts only 0 to 100. |
| 5 | `print(p.battery());` | `battery` is a getter, so it is used like a field. Writing `()` treats it like a method. | `print(p.battery);` |
| Not a bug | `Phone p = new Phone('Tecno', 50);` | The `new` keyword is old style but still allowed in Dart. It works the same as `Phone('Tecno', 50)`. | (none) |

The fixed program prints `100`.

## Part 5

My prediction:

```
1
5
```

Why: For `Bag a`, `add()` makes items 1. Then `a.items = -5` is refused because the setter only accepts 0 or more, so items stays 1 and it prints 1. For `BigBag b`, each `add()` calls `super.add()` two times, so it adds 2. Two calls make 4. Then `b.items = b.items + 1` sets it to 5, which is allowed, so it prints 5.

Real output:

```
1
5
```

Was I right? Yes, the real output matches my prediction.
