# C Introduction Notes


## GCC compiler use case example
```bash
gcc -std=c11 -Wall -Werror -Wextra -0 <binary-name> src/hello.c
```

## Check if value is an integer
```c
    // ...
    int x, y, z;
    char term;
    
    if ((scanf("%d %d %d%c", &x, &y, &z, &term) != 4) || (term != '\n')) {
        printf("n/a");
        return -1;
    }
    // ...
```
## Cicles 

- while ...
- do { while ...}
- for (...) {...}
- infinite loop with empty for or wihli 1

## Pointers

There are two type of pointers:
1. _Typed_ — pointer to a memory slot of a particular data type;
2. _Universal_ — pointer to a #void.

In essence pointer is the address (it's just a number) of some variable;


1. Poiner use case:
    ```c
    int main(void) {
        int x = 7;
        int* px = &x; // pointer
        int** ppx = &px;  // pointer to a pointer
        *px = 8; // rewrite the value under this address
                // which means that x is now 8

        int* p = 0;  // common practice to initialize pointer with 0

        int* p = a + 1;
        p[-1] = 8;

        printf("%p\n", p);
        
        return 0
    }
    ```

2. Another example of poiners usage:

    ```c
    #include <stdio.h>

    int main(void) {

        int b;
        int a[3];

        a[1] = 5;
        b = *(a+1);

        printf("%d\n", b);
        *(a + 1) = 6;

        int* p = &b;
        *p = *(a + 1);

        printf("%p\t%d\n", p, b);

        return 0;
    }
    ```

3. Another example from the project's read
    ```c
    void main() {
        int a = 2;      // a == 2
        int b = 4;      // b == 4
        int *p = 0;     // p == 0
        p = &a;         // p == адрес переменной a
        *p = 3;         // a == 3... или нет?
        p++;            // p == адрес переменной b ??!?!?
        (*p)++;         // b == 5 O_o WTF
        *p = *(p - 1);  // b == a == 3 ...
    }
    ```
4. And another one from school21
    ```c
    void main() {
        int a[10];
        a[2] == *(a + 2) == *(2 + a) == 2[a]; //!!!!!!!!!!!!!!!
    }
    ```
 

### Arrays
```c
int main() {
    int a[3]; // define an array

    return 0;
}
```

## Sorting algorithms

Regular sorting algorithms have complexity $O(n^2)$ \
Effective onese aprroach $O(n * \ln n)$

### Bubble sort

```c
#include <stdio.h>

void bubble_sort(int* a, int size);

int main(void) {

    int i = 0;
    // int array[] = {9, 1, 8, 2, 7, 3, 6, 4, 5};
    int array[] = {'F', 'A', 'D', 'B', 'C'};
    int size = sizeof(array) / sizeof(array[0]);

    bubble_sort(array, size);

    for (; i < size; i++) {
        // printf("%d ", array[i]);
        printf("%c ", array[i]);
    }

    return 0;
}


void bubble_sort(int* a, int n) {
    int i, j, temp;

    for (i = 0; i < n - 1; i++) {
        for (j = 0; j < n - i - 1; j++) {
            if (a[j] > a[j+1]) {
                temp = a[j];
                a[j] = a[j+1];
                a[j+1] = temp;
            }
        }
    }
}
```




### stdin/out teminology

Usually standard input is from a keyboard, and standard output is printing out infromation in the terminal window.

# Setup C debugging in VSCode

The only working option I found to run debugging in VS Code with internal terminal is to install extension called CodeLLDB.

Here is my launch.json configuration file:
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "lldb",
            "request": "launch",
            "name": "Launch",
            "program": "${fileDirname}/${fileBasenameNoExtension}",
            "args": [],
            "cwd": "${fileDirname}"
        }

    ]
}
```

# Instructions for running tests

In addition to testing for correct output data, the autotest system will
check your program and its source code for the following points:

* Style tests. To check how much the beauty of your code matches
  for example, you can test your code using the _clang-format_ utility.
  Thematerials/linters folder contains the.clang-format file, which contains
  the necessary settings for the style test. This configuration file extends its action to all files that lie with it in the directory
  or in the directories below. So in order for these settings to apply to your source code files,
  copy.clang-format to thesrc folder. \
  \
  To run the style check, run the following command: \
 clang-format -n src/sourcefile_name.c \
  \
  To download clang-format, enter one of the following commands in the terminal: \
 brew install clang-format \
  or if you have root rights (for Ubuntu / Linux Mint / Debian) \
 
  Required version of clang-format: \
  Mac 14.0.5 \
  Linux 13.0.1


# Test for memory leaks

f**Тест на корректную работу с памятью.** При написании C-программ очень важно следить за утечками памяти. Для этого в Unix-подобных операционных системах довольно часто используют утилиту _valgrind_. Однако, на OS X имеются проблемы с поддержкой valgrind, поэтому вместо нее можно использовать утилиту _leaks_. Вдаваться в механизм работы этих утилит мы сейчас не будем - если интересно, можете почитать в гугле.
  
  **_LEAKS_**

  Чтобы запустить ваш исполняемый файл с помощью этой утилиты, наберите в терминале: \
  ```leaks -atExit -- ./main.out | grep LEAK:```
  
  Обратите внимание на команду ```| grep LEAK:```. Мы используем ее для короткого вывода, чтобы видеть только линии с утечками, если они есть. Если вы хотите увидеть весь вывод, просто удалите эту команду. 

  При запуске исполняемого файла с помощью _leaks_ может появиться сообщение об ошибке:
  >dyld: could not load inserted library ‘/usr/local/lib/libLeaksAtExit.dylib’ because image not found
  
  Ошибка возникает из-за того, что _leaks_ не может найти библиотеку _libLeaksAtExit.dylib_. \
  В этом случае вам необходимо ввести следующие команды:
  ```sh
  cd /usr/local/lib  
  sudo ln -s /Applications/Xcode.app/Contents/Developer/usr/lib/libLeaksAtExit.dylib
  ```

  _Дополнительно:_ \
  Используйте флаг ```-exclude``` утилиты _leaks_ для того, чтобы отфильтровать утечки в функциях, где известно об утечках памяти. Этот флаг позволяет уменьшить количество посторонней информации, сообщаемой _leaks_.

  **_VALGRIND_**
  
  Чтобы установить _valgrind_ на компьютер, введите одну из следующих команд: \
  ```brew install valgrind``` \
  или, если у вас есть root-права (для Ubuntu / Linux Mint / Debian) \
  ```sudo apt install valgrind``` \
  Чтобы запустить ваш исполняемый файл с помощью этой утилиты, наберите в терминале: \
  ```valgrind --tool=memcheck --leak-check=yes  ./main.out```

  Не рекомендуется использовать _valgrind_ на OS X, вместо нее лучше использовать _leaks_.
