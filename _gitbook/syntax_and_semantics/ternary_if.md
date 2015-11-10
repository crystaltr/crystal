# Ternary if (Üçlü if)

Ternary `if`, kısa şekilde `if` yazımına olanak sağlar.

```crystal
a = 1 > 2 ? 3 : 4

# Yukarıdaki kullanımın aynısıdır:
a = if 1 > 2
      3
    else
      4
    end
```
