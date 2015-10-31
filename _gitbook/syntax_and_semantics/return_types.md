# Dönüş Tipleri(Return types)

Bir methodun dönüş tipi daima derleyici tarafından çıkarılır. Ancak, belki iki sebepten dolayı bunu siz belirtmek isteyebilirsiniz:

1. Methodun döndüğü tipin sizin istediğiniz olmasından emin olmak için
2. Belgeleme yorumlarında görünür kılmak için

Örneğin:

```crystal
def methodum : String
  "selam"
end
```

Dönüş tipleri [type grammar](type_grammar.html)'de devam etmekte.
