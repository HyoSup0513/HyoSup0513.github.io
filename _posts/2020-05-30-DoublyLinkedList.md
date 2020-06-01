---
layout: post
title: [c++] Doubly Linked List Implementation 이중 연결 리스트 구현
comments: true
categories: [Data Structure]
---

# Doubly Linked List 이중 연결 리스트

## 리스트란?

- 선형 (Sequential) 구조
- 리스트는 자료를 순서대로 저장하는 자료구조이다.
- 리스트는 한 줄로 데이터를 저장한다.

## 이중 연결 리스트의 특징

- 노드 사이의 연결이 양뱡향이다.
  - 각 노드는 다음 노드뿐만 아니라 이전 노드에 대한 링크를 추가로 가지고 있다.
  - 따라서 이전 노드로의 접근이 한번에 가능하다.
- 각각의 노드에 추가적인 연결 정보를 저장하기 때문에 메모리 공간을 더 많이 사용하며 구현이 더 복잡하다.

![screen](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2014/03/DLL1.png)

## Structure

- ### header file

```
#pragma once

class dlist {

public:
	// Constructor
    dlist() { }

    struct node {
        int value;
        node* next;
        node* prev;
    };

    node* head() const { return _head; }
    node* tail() const { return _tail; }

    node* at(int n) const;

    void insert(node* previous, int value);

    void remove(node* which);

    void push_back(int value);

    void push_front(int value);

    void pop_front();

    void pop_back();

    int size() const;

    bool empty() const;

private:
    node* _head = nullptr;
    node* _tail = nullptr;
};
```

* Equality of two lists O(m), a == b

m is the length of the shorter of the two lists.

```
bool operator== (const dlist& a, const dlist& b) {
    dlist::node* tempA = a.head();
    dlist::node* tempB = b.head();

    if (a.size() != b.size())
        return false;
    else {
        while (tempA != nullptr)
        {
            if (tempA->value != tempB->value)
                return false;
            else {
                tempA = tempA->next;
                tempB = tempB->next;
            }
        }
        return true;
    }
};
```

* List concatenation O(n), a + b

Returns a new list consisting of all the elements of a, followed by all the elements of b

```
dlist operator+ (const dlist& a, const dlist& b) {
    dlist::node* tempB = b.head();
    dlist::node* tempA = a.head();
    dlist c;
    while (tempA != nullptr)
    {
        c.push_back(tempA->value);
        tempA = tempA->next;
    }
    while (tempB != nullptr)
    {
        c.push_back(tempB->value);
        tempB = tempB->next;
    }

    return c;
};
```

* Reverse list O(n)

Returns a new list that is the reversal of l; that is, a new list
containing the same elements as l but in the reverse order.

```
dlist reverse(const dlist& l) {
    dlist::node* tempA = l.tail();
    dlist c;
    while (tempA != nullptr)
    {
        c.push_back(tempA->value);
        tempA = tempA->prev;
    }

    return c;
};
```

- ### cpp file

* at O(n)

Returns the node at a particular index (0 is the head)

```
dlist::node* dlist::at(int n) const {
	if (n >= size())
		return nullptr;
	else if (n < 0)
		return head();
	else {
		node* current = head();

		for (int i = 0; i < n; i++) {
			current = current->next;
		}
	}

};
```

* Insert the node O(1)

Insert a new value, after an existing one.

```
void dlist::insert(node* previous, int value)
{
	if (previous == nullptr && _head == nullptr && _tail == nullptr) {

		node* newNode = new node;
		newNode->value = value;

		_head = newNode;
		_tail = _head;
		_head->prev = nullptr;
		_head->next = nullptr;

	}
	else if (_head == _tail && size() == 1) {
		node* newNode = new node;
		newNode->value = value;
		_head->next = newNode;
		_tail = newNode;
		_tail->next = nullptr;
		_tail->prev = _head;
	}
	else if (previous != _head && previous != _tail && size() == 2) {
		node* newNode = new node;
		newNode->value = value;
		_tail->next = newNode;
		_tail = newNode;
		_tail->next = nullptr;
	}
	else if (previous == _tail && previous != _head) {
		push_back(value);
	}

	else {
		node* newNode = new node;
		newNode->value = value;
		node* storenode = new node;

		storenode = previous->next;
		previous->next = newNode;
		storenode->prev = previous->next;
		newNode->next = storenode;
		newNode->prev = previous;
	}
}
```

* Delete the node O(1)

```
void dlist::remove(node* which) {
	node* temp = which;
	if (which == nullptr) {
		return;
	}

	else if (which != nullptr) {

		if (which == _head) {
			node* newNode = new node;
			newNode->value = which->value;
			_head = which->next;
			_head->prev = nullptr;
		}

		else {
			which = which->next;
		}
	}
}
```

* Push back the node O(1)

Add a new element to the end of the list

```
void dlist::push_back(int value) {

	if (_head == nullptr || _tail == nullptr) {
		node* newNode = new node;
		newNode->value = value;

		_head = newNode;
		_tail = _head;
		_head->prev = nullptr;
		_head->next = nullptr;
		_head = _tail;
	}
	else {
		node* newNode = new node;
		node* storeNode = new node;
		newNode->value = value;

		storeNode = _tail;
		_tail = newNode;
		_tail->prev = storeNode;
		_tail->next = nullptr;
		if (storeNode != nullptr)
			storeNode->next = _tail;
	}
}
```

* Push front the node O(1)

Add a new element to the beginning of the list

```
void dlist::push_front(int value) {

	if (_head == nullptr || _tail == nullptr) {
		node* newNode = new node;
		newNode->value = value;

		_head = newNode;
		_tail = _head;
		_head->prev = nullptr;
		_head->next = nullptr;
	}

	else {
		node* newNode = new node;
		node* storeNode = new node;
		newNode->value = value;

		storeNode = _head;
		_head = newNode;
		_head->next = storeNode;
		_head->prev = nullptr;
		if (storeNode != nullptr)
			storeNode->prev = _head;
	}
}
```

* Pop front the node O(1)

Remove the first element of the list

```
void dlist::pop_front() {

	if (_head == nullptr || _tail == nullptr) {
		return;
	}
	else if (size() == 1) {
		_head = nullptr;
		_tail = nullptr;
	}
	else {
		node* newNode = new node;
		newNode = _head->next->next;

		_head = _head->next;
		_head->prev = nullptr;

	}

}
```

* Pop back O(1)

Remove the last element of the list

```
void dlist::pop_back() {

	if (_head == nullptr || _tail == nullptr) {
		return;
	}
	else if (size() == 1) {
		_head = nullptr;
		_tail = nullptr;
	}
	else {

		_tail = _tail->prev;
		_tail->next = nullptr;

	}
}
```

* Get the size of the list

Should run in O(n) time at the worst

```
int dlist::size() const {
	int listsize = 0;

	node* current = head();
	if (current != nullptr) {

		while (current != nullptr) {
			listsize++;
			current = current->next;
		}
	}
	return listsize;
}
```

* Check empty O(1)

```
bool dlist::empty() const{
	return head() == tail();
}
```

[Github Link](https://github.com/HyoSup0513/study/tree/master/Datastructure/Doubly%20Linked%20List)
