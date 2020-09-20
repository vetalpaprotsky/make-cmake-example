## Compiling using command line examples

### How to complile cjpeg.c with static library?

1. Compile static library
    ```
    # in library folder
    gcc -c *.c -O3
    ar rcs libjpeg.a *.o
    ```
2. Compile cjpeg.c and cdjpeg.c
    ```
    # in example folder
    gcc -c cjpeg.c cdjpeg.c -I ../library -O3
    ```
3. Create executable
    ```
    # in example folder
    gcc cdjpeg.o cjpeg.o -o prog_stat -L ../library -l jpeg -O3
    ```

### How to compile cjpeg.c with dynamic library?

1. Compile dynamic library
    ```
    # in library folder
    gcc -c *.c -O3 -fPIC
    gcc -shared *.o -O3 -fPIC -o libjpeg.so
    ```
2. Compile cjpeg.c and cdjpeg.c
    ```
    # in example folder
    gcc -c cjpeg.c cdjpeg.c -I ../library -O3
    ```
3. Create executable
    ```
    # in example folder
    gcc cdjpeg.o cjpeg.o -o prog_dyn -L ../library -l jpeg -O3 -Wl,-rpath,\$ORIGIN/../library
    ```

#### Remarks:
- In these examples bin and obj folders aren't used
- Replace cjpeg.c with djpeg.c everywhere if you want to compile djpeg.c
