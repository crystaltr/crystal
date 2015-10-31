# String

Bir [String](http://crystal-lang.org/api/String.html) değişmez bir dizi UTF-8 karakterini belirtir.

Bir String, genellikle bir dizi UTF-8 karakterini çevreleyen çift tırnaklarla tanımlanır.

```crystal
"hello world"
```

String içindeki bazı karakterleri belirtmek için ters bölü işareti kullanılabilir:

```crystal
"\"" # double quote
"\\" # backslash
"\e" # escape
"\f" # form feed
"\n" # newline
"\r" # carriage return
"\t" # tab
"\v" # vertical tab
```

Ters bölü işaretini bir code point belirtmek için, en fazla 3 hane kaplayan sekizli sayılarla kullanabilirsiniz:

```crystal
"\101" # == "A"
"\123" # == "S"
"\12"  # == "\n"
"\1"   # string with one character with code point 1
```

Ters bölü işaretini bir  unicode codepoint belirtmek için,  bir *u* ardından 4 onaltılı karakter ile kullanabilirsiniz:

```crystal
"\u0041" # == "A"
```

Ya da süslü parantezleri kullanıp 6 haneli onaltılı sayılara kadar belirtebilirsiniz (0'dan 10FFFF 'ye kadar):

```crystal
"\u{41}"    # == "A"
"\u{1F52E}" # == "🔮"
```

Bir string birden fazla satırı kaplayabilir

```crystal
"hello
      world" # same as "hello\n      world"
```

Yukarıdaki örnekte boşlukların ve yeni satırların sonuçlanan string'te bittiğini dikkate alın.
Bundan kaçınmak içinbir string'i birden fazla satıra ters bölü işaretlerini kullanarak
bölebilirsiniz:

```crystal
"hello " \
"world, " \
"no newlines" # same as "hello world, no newlines"
```

Alternatif olarak ters bölü işaretinin ardından eklenecek bir yeni satır string değişmezine eklenebilir:

```crystal
"hello \
     world, \
     no newlines" # same as "hello world, no newlines"
```

Bu durumda, önde gelen boşluk sonuç string'ine dahil edilmez.

Eğer çift tırnak, parantez ya da buna benzer karakterler içeren bir string yazmak istiyorsanız,
alternatif değişmezleri kullanabilirsiniz:

```crystal
# Çift tırnakları ve içiçe parantezleri destekler
%(hello ("world")) # same as "hello (\"world\")"

# Çift tırnakları ve içiçe köşeli parantezleri destekler
%[hello ["world"]] # same as "hello [\"world\"]"

# Çift tırnakları ve içiçe süslü parantezleri destekler
%{hello {"world"}} # same as "hello {\"world\"}"

# Çift tırnakları ve içiçe '<>' işaretlerini destekler
%<hello <"world">> # same as "hello <\"world\">"
```

## Interpolasyon

Gömülü içerikler ile bir String yaratmak için string interpolasyonunu kullanabilirsiniz:

```crystal
a = 1
b = 2
"sum = #{a + b}"        # "sum = 3"
```

Bu `#{...}` ile çevrelenen her içerik için `Object#to_s(IO)`çağırarak sonlanır.
