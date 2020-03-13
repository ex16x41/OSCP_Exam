# Compiling C/C++ code

## compiling c code in linux for windows environment

Installing the cross-compilation

```text
sudo apt-get install mingw-w64
```

32bit

```text
i686-w64-mingw32-gcc -o test.exe test.c
```

64bit

```text
x86_64-w64-mingw32-gcc -o test.exe test.c
```

ref : [https://stackoverflow.com/questions/44670209/how-to-compile-c-code-in-linux-to-run-on-windows](https://stackoverflow.com/questions/44670209/how-to-compile-c-code-in-linux-to-run-on-windows)

## compiling c code in linux for linux environment

* `gcc test.c -o exec_run`

![](../.gitbook/assets/image.png)

### compiling a c code in 32bit linux

* gcc test.c -m32 -o exec\_run

