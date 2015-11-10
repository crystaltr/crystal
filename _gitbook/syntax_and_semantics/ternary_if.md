# Üçlü if

The ternary `if` allows writing an `if` in a shorter way:
Üçlü `if`, kısa şekilde `if` yazımına olanak sağlar.

```crystal
a = 1 > 2 ? 3 : 4

# Yukarıdaki kullanımın aynısıdır:
a = if 1 > 2
      3
    else
      4
    end
```
