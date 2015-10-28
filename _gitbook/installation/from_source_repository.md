# Kaynak Kod Üzerinden

Eğer Crystal'e katkıda bulunmak istiyorsanız Crystal'i kaynak üzerinden kurmak isteyebilirsiniz.
 Ama Crystal, Crystal'in kendisiyle yazılmıştır. Bu nedenle öncelikle çalışan bir derleyiciye sahip olmak için daha önce bahsedelen yöntemlerden birini kullanmaya ihtiyacanız var.  
Ayrıca LLVM 3.5 ya da 3.6'ya path içerisinde ihtiyacınız olacak. Eğer Mac ve HomeBrew yöntemini kullanıyorsanız ve Crystal'i `--with-llvm` ile kurduysanız,
 otomatik olarak path ayarını sizin için yapacaktır.

Daha sonra depoyu makinenize klonlayın:

```
git clone https://github.com/manastech/crystal.git
```

ve kodlamaya başlamak için hazırsın.

Kendi derleyici versiyonunuzu yaratmak için, terminalden `make`'i çalıştırın. Yeni derleyici `.build/crystal` altında konumlandırılacaktır.

[Tüm gerekli kütüphanlerin(https://github.com/manastech/crystal/wiki/All-required-libraries) yüklü olduğundan emin olun. Ayrıca [destekleme rehberini](https://github.com/manastech/crystal/blob/master/Contributing.md) okumak isteyebilirsiniz.

Deponun içerisinde `bin/crystal` altında bir betik bulacaksınız. Bu betik global yüklenmiş derleyiciyi ya da eğer varsa henüz derlediğiniz dosyayı çalıştıracaktır.