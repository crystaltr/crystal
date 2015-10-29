# RedHat ve CentOS Üzerine

RedHat türevi dağıtımlarda, resmi Crystal deposunu kullanabilirsiniz.

## Depo kurulumu

İlk olarak YUM ayar dosyanıza Crystal deposunu eklemelisiniz. Kolayca kurmak için aşağıdaki komutu çalıştırın:

```
  curl http://dist.crystal-lang.org/rpm/setup.sh | sudo bash
```

Bu giriş anahtarını ve depo ayarlarını ekleyecektir. Dilerseniz manuel olarak da çalıştırabilirsiniz.

```
rpm --import http://dist.crystal-lang.org/rpm/RPM-GPG-KEY

cat > /etc/yum.repos.d/crystal.repo <<END
[crystal]
name = Crystal
baseurl = http://dist.crystal-lang.org/rpm/
END
```

## Kurulum

Depo ayarları yapıldığında Crystal'i kurmaya hazırsınız:

```
sudo yum install crystal
```

## Yükseltme(Upgrade)

Yeni bir Crystal sürümü çıkarıldığında bununla sisteminizi yükseltebilirsiniz:

```
sudo yum update crystal
```
