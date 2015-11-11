# if var

Eğer bir değişken `if` koşulu içindeyse, `then` bloğu içinde `Nil` tipinde olmayacağı kabul edilir:

```crystal
a = some_condition ? nil : 3
# a is Int32 or Nil

if a
  # Since the only way to get here is if a is truthy,
  # a can't be nil. So here a is Int32.
  a.abs
end
```

Bir if koşulu içinde bir değişkene atama yapıldığı zaman içinde geçerlidir:

```crystal
if a = some_expression
  # here a is not nil
end
```

Eğer koşul içinde ve(`&&`) varsa mantık(logic) yapısı geçerlidir.

```crystal
if a && b
  # here both a and b are guaranteed not to be Nil
end
```

Burada, `&&` ifadesinin sağ tarafında `a`'nın `Nil` olmadığı garantidir.

Tabiki, bir değişkene `then` bloğu içinde tekrar atama yapılırsa değişkenin atama ifadesine bağlı yeni bir tipi olur.

Yukarıdaki mantık ifadesi instance değişkenler, class(sınıf) değişkenleri veya global değişkenler ile **çalışmaz**:

```crystal
if @a
  # here @a can be nil
end
```

Bunun nedeni ise herhangi method çağrısının instance değişkenini etkileme olasılığıdır, onu `nil` şeklinde yorumlar. Bir diğer nedeni ise diğer threadlerin instance değişkeni koşuldan sonra değiştirebilmesidir.

Yalnızca `nil` olmayan `@a` ile bir şeyler yapmak için iki seçeneğiniz vardır:

```crystal
# First option: assign it to a variable
if a = @a
  # here a can't be nil
end

# Second option: use `Object#try` found in the standard library
@a.try do |a|
  # here a can't be nil
end
```

Bu mantık yapısı, getter ve özellikleri(properties) içeren proc ve method çağrıları ile de çalışmıyor, çünkü nilable(veya, daha genel union tipli) proc'lar ve methodlar peş peşe aynı çağrılarda aynı tip dönmeyi garanti etmezler.

```crystal
if method # first call to a method that can return Int32 or Nil
          # here we know that the first call did not return Nil
  method  # second call can still return Int32 or Nil
end
```

Instance değişkenler için yukarıda açıklanan teknikler, proc ve method çağrıları için de çalışacaktır
