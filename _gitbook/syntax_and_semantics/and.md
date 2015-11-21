# &&

`&&` sağında ve solunda bulunan ifadeleri değerlendirir. Eğer doğru ise sağ tarafı değerlendirir ve onun değerini alır. Aksi takdirde sol tarafı değerlendirir ve onun değerini alır. Tipi sağ ve sol tarafta olabilecek tiplerin toplamıdır olan bir `union`dır.

`&&`i if yerine kullanılan bir syntax sugar olarak düşünebilirsiniz.

```crystal
some_exp1 && some_exp2

# Yukarıda kod ile aynı
tmp = some_exp1
if tmp
  some_exp2
else
  tmp
end
```
