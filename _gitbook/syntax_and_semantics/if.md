# if

`if` içindeki koşul doğru ise `then` bloğunu değerlendirir, aksi halde `else` bloğunu değerlendirir.

```crystal
a = 1
if a > 0
  a = 10
end
a #=> 10

b = 1
if b > 2
  b = 10
else
  b = 20
end
b #=> 20
```

if-else-if basamak yapısı için `elsif` kullanabilirsiniz:

```crystal
if some_condition
  do_something
elsif some_other_condition
  do_something_else
else
  do_that
end
```

`if` kullandıktan sonra, değişkenin tipi her iki blokda da kullanılan ifadelerin tipine bağlıdır. 

```crystal
a = 1
if some_condition
  a = "hello"
else
  a = true
end
# a :: String | Bool

b = 1
if some_condition
  b = "hello"
end
# b :: Int32 | String

if some_condition
  c = 1
else
  c = "hello"
end
# c :: Int32 | String

if some_condition
  d = 1
end
# d :: Int32 | Nil
```

Bir değişken bir blokda tanımlanıp, diğerinde tanımlanmadıysa, if bloğunun sonunda `Nil` tipini de içerir.

`if` bloğunun içindeki değişkenin tipi bloğun içinde atama yapılan değerin tipidir, eğer atama yapılmadıysa bloktan önceki değişkenin tipini alır:


```crystal
a = 1
if some_condition
  a = "hello"
  # a :: String
  a.size
end
# a :: String | Int32
```

Burada, bir değişkenin tipi atanan son değerin tipidir.

Eğer `return`, `next`, `break` ya da `raise` durumlarında olduğu gibi bloklardan biri tamamlanmıyorsa, değişkenin tipi o bloğa girmemiş gibi düşünülmelidir.

```crystal
if some_condition
  e = 1
else
  e = "hello"
  # e :: String
  return
end
# e :: Int32
```
