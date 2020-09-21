# JPEG library

## CMake (linux) instructions
1. Run cmake for library
    ```
    # in library folder
    mkdir build
    cd build
    cmake .. -G"Unix Makefiles" -DCMAKE_INSTALL_PREFIX=../../jpeg
    ```
2. Install library
    ```
    # in library/build folder
    make install
    ```
3. Run cmake for our example
    ```
    # in example folder
    mkdir build
    cd build
    # Djpeg_PREFIX should specify the full path to jpeg library
    cmake .. -G"Unix Makefiles" -Djpeg_PREFIX=$(pwd)/../../jpeg
4. Create executables
    ```
    # in example/build folder
    make
    ```

## Make instructions

1. Run `make` in `library` folder. This will create static and dynamic libraries in `library/bin` folder.
2. Run `make` in `example` folder. This will create `cjpeg` and `djpeg` executables in `example/bin` folder.

### Examples of compiling without using make

#### How to complile cjpeg.c with static library?
1. Compile static library
    ```
    # in library folder
    gcc -c *.c -O3
    ar rcs libjpeg.a *.o
    ```
2. Compile `cjpeg.c` and `cdjpeg.c`
    ```
    # in example folder
    gcc -c cjpeg.c cdjpeg.c -I ../library -O3
    ```
3. Create executable
    ```
    # in example folder
    gcc cdjpeg.o cjpeg.o -o cjpeg_stat -L ../library -l jpeg -O3
    ```

#### How to compile cjpeg.c with dynamic library?
1. Compile dynamic library
    ```
    # in library folder
    gcc -c *.c -O3 -fPIC
    gcc -shared *.o -O3 -fPIC -o libjpeg.so
    ```
2. Compile `cjpeg.c` and `cdjpeg.c`
    ```
    # in example folder
    gcc -c cjpeg.c cdjpeg.c -I ../library -O3
    ```
3. Create executables
    ```
    # in example folder
    gcc cdjpeg.o cjpeg.o -o cjpeg_dyn -L ../library -l jpeg -O3 -Wl,-rpath,\$ORIGIN/../library
    ```

##### Remarks:
- In these examples `bin` and `obj` folders aren't used
- Replace `cjpeg.c` with `djpeg.c` everywhere if you want to compile `djpeg.c`
