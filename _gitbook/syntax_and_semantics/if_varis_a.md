# if var.is_a?(...)

`if` koşulu bir `is_a?` testi ise, bir değişkenin tipi `then` bloğunda bu tip ile sınırlı olması garanti edilir.

```crystal
if a.is_a?(String)
  # Burada String
end

if b.is_a?(Number)
  # Buarada b bir Number dır
end
```

Ayrıca, `else` bloğundaki değişkenin tipi bu tipte olmadığı garanti edilir.

```crystal
a = some_condition ? 1 : "hello"
# a :: Int32 | String

if a.is_a?(Number)
  # a :: Int32
else
  # a :: String
end
```

`is_a?` testini soyut sınıflar ve modüller gibi her tipde kullanabileceğinizi unutmayın.

Aynı zamanda yukarıdaki örnek and (`&&`) operatörleri ilede çalışır:

```crystal
if a.is_a?(String) && b.is_a?(Number)
  # here a is a String and b is a Number
end
```

Yukarıdaki örnek, static olmayan değişkenleri, sınıf değişkenleri ya da global değişkenler kullanıldığında **çalışmaz**. Eğer bunları kullanmak istiyorsanız farklı bir değişkene atamalısınız:

```crystal
if @a.is_a?(String)
  # burada @a bir String olacağı garanti edilmez
end

a = @a
if a.is_a?(String)
  # a nın String olacağı garanti edilir.
end

# A bit shorter:
if (a = @a).is_a?(String)
  # burada da a nın bir String olacağı garanti edilir.
end
```
