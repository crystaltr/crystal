# HTTP Sunucusu

Biraz daha ilgi çekici bir örnekse bir HTTP sunucusu:

```crystal
require "http/server"

server = HTTP::Server.new(8080) do |request|
  HTTP::Response.ok "text/plain", "Hello world! The time is #{Time.now}"
end

puts "Listening on http://0.0.0.0:8080"
server.listen
```

Yukarıdaki kod dokümantasyonun hepsini okuduğunuzda anlam kazanacaktır ama yine de buradan bir şeyler öğrenebiliriz.

* Başka dosyalarda tanımlanmış kodları [require](../syntax_and_semantics/requiring_files.html) edebilirsiniz:

    ```ruby
    require "http/server"
    ```
* Tiplerini belirtmeye gerek kalmadan [yerel değişkenler](../syntax_and_semantics/local_variables.html) tanımlayabilirsiniz:

    ```ruby
    server = HTTP::Server.new ...
    ```

* [Metodları](../syntax_and_semantics/classes_and_methods.html) çağırarak (ya da nesnelere mesajlar göndererek) programlayabilirsiniz.

    ```ruby
    HTTP::Server.new(8000) ...
    ...
    Time.now
    ...
    puts "Listening on http://0.0.0.0:8080"
    ...
    server.listen
    ```

* Yeniden kod kullanımı için uygun bir yol olan ve fonksiyonel dünyanın birkaç özelliğinden faydalanmamızı sağlayan kod bloklarını ya da sadece [blokları](../syntax_and_semantics/blocks_and_procs.html) kullanabilirsiniz:

    ```ruby
    HTTP::Server.new(8080) do |request|
      ...
    end
    ```

* String interpolasyonu olarak bilinen, gömülü içerikten string üretme işini kolaylıkla yapabilirsiniz. Dil array, hash, range, tuple gibi tipler üretebilmek için başka [söz dizimleriyle](../syntax_and_semantics/literals.html) de geliyor.

    ```ruby
    "Hello world! The time is #{Time.now}"
    ```


