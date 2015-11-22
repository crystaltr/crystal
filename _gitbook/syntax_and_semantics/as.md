# as

`as` bir ifadenin tiplerini sınırlar. Örnek olarak:

```crystal
if some_condition
  a = 1
else
  a = "hello"
end

# a :: Int32 | String
```

Yukarıdaki örnekte, `a` bir `Int32 | String` `union`idi. Eğer herhangi bir sebepten `a`nın `if`den sonra `Int32` olduğunu biliyorsak, derleyiciye buna göre davranmasını söyleyebiliriz:

```crystal
a_as_int = a as Int32
a_as_int.abs # Çalışır, derleyici a_as_int in Int32 tipinde olduğunu biliyor.
```

`as` ifadesi bir runtime check yapar: eğer `a` `Int32` değilse bir [exception](exception_handling.html) fırlatılır.

`as` ifadesinin argümanı bir [type](type_grammar.html) olmak zorundadır.

Bir tip başka bir tip tarafından sınırlandırılması mümkün değilse, bir compile-time hatası oluşur.

```crystal
1 as String # Hata
```

**Not:** `as` ifadesini bir tipi ilgisi olmayan başka bir tipe çevirmek için kullanamazsınız: `as` başka dillerdeki `cast` ile aynı değildir. Integer, Float ve Char üzerindeki metodlar çevirme işleminde rahatlık sağlaması için sağlanmıştır. Başka bir seçenek ise, aşağıdaki gibi pointer type arasında çevirme yapmaktır.

## Pointer Tipleri arasında çevirme

Ayrıca `as` ifadesi bize pointer tipleri arasında çevirme imkanı sağlar:

```crystal
ptr = Pointer(Int32).malloc(1)
ptr as Int8* #:: Pointer(Int8)
```

Bu durumda herhangi bir runtime check yapılmaz. Pointer'lar unsafe'dir ve bu tarz bir çevirme sadece C binding yazarken ya da düşük-seviye kod için gereklidir.

## Pointer Tipleri ve Referans Tipler arasında çevirme

Pointer tipleri ve refarans tipleri arasında çevirme yapılabilir.

```crystal
array = [1, 2, 3]

# object_id objenin bellekteki adresini döner,
# bizde bu adresle bellekte bir pointer oluştururuz.
ptr = Pointer(Void).new(array.object_id)

# Oluşturuduğumuz pointer'ı aynı tipe kastediyoruz.
# Bu şekilde aynı değeri almalıyız.
array2 = ptr as Array(Int32)
array2.same?(array) #=> true
```

Bu durumlarda hiç bir runtime check yapılmaz çünkü işin içinde
pointer'lar bulunmaktadır. Bu durum bir önceki örnekten daha
nadir olsa da çeşitli temel tiplerin(Crystal standart kütüphanesinde bulunan String gibi) implemente edilmesine imkan tanır. Ayrıca referans tiplerin void pointer'a çevirilirek C fonksiyonlarına argümant olarak paslanmasına da imkan sağlar.

## Daha büyük bir tipe çevirme

`as` ifadesi bir ifadeyi daha büyük bir tipe çevirmek için kullanılabilir. Örnek olarak:

```crystal
a = 1
b = a as Int32 | Float64
b #:: Int32 | Float64
```

Yukarıdaki örnek pek kullanlışlı olmayabilir, fakat aşağıdaki örnekteki gibi bir dizi elemanları üzerinde map işlemi uygularken:

```crystal
ary = [1, 2, 3]

# İçinde 1,2,3 olan Int32 | Float64 olan bir array oluşturmak istiyoruz.
ary2 = ary.map { |x| x as Int32 | Float64 }

ary2 #:: Array(Int32 | Float64)
ary2 << 1.5 # OK
```

`Array#map` metodu bloğun tipini kullanarak diziyi oluşturur.
 `as` ifadesi olmasaydı, derleyici tipi `Int32` olarak anlamlandırırdı ve bizde diziye bir `Float64` değer ekleyemezdik.

## Derleyici bir block'un tipini anlamlandıramadığında

Bazen derleyici bir block'un tipini anlamlandıramayabilir. Örnek olarak:

```crystal
class Person
  def initialize(@name)
  end

  def name
    @name
  end
end

a = [] of Person
x = a.map { |f| f.name } # Error: can't infer block return type
```

Derleyici `Array#map` ile jenerik diziyi oluştururken block'un tipini bilmesi gerekiyor. Fakat `Person` sınıfından daha önce bir obje oluşturulmadığı için derleyici `@name`'in tipini bilemez. Bu tarz durumlarda `as` ifadesi kullanarak derleyiciye ilgili tipi söyleyebilirsiniz.

```crystal
a = [] of Person
x = a.map { |f| f.name as String } # OK
```

Bu hata çok yaygın değildir, ve `Array#map` işleminden önce `Person` sınfından bir nesne oluşturulursa ortadan kalkar:

```crystal
Person.new "Serdar"

a = [] of Person
x = a.map { |f| f.name as String } # OK
```
