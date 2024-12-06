
# PyPy3과 Python3의 차이 

백준 문제를 풀면서 아래 코드를 실행했더니 


```py
# 28464번 Potato

import sys
input = sys.stdin.readline

# 접시개수
N = int(input())
dishes = list(map(int, input().strip().split()))

dishes.sort()

pk = sum(dishes[N//2:])
sw = sum(dishes[:N//2])
print(sw, pk)
```

아래와 같은 결과가 나왔다. 

|  언어  |  메모리(kb)  |  시간(ms)  |
|:-----:|:---:|:---:|
|  PyPy3  |  141484  |  156  |
|  Python3  |  54036  |  136  |


## Python3과 PyPy3의 차이

PyPy3는 Python3의 실행시 시간이 매우 오래걸리는 단점을 개선하고자 JIT(Just-In-Tume)컴파일 방식을 도입한 것이다. 

### Python의 동작방식 

Python은 C로 구현되어 있다. CPython은 인터프리터이면서 컴파일러이다.

컴파일언어 : 소스코드를 기계어로 compile > 실행파일을 만듬 > 실행 (Run Time)
인터프리터 언어 : 코드를 한줄씩 읽어가며 실행. 동적 타이핑을 지원하며 변수의 타입을 명시하지 않아도 된다. 그러나 상대적으로 속도가 느리다는 단점이 있다. 이를 개선하기 위해 JIT 컴파일러와 같은 기술이 나왔다 (Python -> PyPy, Javascript -> V8엔진)

### PyPy의 동작방식

PyPy는 JIT컴파일러를 사용해 Python 코드를 실행하는데, 정렬과 같은 C확장 함수는 JIT의 이점을 활용하지 못한다. 

코드 실행 전에 컴파일 단계를 거치게 되는데 이 과정에서 추가적인 오버헤드를 발생시킨다. 작업이 간단하고 반복작업이 적은 경우에는 JIT 초기화 비용이 성능을 저하시킬 수 있다. 

또한 메모리를 동적으로 할당하고 최적화를 시도하기 때문에 작은 규모에서는 메모리 사용량이 더 높게 나올 수 있다. 



## 언제 뭘 쓰면 좋을까 

### PyPy를 써야할 때 

1. 반복문이 많거나 
2. 동적인 데이터 구조가 많이 사용되거나 
3. 계산량이 많은 문제 