# Çoklu atama

Virgül(,) ile ifadeleri ayırarak aynı anda birden fazla değişkene atama/deklare yapabilirsiniz.

```crystal
name, age = "Crystal", 1

# The above is the same as this:
temp1 = "Crystal"
temp2 = 1
name  = temp1
age   = temp2
```

Dikkat tek satırda değişkenlerin içeriğini değiştirmek mümkündür çünkü ifadeler geçici değişkenlere atanır.

```crystal
a = 1
b = 2
a, b = b, a
a #=> 2
b #=> 1
```

Eğer sağ taraf tek bir ifade içeriyorsa, sıralanmış tip kabul edilir ve takip eden sözdizimsel şekeri uygular:

```crystal
name, age, source = "Crystal,1,github".split(",")

# The above is the same as this:
temp = "Crystal,1,github".split(",")
name   = temp[0]
age    = temp[1]
source = temp[2]
```

Eğer sol taraf tek bir değişken içeriyorsa, sağ taraf bir array kabul edilir:

```crystal
names = "John", "Peter", "Jack"

# The above is the same as:
names = ["John", "Peter", "Jack"]
```

Çoklu atamada `=` ile sonlanan yöntemler de mevcuttur:

```crystal
person.name, person.age = "John", 32

# Same as:
temp1 = "John"
temp2 = 32
person.name = temp1
person.age = temp2
```

TODO indexers
Ve aynı zamanda indexers(`[]=`) mevcuttur:

```crystal
objects[1], objects[2] = 3, 4

# Same as:
temp1 = 3
temp2 = 4
objects[1] = temp1
objects[2] = temp2
```
