# Splats and tuples

Bir method *splat* (`*`) işaretini kullanarak bir değişken alır. Bu değişken bir argumanlar dizisini temsil eder. Method herhangi bir sırada ya da sayıda arguman alabilir:

```crystal
def sum(*elements)
  total = 0
  elements.each do |value|
    total += value
  end
  total
end

sum 1, 2, 3      #=> 6
sum 1, 2, 3, 4.5 #=> 10.5
```

Girilen argümanlar methodun içerisinde [Tuple](http://crystal-lang.org/api/Tuple.html) olur:

```crystal
# elements is Tuple(Int32, Int32, Int32)
sum 1, 2, 3

# elements is Tuple(Int32, Int32, Int32, Float64)
sum 1, 2, 3, 4.5
```
