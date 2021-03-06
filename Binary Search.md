# Binary Search (이진 탐색)



## 순차 탐색

- 리스트 안에 있는 특정한 데이터를 찾기 위해 앞에서부터 데이터를 하나씩 차례대로 확인하는 방법.

- 순차 탐색의 시간 복잡도는 O(N)이다.

```python
# 순차 탐색 소스코드 구현
def sequential_search(n, target, array):
    # 각 원소를 하나씩 확인하며
    for i in range(n):
        # 현재의 원소가 찾고자 하는 원소와 동일한 경우
        if array[i] == target:
            return i + 1 # 현재의 위치 반환(인덱스는 0부터 시작하므로 1 더하기)

print("생성할 원소 개수를 입력한 다음 한 칸 띄고 찾을 문자열을 입력하세요.")
input_data = input().split()
n = int(input_data[0]) # 원소의 개수
target = input_data[1] # 찾고자 하는 문자열

print("앞서 적은 원소 개수만큼 문자열을 입력하세요. 구분은 띄어쓰기 한 칸으로 합니다.")
array = input().split()

# 순차 탐색 수행 결과 출력
print(sequential_search(n, target, array))

```

- 결과

```python
input:
6 Hyokyun
Heymin Hyokyun Jiyoung Jiyeob MinKwan Yujin

output:
2

input:
5 Yujin
Heymin Hyokyun Jiyoung Jiyeob MinKwan

output:
None
```



## 이진 탐색

- 이진 탐색은 배열 내부의 데이터가 정렬되어 있어야만 사용할 수 있는 알고리즘이다.

  이진 탐색은 탐색 범위를 절반씩 좁혀가며 데이터를 탐색하는 특징이 있다.

- 이진 탐색은 위치를 나타내는 변수 3개를 사용한다. 탐색하고자 하는 범위의 시작점, 끝점, 그리고 중간점이다. 찾으려는 데이터와 중간점 위치에 있는 데이터를 반복적으로 비교해서 원하는 데이터를 찾는 게 이진 탐색 과정이다.

![bs](https://user-images.githubusercontent.com/50684682/136329755-ddb57300-e70c-4426-8681-fd2385407bc2.png)

- 이진 탐색의 시간 복잡도는 O(logN)이다.
- 이진 탐색 소스코드 구현(재귀 함수)

```python
# 이진 탐색 소스코드 구현(재귀 함수)
def binary_search(array, target, start, end):
    if start > end:
        return None
    mid = (start + end) // 2
    # 찾은 경우 중간점 인덱스 반환
    if array[mid] == target:
        return mid
    # 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
    if array[mid] > target:
        return binary_search(array, target, start, mid - 1)
    # 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
    elif array[mid] < target:
        return binary_search(array, target, mid + 1, end)

# n(원소의 개수)과 target(찾고자 하는 문자열)을 입력받기
n, target = list(map(int, input().split()))

# 전체 원소 입력받기
array = list(map(int, input().split()))

# 이진 탐색 수행 결과 출력
result = binary_search(array, target, 0, n - 1)
if result == None:
    print("원소가 존재하지 않습니다.")
else:
    print(result + 1)

```

- 이진 탐색 소스코드 구현(반복문)

```python
# 이진 탐색 소스코드 구현(반복문)
def binary_search(array, target, start, end):
    while start <= end:
        mid = (start + end) // 2
        # 찾은 경우 중간점 인덱스 반환
        if array[mid] == target:
            return mid
        # 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
        elif array[mid] > target:
            end = mid - 1
        # 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
        else:
            start = mid + 1
    return None

# n(원소의 개수)과 target(찾고자 하는 문자열)을 입력받기
n, target = list(map(int, input().split()))
# 전체 원소 입력받기
array = list(map(int, input().split()))

# 이진 탐색 수행 결과 출력
result = binary_search(array, target, 0, n - 1)
if result == None:
    print("원소가 존재하지 않습니다.")
else:
    print(result + 1)


```

- 결과

```python
input:
10 7
1 3 5 7 9 11 13 15 17 19

output:
4

input:
10 7
1 3 5 6 9 11 13 15 17 19

output:
원소가 존재하지 않습니다.
```





- 순차탐색과 이진탐색 비교

![binary-and-linear-search-animations](https://user-images.githubusercontent.com/50684682/136329626-169fc943-0076-47f5-80c1-985f4ef05181.gif)



## 코딩테스트에서의 이진탐색

- 이진 탐색 문제는 탐색 범위가 큰 상황에서의 탐색을 가정하는 문제가 많다.
- 처리해야 할 데이터의 개수나 값이 1000만 단위 이상으로 넘어가면 이진 탐색과 같이 O(logN)의 속도를 내야 하는 알고리즘을 떠올려야 문제를 풀 수 있는 경우가 많다.



> 출처 및 참고자료
>
> https://www.youtube.com/watch?v=SKcG0p73yo4
>
> https://ryu-e.tistory.com/23

