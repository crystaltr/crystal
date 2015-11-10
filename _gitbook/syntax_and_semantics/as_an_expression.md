# Değer olarak kullanımı

Değişken `if` bloklarının her birinde bulunan son ifadenin değeridir.

```crystal
a = if 2 > 1
      3
    else
      4
    end
a #=> 3
```

Eğer bir `if` bloğunun biri boş ise ya da belirtilmemişse, değişkenin içinde `nil` varmış gibi kabul edilmelidir:

```crystal
if 1 > 2
  3
end

# Yukarıdaki kullanmın aynısıdır:
if 1 > 2
  3
else
  nil
end

# Bir diğer örnek:
if 1 > 2
else
  3
end

# Yukarıdaki kullanımın aynısıdır:
if 1 > 2
  nil
else
  3
end
```
