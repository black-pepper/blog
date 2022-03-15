---
layout: single
title: "[Python] itertools - 순열, 조합"
categories: Algorithm
tag: [python, algorithm]
toc: true
author_profile: false
sidebar:
    nav: "docs" 
---

잘못된 부분이 있다면 댓글부탁드립니다:D

*아래에서 '배열'은 '리스트' 또는 '튜플'입니다.

## product - 중복 순열

product(배열1, 배열2, ... , *repeat=배열 중복 개수*)

```python
from itertools import product
result = product([1, 3, 2]) #repeat 기본값: 1
print(list(result))
#결과: [(1,), (3,), (2,)]
```

```python
from itertools import product
result = product([1, 3, 2], repeat=2)
print(list(result))
#결과: [(1, 1), (1, 3), (1, 2), (3, 1), (3, 3), (3, 2), (2, 1), (2, 3), (2, 2)]
```

```python
from itertools import product
result = product([1, 2], [3, 4], repeat=1)
print(list(result))
#결과: [(1, 3), (1, 4), (2, 3), (2, 4)]
```

```python
from itertools import product
result = product([1, 2], [3, 4], repeat=2)
print(list(result))
#결과: [(1, 3, 1, 3), (1, 3, 1, 4), (1, 3, 2, 3), (1, 3, 2, 4), (1, 4, 1, 3), (1, 4, 1, 4), (1, 4, 2, 3), (1, 4, 2, 4), (2, 3, 1, 3), (2, 3, 1, 4), (2, 3, 2, 3), (2, 3, 2, 4), (2, 4, 1, 3), (2, 4, 1, 4), (2, 4, 2, 3), (2, 4, 2, 4)]
```

```python
from itertools import product
result = product([1, 1, 1], repeat=2)
print(list(result))
#결과: [(1, 1), (1, 1), (1, 1), (1, 1), (1, 1), (1, 1), (1, 1), (1, 1), (1, 1)]
```





## permutations - 순열

permutations(배열, *선택 개수*)

```python
from itertools import permutations
result = permutations([1, 3, 2])
print(list(result))
#결과: [(1, 3, 2), (1, 2, 3), (3, 1, 2), (3, 2, 1), (2, 1, 3), (2, 3, 1)]
```

```python
from itertools import permutations
result = permutations([1, 3, 2], 1)
print(list(result))
#결과: [(1,), (3,), (2,)]
```

```python
from itertools import permutations
result = permutations([1, 3, 2], 2)
print(list(result))
#결과: [(1, 3), (1, 2), (3, 1), (3, 2), (2, 1), (2, 3)]
```

```python
from itertools import permutations
result = permutations([1, 3, 2], 4)
print(list(result))
#결과: []
```



## combinations - 조합

combinations(배열, 선택 개수)

```python
from itertools import combinations
result = combinations([1, 3, 2], 1)
print(list(result))
#결과: [(1,), (3,), (2,)]
```

```python
from itertools import combinations
result = combinations([1, 3, 2], 2)
print(list(result))
#결과: [(1, 3), (1, 2), (3, 2)]
```

```python
from itertools import combinations
result = combinations([1, 3, 2], 3)
print(list(result))
#결과: [(1, 3, 2)]
```

```python
from itertools import combinations
result = combinations([1, 3, 2], 4)
print(list(result))
#결과: []
```





## combinations_with_replacement - 중복 조합

combinations_with_replacement(배열, 선택 개수)

```python
from itertools import combinations_with_replacement
result = combinations_with_replacement([1, 3, 2], 1)
print(list(result))
#결과: [(1,), (3,), (2,)]
```

```python
from itertools import combinations_with_replacement
result = combinations_with_replacement([1, 3, 2], 2)
print(list(result))
#결과: [(1, 1), (1, 3), (1, 2), (3, 3), (3, 2), (2, 2)]
```

```python
from itertools import combinations_with_replacement
result = combinations_with_replacement([1, 3, 2], 3)
print(list(result))
#결과: [(1, 1, 1), (1, 1, 3), (1, 1, 2), (1, 3, 3), (1, 3, 2), (1, 2, 2), (3, 3, 3), (3, 3, 2), (3, 2, 2), (2, 2, 2)]
```

```python
from itertools import combinations_with_replacement
result = combinations_with_replacement([1, 3, 2], 4)
print(list(result))
#결과: [(1, 1, 1, 1), (1, 1, 1, 3), (1, 1, 1, 2), (1, 1, 3, 3), (1, 1, 3, 2), (1, 1, 2, 2), (1, 3, 3, 3), (1, 3, 3, 2), (1, 3, 2, 2), (1, 2, 2, 2), (3, 3, 3, 3), (3, 3, 3, 2), (3, 3, 2, 2), (3, 2, 2, 2), (2, 2, 2, 2)]
```



[참고: itertools - 효율적인 루핑을 위한 이터레이터를 만드는 함수](https://docs.python.org/ko/3.8/library/itertools.html)