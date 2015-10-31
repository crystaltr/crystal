# Örnek değişken(Instance variables) tip çıkarımı

Önceki örneklerde `Insan` sınıfının `isim` ve `yas` değişkenlerini tanımlarken hiç tiplerinden bahsetmediğimizi farkettiniz mi? Bunun sebebi derleyicinin bizim yerimize bunu yapmasıdır.

Yazdığımızda:

```crystal
class Insan
  getter isim

  def initialize(@isim)
    @yas = 0
  end
end

osman = Insan.new "Osman"
osman.isim #=> "Osman"
osman.isim.size #=> 4
```

`String` bir argumanla `Insan.new`'i çağırdığımızda, derleyici `@isim` değişkenini de `String` yapar.
`Insan.new`'i farklı bir tiple çağırmış olsaydık, `@isim` değişkeni farklı bir tip alacaktı:

```crystal
bir = Insan.new 1
bir.isim #=> 1
bir.isim + 2 #=> 3
```

Önceki programları `tool hierarchy` komutu ile derleseydik, derleyici bize tip çıkarımlarıyla birlikte bir hiyerarşi grafiği gösterecekti. İlk durumda:

```
- class Object
  |
  +- class Reference
     |
     +- class Insan
            @isim : String
            @yas  : Int32
```

İkinci durumda:

```
- class Object
  |
  +- class Reference
     |
     +- class Insan
            @isim : Int32
            @yas  : Int32
```

Birisini `String`, diğerini `Int32` ile 2 farklı insan oluştursaydık ne olacaktı? Deneyelim:

```crystal
osman = Insan.new "Osman"
bir = Insan.new 1
```

`tool hierarchy` komutu ile derleyiciyi çalıştırınca şunu alırız:
```
- class Object
  |
  +- class Reference
     |
     +- class Insan
            @isim : (String | Int32)
            @yas  : Int32
```

Şimdi görebiliriz ki `@isim`'in tipi `(String | Int32)`, *union* olarak okunan `String` ve `Int32` birleşimidir. Derleyici bu tiplerin tümünün atandığı `@isim` 'i üretti.

Bu durumda, derleyici `@isim` değişkenini her kullanımda `String` ya da `Int32` olduğunu varsayacaktır. Eğer `@isim` değişkeni üzerinden çağırılan bir method, verilen *tüm* tiplerde(burada String ve Int32) tanımlı değilse derleme esnasında hata(compile time error) verecektir.


```crystal
osman = Insan.new "osman"
bir = Insan.new 1

# Error: undefined method 'size' for Int32
osman.isim.size

# Error: no overload matches 'String#+' with types Int32
osman.isim + 3
```

İlk kullanımında değişkenin bir tipinin olduğunu varsayıp sonra o tipi değiştirseniz de derleyici hata verecektir.

```crystal
osman = Insan.new "osman"
osman.isim.size
bir = Insan.new 1
```

Bu, compile-time hatası verir:

```
Error in foo.cr:14: instantiating 'Insan:Class#new(Int32)'

bir = Insan.new 1
             ^~~

instantiating 'Insan#initialize(Int32)'

in foo.cr:12: undefined method 'size' for Int32

osman.isim.size
          ^~~~~~
```

Derleyici global tip çıkarımı yapar ve ne zaman bir sınıf ya da methodu yanlış kullanırsanız size söyler. Devam edebilir ve şu şekilde `def initialize(@isim : String)` bir tip kısıtlaması koyabilirsiniz ama bu yazılan kodu biraz gereksizleştirir ve jenerikliğini azaltır: eğer `Insan` instance'ını `String` ile oluşturursanız, `String` *interface* 'iyle aynı şeye sahip olursunuz, `Insan`'ın isim değişkenini `String` varmış gibi kullanabilirsiniz, bu şekilde idare eder bir kod yazmış olursunuz.

`@isim` değişkenlerinden birisi `Int32` bir diğeri `String` olan 2 farklı `Insan` tipine ihtiyacınız varsa [generics](generics.html)'leri kullanmalısınız.

## Nil olabilen örnek değişkenler(Nilable)

`initialize` tanımlı bir sınıf içerisindeyken atanma yapılmamış bir instance değişkenin tipi derleyici tarafından `Nil` olarak varsayılacaktır. Bir instance değişkeniniz varsa ona bir başlangıç değeri atayın:


```crystal
class Insan
  getter isim

  def initialize(@isim)
    @yas = 0
  end

  def address
    @address
  end

  def address=(@address)
  end
end

osman = Insan.new "osman"
osman.address = "Argentina"
```

Şimdi hiyerarşi grafiği şöyle gözükür:

```
- class Object
  |
  +- class Reference
     |
     +- class Insan
            @isim : String
            @yas : Int32
            @address : String?
```

`@address` : `String?` ifadesinde `String | Nil` gösteriminin kısaltılmış halini görebilirsiniz. Bunun anlamı aşağıdaki gibi bir compile time hatası alacağımızdır:

```crystal
# Error: undefined method 'size' for Nil
osman.address.size
```

`Nil` ve genel olarak union(birleşik) tiplerle başa çıkmak için, bir kaç yöntem vardır: [if var](if_var.html), [if var.is_a?](if_varis_a.html), [case](case.html) ve [is_a?](is_a.html).

## Catch-all initialization

Örnek değişkenler ayrıca `initialize` method dışarısında da initialize edilebilirler(başlatılabilirler):

```crystal
class Insan
  @yas = 0

  def initialize(@isim)
  end
end
```

Her yeni örnek oluşturulduğunda `@yas` sıfıra atanmış olarak gelecektir. Bu kod tekrarından, bir sınıfı tekrar açıp ve bir instance değişken eklediğinizde `Nil` tipinden kaçınmak için kullanışlı olacaktır.

## Instance değişkenlerin tipini belirleme

Belli durumlarda derleyiciye instance değişkenin tipini düzeltmesini söylemek isteyebilirsiniz. Bunu `::` ile yapabilirsiniz:

```crystal
class Insan
  @yas :: Int32

  def initialize(@isim)
    @yas = 0
  end
end
```

Bu örnekte, eğer `@yas` değişkenine `Int32` dışında bir tipte atama yaparsak, atamanın yapıldığı yerde compile-time hatası alacağız.

Hala bir instance değişkeni initialize etmek zorundayız. Ya catch-all initializer ile ya da `initialize` method içerisinde: tipler için "varsayılan"(default) değerler yok.
