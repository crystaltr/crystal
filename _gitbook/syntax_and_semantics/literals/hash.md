# Hash

Bir [Hash](http://crystal-lang.org/api/Hash.html) `A` tipindeki anahtarların `D` tipindeki değerler ile eşleştirilmesini gösterir. Genellikle şöyle tanımlanır:

```crystal
{1 => 2, 3 => 4}     # Hash(Int32, Int32)
{1 => 2, 'a' => 3}   # Hash(Int32 | Char, Int32)
```

Bir Hash, hem anahtarlar hem değerler için karışık tipler içerebilir, yani 'A'/'D' tiplerin birleşimi olur ama bunlar hash tanımlandığında ya 'A' ve 'D' tiplerini belirterek ya da bir hash değişmezi kullanılarak belirlenir. Son durumda 'A'  ve 'D' hash'in anahtar ve değerlerinin tiplerinin birrleşimine eşit olurlar.

Boş bir hash tanımlarken 'A' ve 'D'yi belirtmek zorundasınız:

```crystal
{} of Int32 => Int32 # same as Hash(Int32, Int32).new
{}                   # syntax error
```

## Symbol anahtarlar

Özel bir gösterim ile symbol anahtarlı hash'ler tanımlayabilirsiniz:

```crystal
{key1: 'a', key2: 'b'} # Hash(Symbol, Char)
```

## String anahtarlar

Özel bir gösterim ile string anahtarlı hash'ler tanımlayabilirsiniz:

```crystal
{"key1": 'a', "key2": 'b'} # Hash(String, Char)
```

## Hash'e benzeyen tipler

Özel array sözdizimini argümansız 'new' ve '[]=' metodlarını destekleyen başka tiplerle de kullanabilirsiniz:

```crystal
MyType{"foo": "bar"}
```

Eğer `MyType` <<generic>> değil ise, yukarıdaki şuna eşit olacaktır:

```crystal
tmp = MyType.new
tmp["foo"] = "bar"
tmp
```

Eğer `MyType` <<generic>> ise, yukarıdaki şuna eşit olacaktır:

```crystal
tmp = MyType(typeof("foo"), typeof("bar")).new
tmp["foo"] = "bar"
tmp
```

<<Generic>> tip durumunda, tip argümanları da belirtilebilir:

```crystal
MyType(String, String) {"foo": "bar"}
```
