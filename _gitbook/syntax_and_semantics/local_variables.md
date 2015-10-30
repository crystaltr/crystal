# Local değişkenler

Local değişkenler küçük harflerle başlar. Siz ilk kez bir değere atadığınız zaman onlar deklare edilir.

```crystal
name = "Crystal"
age = 1
```

Onların tipleri sadece ilklenirken değil, kullanıldığında da belirlenir. Genel olarak, sadece programcının programın kullanımı ve değişkenlerin konumlarına göre beklediği değerler ile ilişkili tipleri vardır.

Örneğin, bir değişkene farklı bir ifade ile tekrar atama yapıldığında o ifadenin tipine sahip olur.

```crystal
flower = "Tulip"
# At this point 'flower' is a String

flower = 1
# At this point 'flower' is an Int32
```

Değişken isimlerinin alttire ile başlamasına izin verilir, ama bu isimler derleyici tarafından rezerve edilir, bu yüzden kullanımı tavsiye edilmez (ve kod okunabilirliğini zorlaştırır).
