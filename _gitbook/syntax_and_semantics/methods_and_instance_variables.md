# Methodlar ve Örnek Değişkenler(Instance Variables)

Initialize methodumuza aldığımız argümanı örnek değişkene atamak için daha kısa yolu kullanarak methodumuzu basitleştirebiliriz:

```crystal
class Insan
  def initialize(@isim)
    @yas = 0
  end
end
```

Şu an, bir insan ile daha fazlasını yapamayız: bir isimle oluşturuyoruz, ismini ve yaşını soruyoruz ve yaşı her zaman 0 geliyor. Öyleyse insanımızı yaşlandıran bir method yazalım:

```crystal
class Insan
  def yaslandir
    @yas += 1
  end
end

osman = Insan.new "Osman"
kemal = Insan.new "Kemal"

osman.yas #=> 0

osman.yaslandir
osman.yas #=> 1

kemal.yas #=> 0
```

Method isimlerinin genel kullanımı; küçük harfle başlar. Alt çizgi ve sayi ile de başlayabilir.

Yan bilgi olarak, `yaslandir` methodunu orjinal `Insan` sınıfı içinde tanımlayabildiğimiz gibi ayrı bir yerde de tanımlayabiliriz:
Crystal tüm tanımlamaları tek bir sınıf içerisinde toplar. Aşağıdaki kod tamamen geçerlidir:

```crystal
class Insan
  def initialize(@isim)
    @yas = 0
  end
end

class Insan
  def yaslandir
    @yas += 1
  end
end
```

## Methodları yeniden tanımlama ve previous_def

Eğer bir methodu tekrar tanımlarsak farklı bir yerde aynı sınıf içerisinde son tanımlanan çağırılır.

```crystal
class Insan
  def yaslandir
    @yas += 1
  end
end

class Insan
  def yaslandir
    @yas += 2
  end
end

insan = Insan.new "Osman"
insan.yaslandir
insan.yas #=> 2
```

`previous_def` ile önce tanımlanmış methodu çağırabilirsiniz:

```crystal
class Insan
  def yaslandir
    @yas += 1
  end
end

class Insan
  def yaslandir
    previous_def
    @yas += 2
  end
end

insan = Insan.new "Osman"
insan.yaslandir
insan.yas #=> 3
```

Argüman ve parantezler olmadan, `previous_def` methodmuş gibi methodun ayni argümanlarını alır. Eğer argüman verilirse onları da alır.
