# Debian ve Ubuntu Üzerine

Debian türevi dağıtımlarda, resmi Crystal deposunu kullanabilirsiniz.

## Depo kurulumu

Oncelikle APT ayarlarınıza depoyu eklemelisiniz. Kolayca kurmak için aşağıdaki satırı çalıştırın:

```
  curl http://dist.crystal-lang.org/apt/setup.sh | sudo bash
```

Bu giriş anahtarını ve depo ayarlarını ekleyecektir. Dilerseniz manuel olarak da çalıştırabilirsiniz

```
apt-key adv --keyserver keys.gnupg.net --recv-keys 09617FD37CC06B54
echo "deb http://dist.crystal-lang.org/apt crystal main" > /etc/apt/sources.list.d/crystal.list
```

## Yükleme
Depo ayarları yapıldığında Crystal'i yüklemeye hazırsınız:

```
sudo apt-get install crystal
```

## Upgrade

Yeni bir Crystal sürümü çıkarıldığında bununla sisteminizi yükseltebilirsiniz:

```
sudo apt-get update
sudo apt-get install crystal
```
