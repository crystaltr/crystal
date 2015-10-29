# Derleyici kullanımı

Derleyiciyi bir kez [kurduktan](../installation/README.md) sonra elinizin altında `crystal` binary'si olacak.

Sonraki bölümlerde komut satırı (`$`) dolar işareti ile gösterilecek.

## Tek seferde derleme ve çalıştırma

Bir dosya ismi ile beraber `crystal` komutunu çağırırsanız tek seferde derleyebilir ve programı çalıştırabilirsiniz.

```
$ crystal some_program.cr
```

Crystal dosyaları `.cr` eki ile biter.

Alternatif olarak `run` komutunu da kullanabilirsiniz.

```
$ crystal run some_program.cr
```

## Çalıştırılabilir bir şey oluştur

Çalıştırılabilir bir şeyler oluşturmak için `build` komutunu kullanabilirsiniz:

```
$ crystal build some_program.cr
```

Bu komut `some_program` adında bir dosya oluşturacak ve bunu şöyle çalıştırabilirsiniz:

```
$ ./some_program
```

**Not:** Varsayılan olarak **tamamen optimize** çalıştırılabilir dosya oluşturmaz. Optimizasyonları yapması için, `--release` flag'ini kullanmalısınız:

```
$ crystal build some_program.cr --release
```

Production için derlerken ve benchmark ölçümleri yaparken her zaman `--release` kullandığınızdan emin olun.

Optimizasyonsuzda oldukça iyi performans sergilemesi ve hızlı derleme süresine sahip olması sebebiyle neredeyse bir yorumlayıcı var gibi `crystal` komutunu kullanabilirsiniz.

## Bir proje veya kütüphane oluşturma

Bir Crystal projesinin standart dizin yapısını oluşturmak için `init` komutunu kullanın.

```
$ crystal init lib MyCoolLib
      create  MyCoolLib/.gitignore
      create  MyCoolLib/LICENSE
      create  MyCoolLib/README.md
      create  MyCoolLib/.travis.yml
      create  MyCoolLib/shard.yml
      create  MyCoolLib/src/MyCoolLib.cr
      create  MyCoolLib/src/MyCoolLib/version.cr
      create  MyCoolLib/spec/spec_helper.cr
      create  MyCoolLib/spec/MyCoolLib_spec.cr
Initialized empty Git repository in ~/MyCoolLib/.git/
```

## Diğer komutlar ve seçenekler

Tüm komut setini görmek için argümansız olarak `crystal` komutunu çağırmalısınız.

```
$ crystal
Usage: crystal [command] [switches] [program file] [--] [arguments]

Command:
    init                     generate new crystal project
    build                    compile program file
    deps                     install project dependencies
    docs                     generate documentation
    eval                     eval code from args or standard input
    run (default)            compile and run program file
    spec                     compile and run specs (in spec directory)
    tool                     run a tool
    --help, -h               show this help
    --version, -v            show version
```

Belirli bir komut için kullanabileceğiniz seçenekleri görmek için, komuttan sonra `--help` yazmanız yeterli:

```
$ crystal build --help
Usage: crystal build [options] [programfile] [--] [arguments]

Options:
    --cross-compile flags            cross-compile
    -d, --debug                      Add symbolic debug info
    -D FLAG, --define FLAG           Define a compile-time flag
    --emit [asm|llvm-bc|llvm-ir|obj] Comma separated list of types of output for the compiler to emit
    -h, --help                       Show this message
    --ll                             Dump ll to .crystal directory
    --link-flags FLAGS               Additional flags to pass to the linker
    --mcpu CPU                       Target specific cpu type
    --no-color                       Disable colored output
    --no-codegen                     Don't do code generation
    -o                               Output filename
    --prelude                        Use given file as prelude
    --release                        Compile in release mode
    -s, --stats                      Enable statistics output
    --single-module                  Generate a single LLVM module
    --threads                        Maximum number of threads to use
    --target TRIPLE                  Target triple
    --verbose                        Display executed commands
```
