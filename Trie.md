# Trie

## 개요

여러 개의 문자열을 가지고 있을 때, 어떤 문자열이 그 문자열 중 하나인지 알아내는 방법은 뭐가 있을까?

가장 먼저 떠오르는 방법은 일일이 비교해보면 된다. 

예를 들어, 최대 길이가 `m`인 문자열 `n`개의 집합에서 마찬가지로 최대 길이가 `m`인 임의의 문자열이 그 문자열들의 집합에 포함되는지를 일일이 확인하면, 최악의 경우 `O(n*m)`의 비교 횟수가 필요하다.



## Trie 자료구조는 언제 사용할까?

- 검색어 자동완성, 사전에서 찾기 그리고 문자열 검사 같은 부분에서 사용할 수 있다.



## 시간복잡도

- 제일 긴 문자열의 길이를 `L` 총 문자열들의 수를 `M`이라 할 때 시간복잡도는 아래와 같다.
- 생성시 시간복잡도: `O(M*L)`,  `M`개에 대해서 트라이 자료구조에 넣는건 가장 긴 문자열 길이 `L`만큼 걸리므로, `O(M*L)` 의 시간이 걸린다.
- 탐색시 시간복잡도: `O(L)`, 트리를 타고 들어가도 가장 긴 문자열의 길이만큼만 탐색하기 때문에 `O(L)`만큼 걸린다.



## Trie 자료구조의 특징

1. Trie 알고리즘은 **노드를 이용한 Tree 형태**로 이루어져 있다.

2. 문자열의 **끝을 알리는 flag가 존재**한다.



frodo, front, firefox, fire 이라는 단어가 입력되었을때, 다음과 같은 트리가 생성된다.

firefox 와 fire 처럼 한 줄이지만, flag를 통해 두개의 단어가 있다는 것을 알 수 있다.



![img](https://mblogthumb-phinf.pstatic.net/MjAxOTEyMTdfODEg/MDAxNTc2NTYwMDI4MTMz.1e8_EuMhqD4ihjX8HbSYlQr_j7QvNseEVxH--dAjfH0g.he-A1TE1CTSRij8udR5LWSvgrZmggeRO9MmVS0lz0a0g.PNG.cjsencks/image.png?type=w800)



## 구현

Node와 Trie로 구성된다.



### Node

```python
class Node(object):
    def __init__(self, key, data=None):
        self.key = key
        self.data = data
        self.children = {}
```

노드에는 세 가지가 구현되어 있다.

1. key - 값으로 입력될 문자

2. data - 문자열의 종료를 알리는 flag. ( True/False로도 구현할 수 있지만, 돌아가는 일이 없게 하기위해 전체 문자열을 저장)

3. children - 자식노드를 저장



### Trie

```python
class Trie:
    def __init__(self):
        self.head = Node(None)
        
    def insert(self, string):
        current_node = self.head

        for char in string:
            if char not in current_node.children:
                current_node.children[char] = Node(char)
            current_node = current_node.children[char]
        current_node.data = string

    def search(self, string):
        current_node = self.head

        for char in string:
            if char in current_node.children:
                current_node = current_node.children[char]
            else:
                return False

        if current_node.data:
            return True
        else:
            return False

    def starts_with(self, prefix):
        current_node = self.head
        words = []

        for p in prefix:
            if p in current_node.children:
                current_node = current_node.children[p]
            else:
                return None

        current_node = [current_node]
        next_node = []
        while True:
            for node in current_node:
                if node.data:
                    words.append(node.data)
                next_node.extend(list(node.children.values()))
            if len(next_node) != 0:
                current_node = next_node
                next_node = []
            else:
                break

        return words
```

각각의 메서드에 대한 설명은 다음과 같다.

1. head를 빈 노드로 설정
2. insert 함수 : 트리를 생성하기 위한 함수이다. 입력된 문자열의 문자를 하나씩 children에 확인 후 저장하고 문자열을 다 돌면 마지막 노드의 data에 문자열을 저장한다.
3. search 함수 : 문자열이 존재하는지에 대한 여부를 리턴하는 함수이다. 문자열을 하나씩 돌면서 확인 후 마지막 노드가 data가 존재한다면 True를, 그렇지 않거나 애초에 children에 존재하지 않는다면 False를 리턴한다.
4. starts_with 함수 : prefix단어로 시작하는 단어를 찾고 배열로 리턴하는 함수입니다. prefix단어까지 tree를 순회 한 이후 그다음부터 data가 존재하는 것들만 배열에 저장하여 리턴합니다.



## 예제

```python
trie = Trie()
word_list = ["frodo", "front", "firefox", "fire"]
for word in word_list:
    trie.insert(word)
print(trie.search("friend"))
print(trie.search("frodo"))
print(trie.search("fire"))
print(trie.starts_with("fire"))
print(trie.starts_with("fro"))
print(trie.starts_with("jimmy"))
print(trie.starts_with("f"))
```



```python
trie.search("friend")
>>False
trie.search("frodo")
>>True
trie.search("fire")
>>True
trie.starts_with("fire")
>>['fire', 'firefox']
trie.starts_with("fro")
>>['frodo', 'front']
trie.starts_with("jimmy")
>>None
trie.starts_with("f")
>>['fire', 'frodo', 'front', 'firefox']
```



> 참고자료
>
> https://m.blog.naver.com/cjsencks/221740232900
>
> https://twpower.github.io/187-trie-concept-and-basic-problem#%EC%B0%B8%EA%B3%A0%EC%9E%90%EB%A3%8C

