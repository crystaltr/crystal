# alias

`alias` kullanarak bir tipe başka bir isim verebilirsiniz:

```crystal
alias PInt32 = Pointer(Int32)

ptr = PInt32.malloc(1) # :: Pointer(Int32)
```

Bir alias kullanıldığında derleyici bunu refere ettiği tiple ile değiştirir.

`alias`lar uzun tip isimlerini yazmanızı önlemesi sayesinde oldukça kullanışlıdır.
Bunun yanında özyinelemeli tiplerden de bahsedebilmemizi sağlar.

```crystal
alias RecArray = Array(Int32) | Array(RecArray)

ary = [] of RecArray
ary.push [1, 2, 3]
ary.push ary
ary #=> [[1, 2, 3], [...]]
```

Gerçek hayatta karşımıza çıkan en yaygın özyinelemeli tiplerden biri ise json'dır.

```crystal
module Json
  alias Type = Nil |
               Bool |
               Int64 |
               Float64 |
               String |
               Array(Type) |
               Hash(String, Type)
end
```
