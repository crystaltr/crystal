# Proc

Bir [Proc](http://crystal-lang.org/api/Proc.html) bir fonksiyon işaretçisine (ve opsiyonel içeriğine (kaspam verisi)) karşılık gelir. Genellikle şöyle tanımlanır:

```crystal
# Argümansız bir proc
->{ 1 } # Proc(Int32)

# Tek argümanlı proc
->(x : Int32) { x.to_s } # Proc(Int32, String)

# İki argümanlı proc:
->(x : Int32, y : Int32) { x + y } # Proc(Int32, Int32, Int32)
```

Bir proc değişmezini C bağlayıcılarında direk olarak 'fun' kütüphanesine göndermedikçe, argüman tipleri zorunludur.

Dönüş değeri Proc'un  gövdesinden türer.

Özel `new` metodu da desteklenir:

```crystal
Proc(Int32, String).new { |x| x.to_s } # Proc(Int32, String)
```

Bu biçim size dönüş tipini belirleme ve Proc'un gövdesiyle kontrol etme imkanı veriyor.

## Çağırmak

Bir Proc'u çağırmak için, üzerinde `call` metodunu çağırın. Argüman sayısı Proc'un tipiyle eşleşmeli:

```crystal
proc = ->(x : Int32, y : Int32) { x + y }
proc.call(1, 2) #=> 3
```

## Metodlardan

Bir Proc halihazırda var olan başka bir metodtan yaratılabilir:

```crystal
def one
  1
end

proc = ->one
proc.call #=> 1
```

Eğer metodun argümanları varsa, tiplerini belirtmelisiniz:

```crystal
def plus_one(x)
  x + 1
end

proc = ->plus_one(Int32)
proc.call(41) #=> 42
```

Bir Proc isteğe bağlı olarak bir alıcı belirleyenilir:

```crystal
str = "hello"
proc = ->str.count(Char)
proc.call('e') #=> 1
proc.call('l') #=> 2
```
