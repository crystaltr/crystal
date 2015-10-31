# Dönüş Tipleri(Return types)

A method's return type is always inferred by the compiler. However, you might want to specify it for two reasons:
Bir methodun dönüş tipi daima derleyici tarafından çıkarılır. Ancak, belki iki sebepten dolayı siz isteyebilirsiniz:

1. Methodun döndüğü tipin sizin istediğiniz olmasından emin olmak için
2. Belgeleme yorumlarında görünür kılmak için

Örneğin:

```crystal
def methodum : String
  "selam"
end
```

Dönüş tipleri [type grammar](type_grammar.html)'de devam etmekte.
