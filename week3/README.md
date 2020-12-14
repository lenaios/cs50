# Lecture 3
- Searching
- Big O
- Linear search
- Structs
- Sorting
- Selection sort
- Recursion
- Merge sort
## Searching
- linear search, where we move in a line, since our array isn’t sorted.
- binary search, since we can divide our problem in two with each step.
## Big O
알고리즘이 최악인 경우의 running time이다.  
- O(n^2)
- O(n log n)
- O(n) (linear search)
- O(log n) (binary search)
- O(1)
## Big Ω
big Omega notation은 알고리즘이 최선이 경우의 running time을 말한다. 
- Ω(n^2)
- Ω(n log n)
- Ω(n) (counting the number of items)
- Ω(1) (linear search, binary search)  
## Linear search
we can return an exit code of either 0 (for success) or 1 (for failure).  
`strcmp` (in `string` library)를 사용해서 문자열을 비교할 수 있다.  
```c
#include <cs50.h>
#include <stdio.h>
#include <string.h>

int main(void)
{
    // An array of names
    string names[] = {"EMMA", "RODRIGO", "BRIAN", "DAVID"};

    // Search for EMMA
    for (int i = 0; i < 4; i++)
    {
        if (strcmp(names[i], "EMMA") == 0)
        {
            printf("Found\n");
            return 0;
        }
    }
    printf("Not found\n");
    return 1;
}
```
구조체를 정의하는 방법도 있다.  
```c
typedef struct
{
    string name;
    string number;
}
person;

int main(void)
{
    person people[4];

    people[0].name = "EMMA";
    people[0].number = "617–555–0100";

    people[1].name = "RODRIGO";
    people[1].number = "617–555–0101";

    people[2].name = "BRIAN";
    people[2].number = "617–555–0102";

    people[3].name = "DAVID";
    people[3].number = "617–555–0103";

    // Search for EMMA
    for (int i = 0; i < 4; i++)
    {
        if (strcmp(people[i].name, "EMMA") == 0)
        {
            printf("Found %s\n", people[i].number);
            return 0;
        }
    }
    printf("Not found\n");
    return 1;
}
```
## Sorting
- O(n^2) bubble sort  
And Ω for bubble sort is still n^2, since we still check each pair of elements for n – 1 passes.
## Selection sort
- O(n^2) bubble sort, selection sort  
The best case, Ω, is also n^2.  

만약, elements가 정렬된 상태라면 running time은 달라질 수 있다.  
- Ω(n^2) selection sort
- Ω(n) bubble sort

## Recursion
피라미드의 높이 `h`가 주어질 때, 피라미드를 그리는 함수 `draw`를 재귀로 구현할 수 있다.  
```c
#include <cs50.h>
#include <stdio.h>

void draw(int h);

int main(void)
{
    // Get height of pyramid
    int height = get_int("Height: ");

    // Draw pyramid
    draw(height);
}

void draw(int h)
{
    // If nothing to draw
    if (h == 0)
    {
        return;
    }

    // Draw pyramid of height h - 1
    draw(h - 1);

    // Draw one more row of width h
    for (int i = 0; i < h; i++)
    {
        printf("#");
    }
    printf("\n");
}
```
## Merge sort
We can take the idea of recusion to sorting, with another algorithm called merge sort.  
It took a lot of steps, but it actually took fewer steps than the other algorithms we’ve seen so far.  
```
7 | 4 | 5 | 2 | 6 | 3 | 8 | 1
4   7 | 2   5 | 3   6 | 1   8
2   4   5   7 | 1   3   6   8
1   2   3   4   5   6   7   8
```
- O(n log n) merge sort.  
The best case, Ω, is still n log n, since we still sort each half first and then merge them together

최악의 경우와 최선의 경우의 running time이 같을 경우 Θ, Theta로 표기할 수 있다.  
which we use to describe running times of algorithms if the upper bound and lower bound is the same.  
For example, merge sort has Θ(n log n) since the best and worst case both require the same number of steps.  
And selection sort has Θ(n^2).
