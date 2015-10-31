# Array

Bir [Array](http://crystal-lang.org/api/Array.html) 'T' tipinde elemanları olan genel bir tiptir.
Bir array değişmezi genellikle şöyle tanımlanır:

```crystal
[1, 2, 3]         # Array(Int32)
[1, "hello", 'x'] # Array(Int32 | String | Char)
```

Bir Array karışık türler içerebilir, yani `T`  tiplerin birleşimi olabilir ama bunlar array oluşturulduğunda belirlenir, veya T belirtilir ya da bir array değişmezi kullanılır. Son durumda, T array elemanlarının birleşimine denk gelir.

Boş bir array yaratırken her zaman T'yi belirtmek zorundasınız:

```crystal
[] of Int32 # Array(Int32).new ile aynı
[]          # syntax error
```

## String'lerin Array'i

String'leri içeren Array özel bir sözdizimi ile yaratılabilir:

```crystal
%w(one two three) # ["one", "two", "three"]
```

## Symbol'lerin Array'i

Symboller'i içeren Array özel bir sözdizimi ile yaratılabilir:

```crystal
%i(one two three) # [:one, :two, :three]
```

## Array'e benzeyen tipler

Özel array sözdizimini argümansız 'new' ve '<<' metodlarını destekleyen başka tiplerle de kullanabilirsiniz:

```crystal
MyType{1, 2, 3}
```

Eğer `MyType` <<generic>> değil ise, yukarıdaki şuna eşit olacaktır:

```crystal
tmp = MyType.new
tmp << 1
tmp << 2
tmp << 3
tmp
```

Eğer `MyType` <<generic>> ise, yukarıdaki şuna eşit olacaktır:

```crystal
tmp = MyType(typeof(1, 2, 3)).new
tmp << 1
tmp << 2
tmp << 3
tmp
```

<<Generic>> tip durumunda, tip argümanları da belirtilebilir:

```crystal
MyType(Int32 | String) {1, 2, "foo"}
```
