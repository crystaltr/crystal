# Özellikler (Attributes)

Bazı tipler ve metodlar özellik ile işaretlenebilir. Şu an için
özellik sayısı sınırlı fakat gelecekte kullanıcı tanımlı özellikler olacak.

## Link

Derleyiciye bir C kütüphanesine nasıl bağlanacağını söyler. Bu [lib](c_bindings/lib.html) sekmesinde detaylı olarak anlatılmıştır.

## ThreadLocal

`@[ThreadLocal]` özelliği global ve sınıf değişkenlerine uygulanabilir. Bunları her thread'e lokal hale getirir.

```crystal
# Her thread için bir adet
@[ThreadLocal]
$values = [] of Int32
```

## Packed

Bir [C struct](c_bindings/struct.html)'ı packed olarak işaretlememizi sağlar. Bu struct'ın hizalamasını bir byte yapar ve alanlar arasında hiç padding olmamasını sağlar. packed olmayan struct'larda alanlar arasındaki padding hedef sisteme göre eklenir.

## AlwaysInline

Derleyiciye her zaman bu metodu inline etmesi gerektiğini söyler.

```crystal
@[AlwaysInline]
def foo
  1
end
```

## NoInline

Derleyiciye hiç bir zaman bu metodu inline etmemesi gerektiğini söyler. Eğer yield eden bir metod ise bu özellik çalışmaz.

```crystal
@[NoInline]
def foo
  1
end
```

## ReturnsTwice

Bir metodu ya da [lib fun](c_bindings/fun.html) iki kere return ediyor olarak belirtir. C `setjmp` buna güzel bir örnektir.

## Raises

Bir metodu ya da [lib fun](c_bindings/fun.html) potansiyel olarak exception fırlatabilir olarak işaretler.[callbacks](c_bindings/callbacks.html) bölümünde detaylı olarak açıklanmıştır.

## CallConvention

[lib fun](c_bindings/fun.html) call convention'ını belirtir. Örnek olarak:

```crystal
lib LibFoo
  @[CallConvention("X86_StdCall")]
  fun foo : Int32
end
```

Geçerli call convention listesi.

* C (varsayılan)
* Fast
* Cold
* WebKit_JS
* AnyReg
* X86_StdCall
* X86_FastCall

Detaylı olarak [burada](http://llvm.org/docs/LangRef.html#calling-conventions) açıklanmıştır.

## Flags

[enum](enum.html)'u "flags enum" olarak işaretler, `to_s` gibi bazı metodların davranışını değiştirir.
