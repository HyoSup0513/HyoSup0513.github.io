---
layout: post
title: C Array List Implementation 배열 리스트 구현
comments: true
categories: [Data Structure]
tags: [List]
toc: true
---

# Array List

## 리스트란?

- 선형 (Sequential) 구조
- 리스트는 자료를 순서대로 저장하는 자료구조이다.
- 리스트는 한 줄로 데이터를 저장한다.

## 배열 리스트의 추상 자료형

- 리스트 생성 CreateList()
  - 빈 리스트를 생성
- 자료 추가 addListData()
  - Data를 원하는 Position에 추가
- 자료 반환 getListData()
  - Position에 있는 Data 값을 반환
- 자료 개수 반환 getListLength()
  - 리스트의 자료 개수 반환
- 자료 제거 removeListData()
  - 리스트의 Position에 있는 자료 제거
- 리스트 삭제 deleteList()
  - 리스트의 모든 자료 삭제, 메모리 해제

배열 리스트의 노드 선언

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct ArrayListNodeType {
	int data;
} ArrayListNode;
```

배열 리스트를 나타내는 구조체 선언

```
typedef struct ArrayListType {
	int maxCount; // 최대 자료 개수: 배열의 크기
	int currentCount; // 현재 자료 개수
	ArrayListNode *pData; // 자료 저장을 위한 1차원 배열
} ArrayList;
```

배열 리스트 생성

```
ArrayList *createList(int count) {
	if (count <= 0)
		return NULL;

	else {
		ArrayList* pReturn = (ArrayList*)malloc(sizeof(ArrayList));

		if (pReturn != NULL) {
			pReturn->maxCount = count;
			pReturn->currentCount = 0;
			pReturn->pData = (ArrayListNode*)malloc(sizeof(ArrayListNode) * count);

			// pReturn->pData 가 가리키는 메모리를
      // sizeof(ArrayListNode) * count 바이트만큼 0으로 설정
			memset(pReturn->pData, 0, sizeof(ArrayListNode) * count);

			return pReturn;
		}
		else
			return NULL;

	}
}
```

특정 위치에 자료 추가

```
int addListData(ArrayList* pList, int position, int data) {
	if (pList == NULL)
		return 1;
	if (pList->currentCount < pList->maxCount) {
		if (position < 0 && position > pList->currentCount)
			return 2;
	}

	int i = 0;
    // 추가되는 위치와 그 오른쪽에 있는 기존 자료를 모두 오른쪽으로 한칸씩 이동

	for (i = pList->currentCount - 1; i >= position; i--) {
		pList->pData[i + 1] = pList->pData[i];
	}

	pList->pData[position].data = data; // 실제 자료 추가
	pList->currentCount++; // 현재 저장된 자료 개수를 1 증가
	return 0;
}
```

특정 위치에 있는 자료 제거

```
int removeListData(ArrayList* pList, int position){
	if (pList == NULL)
		return 1;
	if (position < 0 && position > pList->currentCount - 1)
		return 2;

	int i = 0;
    // 제거되는 원소의 위치와 그 오른쪽에 있는 원소를 왼쪽으로 한칸씩 이동
	for (i = position; i < pList->currentCount - 1; i++) {
		pList->pData[i] = pList->pData[i + 1];
	}

	pList->currentCount--;
	return 0;
}
```

특정 위치에 있는 데이터 값 반환

```
int getListData(ArrayList* pList, int position) {
	if (pList == NULL)
		return 1;
	if (position < 0 && position > pList->currentCount - 1)
		return 2;

	return pList->pData[position].data;
}
```

배열 리스트를 제거

```
void deleteList(ArrayList* pList) {
	if (pList != NULL) {
		if (pList->pData != NULL) {
			free(pList->pData);
		}
		free(pList);
	}
}
```

배열 리스트의 길이 반환

```
int getListLength(ArrayList* pList) {
	return pList->currentCount;
}
```

테스트

```
int main() {
	ArrayList* pList = NULL;
	int value = 0;

	pList = createList(5);
	addListData(pList, 0, 10);
	addListData(pList, 1, 20);
	addListData(pList, 0, 30);

	// value = getListData(pList, 1);
	value = getListLength(pList);
	// printf("위치: %d, 값: %d\n", 1, value);
	printf("자료의 개수: %d\n", value);

	removeListData(pList, 0);
	deleteList(pList);

	return 0;
}
```

[GitHub](https://github.com/HyoSup0513/study/tree/master/Datastructure/Array%20List)
