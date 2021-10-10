# xor-analyze/README

XOR Cipher implementation and breaking

By Thomas Habets <[thomas@habets.pp.se](thomas@habets.pp.se)>
Written around 2000-2002

## Introduction

Every amateur cryptographer (that I've met) has at one point implemented some version of XOR encryption. Some thinking that it's completely secure, others did it just for fun. The truth is, of course, that it's pathetically insecure.

It's been many years since I first implemented XOR encryption, and then it was just with an 8-bit key. Here's a variable key-length implementation and a program for breaking using a ciphertext-only attack (known/chosen plaintext/ciphertext is so trivial I broke them when I first implemented the 8-bit version when I was eight years old).

This program was inspired by the excellent book ['Applied cryptography' by Bruce Schneier](https://www.goodreads.com/book/show/351301.Applied_Cryptography). ISBN 0-471-11709-9 or 0-471-12845-7. Buy it, read it. Love it.

Although XOR 'encryption' is trivially broken I have never seen a program for automatically breaking it, so I made one myself.

## Algorithms

To find out what length the password is the ciphertext is XOR-ed against itself with different shifts (see `XOR_analyze::coincidence()` in `analyze.cc`) and the number of zeroes (equal bytes) are counted. This is called counting coincidences. When the number of zeroes is high the shift value is potentially a multiple of the key length. The one that stands out most is checked with statistics (with a frequency table) to get the key. To check with statistics on all key-lengths in key-length interval (-m and -M) use the -a switch (with -v for one key per keylength).

## Compiling

Type `make`. Mail me if it doesn't compile with error messages and don't forget to tell me what kind of system you have.

Type `make win32` to cross compile. It works on my box, but probably not on yours. Edit the makefile adjust compiler and compiler options.

## Encryption

`./xor-enc <key> <infile> <outfile>`

Where:

```text
key      = the password
file.txt = input plaintext filename
file.xor = output 'ciphertext' filename
```

## Decryption

`/xor-dec <key> <infile> <outfile>`

Where:

```text
key      = the password
file.xor = input 'ciphertext' filename
file.txt = output plaintext filename
```

## Cryptanalyzing (cracking/breaking)

`./xor-analyze -h` will give you some help.

All tests will work (are successfully cryptanalyzed) without any parameters except ciphertext and frequency table.

### Frequency table generation

The frequency table generator is in `tests/freq-gen.c.xor`. You need to crack the file to get it. Use the frequency table already generated from my patched Linux source in `freq/linux-2.2.14-int-m0.freq`.

To compile the frequency table generator, run `gcc freq-gen.c -o freq-gen`.

To generate `freq/linux-2.2.14-int-m0.freq` I used:

`find /usr/src/linux -name "*.[ch]" | ./freq-gen > freq/linux-2.2.14-int-m0.freq`

Note that this does *not* represent average C-code.

## FAQ

Q: The windows version doesn't work/needs file X/crashes the system.

A: Here's a nickel kid, go buy yourself a *real* OS. If the windows version doesn't work, I won't be able to debug it myself. The windows version is created under Linux using a cross-compiler. And since I don't have windows, it's enough for me if it just compiles. I don't cate about the windows version.

As someone once said: I can code the unix stuff for free, but if you want me to program in windows, you have to pay me.

Q: Where can I find a compiled version (as in: "I run windows and can't code")

A: [http://www.habets.pp.se/synscan/files/xor-analyze-*-BINARY.tar.gz](http://www.habets.pp.se/synscan/files/xor-analyze-*-BINARY.tar.gz)

Q: I can't seem to crack this file, I'm sending it to you as an attachment. Will you take a look at it?

A: Probably not. If you can't crack it with this program, it probably means that I would have to spend quite a while trying. And unless you can give me a sufficient reason to do so (like money or a favor or something) I don't really feel like doing other peoples work.

And even if you offer money, I won't hessitate to report you to the proper authorities if I suspect you are trying to get me involved in stolen or otherwise dubious data.

## Misc

I developed this program until it worked, and no longer. Looking at the code now I think it should be rewritten, and maybe I'll do that some day.

If you send a patch that adds/fixes something, it'll probably be added, but suggestions and requests will most likely not be implemented (by me) before the rewrite.

Maybe I'll do the rewrite during the summer of 2002. But then again, maybe not.

## License

It's all GPL, see the LICENSE file.

## Contact

Send questions/suggestions/patches/rants/money/sparc64s to [thomas@habets.pp.se](thomas@habets.pp.se)
