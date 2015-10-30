# new, initialize ve allocate

Sınıf örneği(instance) oluşturmak için `new` methodunu sınıf üzerinden çağırırız:

```
insan = Insan.new
```

Burada `insan`, `Insan` sınıfının örneği olmakta.

`insan` örneğiyle daha fazla şey yapamayacağız, bu yüzden `Insan` sınıfına yeni özellikler ekleyelim. Bir `Insan`'ın isim ve yaşı olsun. "Her şey bir nesnedir" bölümünde bir nesnenin etkileşim içerisinde olabilmesinin tek yolunun tipi ve bazı methodları cevaplama özelliklerinin olduğundan bahsetmiştik, öyleyse şu an bizim `isim` ve `yas` methodlarına ihtiyacımız var. Bu bilgileri, örnek değişkenler(instance variables) içerisinde saklayacağız. Örnek değişkenler(instance variables) her zaman *at* (`@`) işareti ile başlar. Ayrıca insan örneğini oluşturduğumuzda yaşının 0 gelmesini, oluştururken de istediğimiz bir ismi vermek istiyor olalım.
Bu kısımları `initialize` adlı Crystal'in içerisinde bulunan özel bir method ile yapacağız. Bu method diğer dillerde *constructor*
ya da yapıcı method olarak bilinmekte. Ancak diğer dillerde oldığı gibi bir sınıf içerisinde birden fazla tanımlanamaz.

```crystal
class Insan
  def initialize(isim)
    @isim = isim
    @yas = 0
  end

  def isim
    @isim
  end

  def yas
    @yas
  end
end
```

Şimdi bir kaç insan örneği oluşturalım:

```crystal
osman = Person.new "Osman"
kemal = Person.new "Kemal"

osman.name #=> "Osman"
osman.age #=> 0

kemal.name #=> "Kemal"
```

Dikkatinizi çekmiştir ki biz new methoduyla nesnemizi oluşturduk ancak sınıf içerisinde böyle bir method tanımlamadık. Aslında sınıf içerisinde bu işlemi yapmak için initialize diye bir method yazdık. Peki new nasıl initialize methodunun yerini aldı?

Cevap, biz `initialize` methodunu tanımladığımızda, Crystal bizim için `new` adında aşağıdaki gibi bir method tanımladı:

```crystal
class Insan
  def self.new(isim)
    instance = Insan.allocate
    instance.initialize(isim)
    instance
  end
 end
```

İlk olarak `self.new` gösterimine dikkat. Bunun anlamı; bu method `Insan` **sınıfına** bağlı, bu sınıfın örneğine(instance) bağlı değil. Yani sınıf methodu(class method). Yani SinifIsmi.self_ile_tanimli_method. Bu şekilde sınıftan bir örnek oluşturmadan methodu sınıf üzerinden çağırabiliyoruz.

İkinci olarak `allocate`; herhangi bir değer atanmamış, verilen tipte(burada verdiğimiz tip, Insan tipinde bir sınıf) nesne oluşturan, alt seviye bir sınıf methodudur(class method). Basitçe, gerekli olan alanı(memory) nesneye tahsis eder, ayır(allocate).
Daha sonra `initialize` oluşturulan nesne üzerinden çağırılıdığında örneğimizi(instance) elde ederiz. Genel olarak asla `allocate` methodunu çağırmayın, [güvenli değildir](unsafe.html).
