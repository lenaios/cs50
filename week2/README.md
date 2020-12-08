# Lecture 2
- Compiling
- Debugging
- help50 and printf
- debug50
- check50 and style50
- Data Types
- Memory
- Arrays
- Strings
- Command-line arguments
- Readability
- Encryption

## Compiling
컴파일링은 다음과 같이 4단계로 이루어진다.  
- preprocessing
- compiling
- assembling
- linking

Preprocessing은 `#include`한 `header file`을 코드로 바꾸는 과정이다.  
```
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    string name = get_string("Name: ");
    printf("hello, %s\n", name);
}
```
… will be preprocessed into:
```
string get_string(string prompt);
int printf(const char *format, ...);

int main(void)
{
    string name = get_string("Name: ");
    printf("hello, %s\n", name);
}
```
Compiling은 `source code`를 CPU가 실제로 이해하는 언어인 `assembly code`로 변경한다.  
Assembling은 `assembly code`를 CPU가 실행할 수 있는 이진수, `machine code`로 변경한다.  
Linking은 연결하려는 각 컴파일된 파일을 하나로 합친다.  

## Debugging
버그는 우리의 프로그램에서 의도하지 않은 실수이다. 디버깅은 이러한 버그를 찾고 고치는 과정이다.  
`printf`, `help50`, `debug50`

## Data Types
C에는 여러 데이터 타입이 있다. 각 타입의 변수를 생성할 때 다음과 같은 바이트를 차지한다.  
- bool 1 byte
- char 1 byte
- int 4 bytes
- float 4 bytes
- long 8 bytes
- double 8 bytes
- string ? bytes

## Arrays
A list of variables stored, one after another in a contiguous chunk of memory, is called an array.  
`loop`를 통해서 배열의 값에 접근할 수 있다.
```
#include <cs50.h>
#include <stdio.h>

float average(int length, int array[]);

int main(void)
{
    // Get number of scores
    int n = get_int("Scores:  ");

    // Get scores
    int scores[n];
    for (int i = 0; i < n; i++)
    {
        scores[i] = get_int("Score %i: ", i + 1);
    }

    // Print average
    printf("Average: %.1f\n", average(n, scores));
}

float average(int length, int array[])
{
    int sum = 0;
    for (int i = 0; i < length; i++)
    {
        sum += array[i];
    }
    return (float) sum / (float) length;
}
```
배열 자체를 할당하는 것은 불가능하다.
```
#include <stdio.h>

int main(void)
{
    int foo[5] = {1, 2, 3, 4, 5};
    int bar[5];

    bar = foo; // error: array type 'int [5]' is not assignable
}
```
## Strings
Strings은 사실 characters의 배열이다. string은 모든 비트가 0인 `\0`로 끝난다.  
`\0`은 다른 변수를 저장하는 메모리의 시작과 구분하기 위한 문자이다.  
string은 종단 문자 `\0`를 포함한 바이트가 필요하다. 
```
string names[4];
names[0] = "EMMA";
names[1] = "RODRIGO";
names[2] = "BRIAN";
names[3] = "DAVID";

printf("%s\n", names[0]);
printf("%c%c%c%c\n", names[0][0], names[0][1], names[0][2], names[0][3]);
```

## Command-line arguments
프로그램을 실행시키면서 명령행 인자를 받을 수도 있다.  
`main` 함수의 리턴타입이 `int`인 이유는 에러 발생 시 특정 숫자를 리턴하도록 되어있기 때문이다.  
프로그램이 에러 없이 종료되면 0을 리턴한다.  
```
#include <cs50.h>
#include <stdio.h>

int main(int argc, string argv[])
{
    if (argc == 2)
    {
        printf("hello, %s\n", argv[1]);
    }
    else
    {
        printf("hello, world\n");
    }
}
```
