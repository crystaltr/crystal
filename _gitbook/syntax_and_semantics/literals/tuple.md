# Tuple

Bir [Tuple](http://crystal-lang.org/api/Tuple.html) genellikle şöyle tanımlanır:

```crystal
tuple = {1, "hello", 'x'} # Tuple(Int32, String, Char)
tuple[0]                  #=> 1       (Int32)
tuple[1]                  #=> "hello" (String)
tuple[2]                  #=> 'x'     (Char)
```

Boş bir tuple oluşturmak için [Tuple.new](http://crystal-lang.org/api/Tuple.html#new%28%2Aargs%29-class-method)'i kullanın.
