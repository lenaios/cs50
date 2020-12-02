# Lecture 1
- C
- hello, world
- Compilers
- String
- Scratch blocks in C
- Types, formats, operators
- More examples
- Memory, imprecision, and overflow

## C
C에서는 `main`함수로 프로그램을 실행시킨다.  
```
int main(void)
{

}
```
## Compilers
소스코드를 작성하고나면 기계가 이해할 수 있는 머신코드로 컴파일해야 한다.  
우리는 컴파일러를 이용해 컴파일 할 수 있는데 터미널에서 다음 명령어를 입력하면 된다.  
```
clang hello.c
```

## String
`\n` 문자를 사용해서 줄바꿈 할 수 있다.
```
#include <stdio.h>

int main(void)
{
    printf("hello, world\n");
}
```
`clang -o`를 사용해 실행파일 이름을 지정할 수 있다.
```
clang -o hello hello.c
```

`#include <cs50.h>` 라이브러리의 `get_string`을 사용해서 문자열 입력값을 받아올 수 있다.

```
string answer = get_string("What's your name?\n");
printf("hello, %s\n", answer);
```

`%s` 문자열  
`%i` int형  
`%.2f` float, double형, 소숫점 이하 2자리까지만 표시  
이 때, 단지 `clang -o string string.c`로 컴파일 시도하면 에러가 발생한다.  

```
$ clang -o string string.c
/tmp/string-aca94d.o: In function `main':
string.c:(.text+0x19): undefined reference to `get_string'
clang-7: error: linker command failed with exit code 1 (use -v to see invocation)
```

에러를 해결하기 위해서는 컴파일러에게 라이브러리를 추가했다는 것을 다음과 같이 알려줘야 한다.
```
clang -o string string.c -lcs50
```
## Scratch blocks in C
### condition
```
if (x < y)
{
    printf("x is less than y\n");
}
```
### loop
```
while (true)
{
    printf("hello, world\n");
}

for (int i = 0; i < 50; i++)
{
    printf("hello, world\n");
}
```
## Types, formats, operators
There are other types we can use for our variables  
- `bool`, a Boolean expression of either `true` or `false`  
- `char`, a single character like a or 2  
- `double`, a floating-point value with even more digits  
- `float`, a floating-point value, or real number with a decimal value  
- `int`, integers up to a certain size, or number of bits  
- `long`, integers with more bits, so they can count higher  
- `string`, a string of characters

For printf, too, there are different placeholders for each type:  
- `%c` for chars  
- `%f` for floats, doubles  
- `%i` for ints  
- `%li` for longs  
- `%s` for strings  

And there are some mathematical operators we can use:  
- `+` for addition
- `-` for subtraction
- `*` for multiplication
- `/` for division
- `%` for remainder

## More examples
함수를 정의할 경우, 함수의 프로토타입을 `main`함수 앞에 작성해야 한다.
```
#include <stdio.h>

void cough(void);

int main(void)
{
    for (int i = 0; i < 3; i++)
    {
        cough(); // 추상화
    }
}

void cough(void)
{
    printf("cough\n");
}
```
## Memory, imprecision, and overflow
컴퓨터는 메모리에 데이터를 저장하는데, 메모리는 유한한 하드웨어 장치이다.  
한정적인 메모리 때문에 imprecision and overflow가 발생할 수 있다.  
```
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    // Prompt user for x
    float x = get_float("x: ");

    // Prompt user for y
    float y = get_float("y: ");

    // Perform division
    printf("x / y = %.50f\n", x / y); // 소숫점 이하 50자리까지 표현
}
```
다음과 같이 `x/y`가 부정확한 값을 나타내는데, 이는 값을 저장할 bit가 충분하지 않기 때문에 컴퓨터가 유사한 값을 저장하면서 발생한다.
```
x: 1
y: 10
x / y = 0.10000000149011611938476562500000000000000000000000
```
다음 코드는 overflow를 발생시킨다. 저장 가능한 int의 비트를 초과하기 때문  
```
#include <stdio.h>
#include <unistd.h>

int main(void)
{
    for (int i = 1; ; i *= 2)
    {
        printf("%i\n", i);
        sleep(1);
    }
}
```
