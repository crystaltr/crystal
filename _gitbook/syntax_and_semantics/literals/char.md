# Char

Bir [Char](http://crystal-lang.org/api/Char.html), bir [Unicode](http://en.wikipedia.org/wiki/Unicode) [code point](http://en.wikipedia.org/wiki/Code_point)'ine karşılık gelir.
32 bitlik yer kaplar.

Bir UTF-8 karakterini tek tırnakla çevreleyebilmek için yaratıldı.

```crystal
'a'
'z'
'0'
'_'
'あ'
```

Bazı karakterleri belirtmek içi ters bölü işareti kullanabilirsiniz:

```crystal
'\'' # single quote
'\\' # backslash
'\e' # escape
'\f' # form feed
'\n' # newline
'\r' # carriage return
'\t' # tab
'\v' # vertical tab
```

Ters bölü işaretini bir code point belirtmek için, en fazla 3 hane kaplayan sekizli sayılarla kullanabilirsiniz:

```crystal
'\101' # == 'A'
'\123' # == 'S'
'\12'  # == '\n'
'\1'   # code point 1
```

Ters bölü işaretini bir  unicode codepoint belirtmek için,  bir *u* ardından 4 onaltılı karakter ile kullanabilirsiniz:

```crystal
'\u0041' # == 'A'
```

Ya da süslü parantezleri kullanıp 6 haneli onaltılı sayılara kadar belirtebilirsiniz (0'dan 10FFFF 'ye kadar):

```crystal
'\u{41}'    # == 'A'
'\u{1F52E}' # == '🔮'
```
