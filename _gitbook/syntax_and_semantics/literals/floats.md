# Float'lar

2 kayan noktalı tip var, [Float32](http://crystal-lang.org/api/Float32.html) ve [Float64](http://crystal-lang.org/api/Float64.html),
bunlar IEEE tarafından tanımlanmış [binary32](http://en.wikipedia.org/wiki/Single_precision_floating-point_format)
ve [binary64](http://en.wikipedia.org/wiki/Double_precision_floating-point_format) formatlarına karşılık gelir.

Bir float değişmezi: `+` ya da `-` işaretini (opsiyonel), takip eden
bir dizi rakam ya da alttire ve bunları takip eden bir nokta ve arkasına
rakamlar ya da alttireler ve bir son ek ile gösterilebilir.
Eğer son ek yoksa değişmezin tipi 'Float64' olur.

```crystal
1.0      # Float64
1.0_f32  # Float32
1_f32    # Float32

1e10     # Float64
1.5e10   # Float64
1.5e-7   # Float64

+1.3     # Float64
-0.5     # Float64
```

Son ekten önceki alttire '_' isteğe bağlıdır.

Alttireler sayıları daha okunabilir yapmak için kullanılabilir.

```crystal
1_000_000.111_111 # 1000000.111111 'den daha iyi
```
