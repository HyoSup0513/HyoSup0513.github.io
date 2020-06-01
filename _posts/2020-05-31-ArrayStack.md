---
layout: post
title: C Array Stack Implementation 배열 스택 
comments: true
categories: [Data Structure]
---

# Array Stack 배열 스택

## 스택이란 ?

- 리스트와 같이 선형 (Sequential) 구조
- 리스트와 다르게 LIFO(후입 선출)
  - 자료의 추가와 제거가 TOP에서 이루어 진다.

## 스택에 필요한 주요 Operations

- Pop - 스택의 Top에 있는 자료를 제거한 후 반환한다.
- Push - 스택의 Top에 자료를 추가한다.
- Peek - 스택의 Top에 있는 자료를 반환한다. (제거 x)
- isEmpty - 스택이 비어있는지 확인한다.

![stackimg1](/public/images/stack1.PNG)

## 배열 스택으로 구현한다면?

- 구현이 간단하다.
- 스택의 크기를 미리 정해야 한다.
- 추가 Operation, isFull 을 추가해서 스택이 가득 차 있는지 확인이 필요하다.

## Implementation 배열 스택 구현

Array로 구현하기 때문에 노드 사이의 Link는 필요 없고 단순히 Data만 저장한다.
노드로 Data를 감싸 동시에 여러개의 Data를 저장할 수 있다.
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

typedef struct ArrayStackNodeType {
	char data;
}ArrayStackNode;
```

maxcount 로 최대로 저장할 수 있는 원소의 개수를 정한다.
스택의 크기는 배열 pData의 원소의 개수와 같다.
```
typedef struct ArrayStackType {
	int maxcount; // Maxium number of data.
	int currentcount; // Currnet number of stored data.
	ArrayStackNode* pData; // 1 dimensional array to store data.
}ArrayStack;
```

#### Create an array stack with a specific size.

```
ArrayStack* createArrayStack(int size) {

	if(size <= 0){
		return NULL;
	}

	ArrayStack* pReturn = NULL;
	pReturn = (ArrayStack*)malloc(sizeof(ArrayStack)); // Memory allocation.

	if(pReturn == NULL){
		return NULL;
	}

	else{
		memset(pReturn, 0, sizeof(ArrayStack)); // Memory initialization.
		pReturn->maxcount = size; // Set Maximum number of data.

		// Creating and initializing arrays with elements as many as the max number of data.
		pReturn->pData = (ArrayStackNode*)malloc(sizeof(ArrayStackNode) * size);
		memset(pReturn->pData, 0, sizeof(ArrayStackNode) * size);
	}

	return pReturn;
}
```

#### Check if the array stack is full.

```
int isArrayStackFull(ArrayStack* pStack) {

	int ret = 0;
	if (pStack != NULL) {
		if (pStack->currentcount == pStack->maxcount) {
			ret = 1;
		}
	}

	return ret;
}
```

#### Push a data to the stack.

```
int pushAS(ArrayStack* pStack, char data) {

	int ret = 0;
	// determine if the array stack is full.
	if (isArrayStackFull(pStack) == 0) {
		// push data to TOP.
		pStack->pData[pStack->currentcount].data = data;

		// Change the position of TOP.
		pStack->currentcount++;
		ret = 1;
	}
	else {
		printf("Error, stack is full !, pushAS()\n");
	}
	return ret;
}
```

#### Check if the stack is empty

```
int isArrayStackEmpty(ArrayStack* pStack) {
	int ret = 0;
	if (pStack != NULL) {
		if (pStack->currentcount == 0) {
			ret = 1;
		}
	}

	return ret;
}
```

#### Pop a data from the stack

```
ArrayStackNode* popAS(ArrayStack* pStack) {
	ArrayStackNode* pReturn = NULL;

	// Check if the array stack if empty.
	if (0 == isArrayStackEmpty(pStack)) {
		// Memory allocation and memory check for nodes to return.
		pReturn = (ArrayStackNode*)malloc(sizeof(ArrayStackNode));

		if (pReturn != NULL) {
			// Enter the data to be returned to the node.
			pReturn->data = pStack->pData[pStack->currentcount - 1].data;
			// Change the position of TOP, to left.
			pStack->currentcount--;
		}

		else {
			printf("Error, memory allocation, popAS()\n");
		}
	}

	return pReturn;
}
```

#### Peek a data from stack (it's not removing)

```
ArrayStackNode* peekAS(ArrayStack* pStack) {
	ArrayStackNode* pReturn = NULL;
	if (pStack != NULL) {
		// Check if the array stack is empty.
		if (isArrayStackEmpty(pStack) == 0) {
			// Speicfy a return value, return a pointer that points the top node of the array stack.
			pReturn = &(pStack->pData[pStack->currentcount - 1]);
		}
	}

	return pReturn;
}
```

#### Delete the stack, free the memory

```
void deleteArrayStack(ArrayStack* pStack) {
	if (pStack != NULL) {
		if (pStack->pData != NULL) {
			free(pStack->pData);
		}
		free(pStack);
	}
}
```

#### Display the stack to see

```
void displayArrayStack(ArrayStack* pStack) {
	int i = 0;
	if (pStack != NULL) {
		int size = pStack->maxcount;
		int top = pStack->currentcount;

		printf("Stack Size: %d, Number of nodes: %d\n", pStack->maxcount, pStack->currentcount);

		for (i = size - 1; i >= top; i--) {
			printf("[%d]-[Empty]\n", i);
		}

		for (i = top-1; i >= 0; i--) {
			printf("[%d]-[%c]\n", i, pStack->pData[i].data);
		}
	}
}
```

#### Check the Implementation

```
int main(int argc, char* argv[]) {
	ArrayStack* pStack = NULL;
	ArrayStackNode* pNode = NULL;

	pStack = createArrayStack(6);
	if (pStack != NULL) {
		pushAS(pStack, 'A');
		pushAS(pStack, 'B');
		pushAS(pStack, 'C');
		pushAS(pStack, 'D');
		displayArrayStack(pStack);

		pNode = popAS(pStack);
		if (pNode != NULL) {
			printf("Pop value-[%c]\n", pNode->data);
			free(pNode);
		}

		displayArrayStack(pStack);

		pNode = peekAS(pStack);
		if (pNode != NULL) {
			printf("Peek value-[%c]\n", pNode->data);
		}
		displayArrayStack(pStack);

		deleteArrayStack(pStack);
	}
	return 0;
}
```

[Github Link](https://github.com/HyoSup0513/study/tree/master/Datastructure/Stack)
