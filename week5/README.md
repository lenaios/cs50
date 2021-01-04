# Lecture 5
- Pointers
- Resizing arrays
- Data structures
- Linked Lists
- More data structures

## Pointers
`malloc()`은 할당하고 싶은 메모리를 byte 단위로 줄 수 있다.  
```c
int main(void)
{
    int *x;
    int *y;

    x = malloc(sizeof(int));

    *x = 42;
    *y = 13;
}
```
`malloc` 함수는 메모리가 부족한 경우 등 메모리 할당에 문제가 생길 경우 NULL를 반환하므로, 체크하는 것이 좋다.  
배열처럼 대괄호 `[]`를 사용해서 각 byte에 접근할 수 있다.
```c
int main(void)
{
    int *list = malloc(3 * sizeof(int));
    if (list == NULL)
    {
        return 1;
    }
    
    list[0] = 1;
    list[1] = 2;
    list[2] = 3;
}
```
## Linked Lists
연결 리스트는 다음 노드의 포인터를 노드의 멤버로 갖고 있다.  
다음과 같이 노드 구조체를 정의할 수 있다.
```c
typedef struct node
{
    int number;
    struct node *next;
}
node;
```
pointer의 속성에 접근하는 방법은 다음과 같이 표현할 수 있다.
```c
node *n = malloc(sizeof(node));
(*n).number
n->number // arrow notation
```

## More data structures
- tree
- hash table
- trie
- queue — FIFO
- stack  — LIFO  

또 다른 자료 구조로 two pointer를 갖는 tree가 있다.  
binary search tree로 정의해서 재귀적으로 탐색할 수 있다.
```c
typedef struct node
{
    int number;
    struct node *left;
    struct node *right;
} node;
```
hash table은 연결 리스트와 배열의 조합이다.  
trie(is short for “retrieval”)는 트리 구조인데, 각 노드가 배열로 이루어져 있다.
