# Program Kavramı

'Program' içerisinde sınıfları, tipleri, methodları, değişkenleri tanımlayabileceğiniz genel nesnedir(global object).

```crystal
# Program içerisinde bir method tanımlama
def ekle(x, y)
  x + y
end

# Program içerisinden ekle methodunu çağırma
ekle(1, 2) #=> 3
```

Methodun dönüş değeri(value), en son çalıştığında çıkandır ve `return` yazmamıza gerek yoktur. Ancak isterseniz `return` yazmak da mümkündür:

```crystal
def cift?(sayi)
  if sayi % 2 == 0
    return true
  end

  return false
end
```

Sınıf içerisinde alıcısı(receiver) olmadan bir method çağırdığınızda, ekle(1, 2) gibi, eğer miras(inherit) aldığı sınıflarda ya da kendi içerisinde bulunamazsa program içerisinde aranacaktır.

```crystal
def ekle(x, y)
  x + y
end

class Foo
  def bar
    # ekle methodunu çağırır
    ekle(1, 2)

    # Foo sınıfının baz methodunu çağırır
    baz(1, 2)
  end

  def baz(x, y)
    x * y
  end
end
```

Kendi sınıfınız içerisinde tanımlı olmasına rağmen aynı isme sahip, sınıf dışındaki methodu kullanmak istiyorsanız, methodun önüne
`::` yazarak çağırabilirsiniz:

```crystal
def baz(x, y)
  x + y
end

class Foo
  def bar
    baz(4, 2) #=> 2
    ::baz(4, 2) #=> 6
  end

  def baz(x, y)
    x - y
  end
end
```

Program içerisinde tanımlanmış değişkenler method içerisinden erişilemez:

```crystal
x = 1

def ekle(y)
  x + y # error: undefined local variable or method 'x'
end

add(2)
```

Method yazımlarında parantez kullanımı tercihe bağlıdır:

```crystal
ekle 1, 2 # şununla aynı: ekle(1, 2)
```
