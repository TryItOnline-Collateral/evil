# [The ``evil`` Programming Language Homepage](https://web.archive.org/web/20070103000858/www1.pacific.edu/~twrensch/evil/index.html)

**The materials in this repository were not produced by the owner of the repository. Please click on the link in the header to go to the original web site these materials were copied from. The purpose of this copy is to automate setup of a mirror for https://tryitonline.net. It's more straight forward to clone a repository than to parse a web page.**

`evil` is a programming language with a simple execution model and an even simpler syntax. The cost for this is that writing programs is quite painful. A good language for masocistic computer scientists.

Commands in `evil` are single lowercase letters. Uppercase letters are reserved for standard library commands (still in process). All other characters are ignored.

This model means that any text file is a legal `evil` program. It also means that program documentation is a real challange.

In fact, it is program documentation that really separates the true `evil` programmer from novices. A novice will either write documentation in a separate file or include no documentation at all. A true `evil` programmer will write documentaiton using digit values encoding ascii values (usually in octal). The true master of `evil` will write the program and the documentation in such a way that the documentation IS the program.

Hello World!

Here is the usual "Hello World!" program in `evil`. Note that this version is highly unoptimized, as it simply uses the commands that directly effect the A register to create the proper character values and write them out.

```Evil
    zaeeeaeeew
    zaeeaeeaeaw
    zaeaeeaeeaew
    zaeaeeaeeaew
    zuueeueew
    zaeeeeew
    zuueueueeeew
    zuueeueew
    zaeeaeeaeaeew
    zaeaeeaeeaew
    zaeeaeeaew
    zaeeeeeaw
    zaeeeeeaeawuuuw
```

A somewhat better Hello World! program can be found here: [hello.txt](hello.txt). This version is the shortest possible Hello World! program in `evil` that uses only the a, u, e, z, and (of course) the w commands. These commands effect only the A register, so these programs have no effect on the pental or wheel. Another program along the same line can be found in [pure.txt](pure.txt).
