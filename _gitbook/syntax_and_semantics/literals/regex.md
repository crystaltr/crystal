# Regex

Düzenli ifadeler [Regex](http://crystal-lang.org/api/Regex.html) sınıfıyla gösterilir, genellikle de şöyle tanımlanır:

```crystal
foo_or_bar = /foo|bar/
heeello    = /h(e+)llo/
integer    = /\d+/
```

Bir düzenli ifade '/' ile ayrılır ve [PCRE](http://pcre.org/pcre.txt) sözdizimini kullanır.

Bu düzenleyiciler Regex'e eklenebilir:

* i: ignore case (PCRE_CASELESS)
* m: multiline (PCRE_MULTILINE)
* x: extended (PCRE_EXTENDED)

Örneğin

```crystal
r = /foo/imx
```

Bölü işaretleri kaçmak zorunda:

```crystal
slash = /\//
```

Alternatif bir sözdizimi de desteklenir:

```crystal
r = %r(regex with slash: /)
```
