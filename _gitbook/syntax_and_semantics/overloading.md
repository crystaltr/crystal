# Overloading(Aşırı yükleme)

`yaslandir` methodunu kaç sene yaşlandıracağını belirten bir sayı alacak şekilde genişletebiliriz:

```crystal
class Insan
  def yaslandir
    @yas += 1
  end

  def yaslandir(sene)
    @yas += sene
  end
end

osman = Insan.new "osman"
osman.yas #=> 0

osman.yaslandir
osman.yas #=> 1

osman.yaslandir 5
osman.yas #=> 6
```

Bunun anlamı, farklı sayıda argüman alan, farklı işlevleri olan methodları aynı isimde tanımlayabiliriz ve derleyici(compiler) bunlara farklı methodlar olarak davranır. Bu işleme *method overloading* denir.

*method overloading* işleminin belirli kriterleri vardır:

* Argüman sayıları
* Argümanlara tip kısıtlaması uygulanmalı
* Bir method ya [blok](blocks_and_procs.html) alır ya da almaz

Örneğin, 4 tane `yaslandir` methodu tanımlayabiliriz:

```crystal
class Insan
  # yasi 1er 1er arttırır
  def yaslandir
    @yas += 1
  end

  # Verilen seneye göre yaşı arttırır
  def yaslandir(sene : Int32)
    @yas += sene
  end

  # String olarak verilen seneye göre yaşı arttırır
  def yaslandir(sene : String)
    @yas += sene.to_i
  end

  # Kişinin mevcut yaşını yield eder(blok içerisinden erişime açar) ve
  # bloktan dönen değer ile arttırır
  def yaslandir
    @age += yield @age
  end
end

insan = Insan.new "Osman"

insan.yaslandir
insan.yas #=> 1

insan.yaslandir 5
insan.yas #=> 6

insan.yaslandir "12"
insan.yas #=> 18

insan.yaslandir do |mevcut_yas|
  mevcut_yas < 20 ? 10 : 30
end
insan.yas #=> 28
```

Yield içeren methoda dikkat edersek, derleyici bunu anladı çünkü `yield` ifadesi kullandık. Bunu daha açıklayıcı yapmak için, methoda argüman olarak sahte(dummy) bir `&block` ekleyebiliriz.

```crystal
class Insan
  def yaslandir(&block)
    @yas += yield @yas
  end
end
```

Üretilen belgelemede dummy `&block` methodu daima görünür olacaktır, siz onu yazsanız da yazmasanız da.

Eşit sayıda argüman verildiğinde, derleyici sıralama yapmaya çalışırken daha az kısıtlanmış olan methodu en sona bırakır:

```crystal
class Insan
  # İlk olarak, bu method tanımlandı
  def yaslandir(yas)
    @yas += yas
  end

  #Overload eşleştirirme dikkate alınırken derleyici bu methodu bir
  #öncekine göre daha önceye koyacaktır çünkü
  #"String" daha kısıtlayıcı, üstteki kısıtlayıcı olmayan methoda göre
  def yaslandir(yas : String)
    @yas += yas.to_i
  end
end

insan = Insan.new "osman"

# İlk tanımlanan çağırılır
insan.yaslandir 20

# İkinci tanımlanan çağırılır
insan.yaslandir "12"
```

Bununla birlikte, derleyici her zaman sıralamayı çıkaramaz çünkü her zaman bütün bir sıralama yoktur, bu yüzden az kısıtlayıcı(less restrictive) methodları sona koymak daima daha iyidir.
