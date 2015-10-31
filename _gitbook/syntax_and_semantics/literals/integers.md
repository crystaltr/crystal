# Integer'lar

4 işaretli integer tipi var: [Int8](http://crystal-lang.org/api/Int8.html), [Int16](http://crystal-lang.org/api/Int16.html), [Int32](http://crystal-lang.org/api/Int32.html) ve [Int64](http://crystal-lang.org/api/Int64.html), sırasıyla 8, 16, 32 ve 64 bit'i gösterirler.

4 işaretsiz integer tipi var: [UInt8](http://crystal-lang.org/api/UInt8.html), [UInt16](http://crystal-lang.org/api/UInt16.html), [UInt32](http://crystal-lang.org/api/UInt32.html) ve [UInt64](http://crystal-lang.org/api/UInt64.html).

Bir integer '+' ya da '-' işaretini (opsiyonel), takip eden bir dizi rakam ve alttirelere
eklenen bir son ek ile (opsiyonel) gösterilir.
Eğer son ek yoksa, değişmezin tipi 'Int32', 'Int64' ve 'UInt64' tiplerinden,
sayının uyduğu en düşük tip olarak belirlenir.

```crystal
1      # Int32

1_i8   # Int8
1_i16  # Int16
1_i32  # Int32
1_i64  # Int64

1_u8   # UInt8
1_u16  # UInt16
1_u32  # UInt32
1_u64  # UInt64

+10    # Int32
-20    # Int32

2147483648          # Int64
9223372036854775808 # UInt64
```

Son ekten önceki alttire '_' isteğe bağlıdır.

Alttireler sayıları daha okunabilir yapmak için kullanılabilir.

```crystal
1_000_000 # 1000000'den daha iyi
```

İkili sayılar `0b` ile başlar:

```crystal
0b1101 # == 13
```

Sekizli sayılar `0o` ile başlar:

```crystal
0o123 # == 83
```

Onaltılı sayılar `0x` ile başlar:

```crystal
0xFE012D # == 16646445
0xfe012d # == 16646445
```
