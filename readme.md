## Examples

### How to complile cjpeg.c with static lib?

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
    gcc cdjpeg.o cjpeg.o -o prog -L ../library -l jpeg -O3
    ```
