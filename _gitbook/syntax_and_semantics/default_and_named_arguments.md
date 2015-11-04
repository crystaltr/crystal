# Varsayılan(default) ve isimli argümanlar(named arguments)

Bir method son agrümanları için varsayılan değerler belirtebilir:


```crystal
class Person
  def become_older(by = 1)
    @age += by
  end
end

john = Person.new "John"
john.age #=> 0

john.become_older
john.age #=> 1

john.become_older 2
john.age #=> 3
```

Ayrıca methodu çağırırken de varsayılan argümanı kullanarak farklı değer atayabilirsiniz:

```crystal
john.become_older by: 5
```

Methodun bir çok varsayılan argümanı olduğunda, methodu çağırma sırasında tanımlanan argümanların sırası önemsizdir ve bazı argümanları isterseniz atlayabilirsiniz:

```crystal
def some_method(x, y = 1, z = 2, w = 3)
  # do something...
end

some_method 10 # x = 10, y = 1, z = 2, w = 3
some_method 10, z: 10 # x = 10, y = 1, z = 10, w = 3
some_method 10, w: 1, y: 2, z: 3 # x = 10, y = 2, z = 3, w = 1
```

Yukarıdaki örnekte `x` argümanini paslarken `x: 10` şeklinde kullanamayız, çünkü varsayılan bir değeri bulunmamakta.

Bu arada, default argümanlar ve isimli argümanlar birbirleriyle ilişkilidir: default argüman tanımladığınız zaman ayrıca çağırdığınız methoda da isimlerini kullanmaya izin veriyorsunuz. İsim seçimi yaparken akıllıca davranın ve iyi isimler seçin.
