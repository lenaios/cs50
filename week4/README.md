# Lecture 4
- Hexadecimal
- Pointers
- string
- Compare and copy
- valgrind
- Swap
- Memory layout
- get_int
- Files
- JPEG

## Hexadecimal
컴퓨터는 데이터를 메모리에 저장한다.  
그리고 메모리의 주소는 16진법을 사용하며, 0x로 시작한다.  

## Pointers
C에서 메모리 주소(데이터가 저장된 메모리의 위치)를 얻고 싶을 때 연산자 `&` 를 붙인다.  
실제 자료형이 아닌 자료형을 저장하고 있는 주소를 변수로 담으려면 `*`를 붙여야 한다.  
```c
int *p = &n;
```

## string
string은 연속된 char의 배열이다.
```c
char *s = "EMMA”;
printf("%p\n", s);
printf("%s\n", s);
printf("%c\n", *s); // *s pointer's actual value
printf("%c\n", *(s+1)); // *s pointer's actual value
```

## Compare and copy
아래 코드는 두 string을 비교하는데, 실제로는 string의 첫 문자가 저장된 주소를 비교한다.  
`s`와 `t`가 같은 문자열이더라도 서로 다른 메모리 위치에 저장되어 있으므로 항상 Different를 출력한다.
```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    // Get two strings
    string s = get_string("s: ");
    string t = get_string("t: ");

    // Compare strings' addresses
    if (s == t)
    {
        printf("Same\n");
    }
    else
    {
        printf("Different\n");
    }
}
```
의도한대로 비교하려면 문자의 주소가 아닌 실제 값을 비교해야 한다.  
문자열을 복사할 때 메모리 할당 함수인 `malloc()`을 사용할 수 있다.
```c
#include <cs50.h>
#include <ctype.h>
#include <stdio.h>
#include <string.h>

int main(void)
{
    char *s = get_string("s: ");

    char *t = malloc(strlen(s) + 1);

    for (int i = 0, n = strlen(s); i < n + 1; i++)
    {
        t[i] = s[i];
    }

    t[0] = toupper(t[0]);

    printf("s: %s\n", s);
    printf("t: %s\n", t);
}
```
## Swap
swap 함수의 인자로 받은 int 변수는 복사된 값이므로 실제 값이 변경되지 않는다.  
포인터를 이용해야 한다.  
```c
void swap(int *a, int *b);

int main(void)
{
    int x = 1;
    int y = 2;

    printf("x is %i, y is %i\n", x, y);
    swap(&x, &y);
    printf("x is %i, y is %i\n", x, y);
}

void swap(int *a, int *b)
{
    int tmp = *a;
    *a = *b;
    *b = tmp;
}
```
## Memory layout
1. 컴파일러가 컴파일하면 0,1의 머신코드들이 메모리의 맨 위에 저장된다.  
2. 글로벌 변수가 그 아래에 저장된다.  
3. malloc으로 메모리를 할당하면 힙에서 메모리를 할당한다. — heap  
4. 로컬변수들은 아래부터 쌓이는 스택 영역에 저장된다. — Stack  

## Files
`fopen()`은 파일의 주소(`FILE` 타입의 pointer)를 리턴하는 함수로,  
첫번째 인자로 파일명, 두번째 인자로 `r` for read, `w` for write, `a` for append 등을 받는다.
we can read from and write to.
```c
int main(void)
{
    // Open file
    FILE *file = fopen("phonebook.csv", "a");

    // Get strings from user
    char *name = get_string("Name: ");
    char *number = get_string("Number: ");

    // Print (write) strings to file
    fprintf(file, "%s,%s\n", name, number); // 파일에 출력

    // Close file
    fclose(file);
}
```
## JPEG
```c
#include <stdio.h>

int main(int argc, char *argv[])
{
    if (argc != 2)
    {
        return 1;
    }

    FILE *file = fopen(argv[1], "r");

    if (file == NULL)
    {
        return 1;
    }
 
    unsigned char bytes[3];
    fread(bytes, 3, 1, file);

    if (bytes[0] == 0xff && bytes[1] == 0xd8 && bytes[2] == 0xff)
    {
        printf("Maybe\n");
    }
    else
    {
        printf("No\n");
    }
    fclose(file);
}
```
