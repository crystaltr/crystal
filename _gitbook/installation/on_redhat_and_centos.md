# RedHat ve CentOS Üzerine

RedHat türevi dağıtımlarda, resmi Crystal deposunu kullanabilirsiniz.

## Depo Kurulumu

Ilk olarak YUM ayar dosyanıza Crystal deposunu eklemelisiniz. Kolayca kurmak için aşağıdaki satırı çalıştırın:

```
  curl http://dist.crystal-lang.org/rpm/setup.sh | sudo bash
```

Bu giriş anahtarını ve depo ayarlarını ekleyecektir. Dilerseniz manuel olarak da çalıştırabilirsiniz

```
rpm --import http://dist.crystal-lang.org/rpm/RPM-GPG-KEY

cat > /etc/yum.repos.d/crystal.repo <<END
[crystal]
name = Crystal
baseurl = http://dist.crystal-lang.org/rpm/
END
```

## Yükleme
Depo ayarları yapıldığında Crystal'i yüklemeye hazırsınız:

```
sudo yum install crystal
```

## Yükseltme

Yeni bir Crystal sürümü çıkarıldığında bununla sisteminizi yükseltebilirsiniz:
```
sudo yum update crystal
```
