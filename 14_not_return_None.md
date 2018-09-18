
## None을 반환하기보다는 예외를 일으키자
*파이썬 프로그램을 개발할 때 None에 의미를 부여하는 경우가 많다.
```
def divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return None
```
*이 함수를 사용할 때 None은 다음과 같이 해석한다.
```
result = divide(x, y)
if result is None:
    print('Invalid inputs')
```
*제대로 None과 비교하여 평가하면 되지만 False를 검사하는 경우 문제가 발생한다.
```
x, y = 0, 5
result = divide(x, y)
if not result :
    print('Invalid inputs') # 잘못된 결과가 나올 수 있다
```

*이건 꽤 흔히 발생하는 실수이고 이런에러 상황을 줄이는 방법이 두가지 있다.
    - 하나는 작업의 성공과 실패 여부를 알려주는 값과 실제 값 즉 2개의 값을 반환하는 튜플로 구성하는 방법이다.
    - 이 경우 호출할 때도 튜플을 풀어야 하며 상태부분까지 고려하여야 한다.


```
def divide(a, b)
    try :
        return True, a/b
    except ZeroDivisionError:
        return False, None

success, result = divide(x, y)
if not success:
    print('Invalid inputs')
```
* 사용자가 출력에서 _변수를 활용해서 튜플의 첫 부분을 무시하는 경우 그냥 None을 반환한 것과 똑같은 실수가 발생할 수 있다. 
이를 방지하기 위하여 None을 반환하지 않고 호출하는 쪽에 예외를 일으켜서 거기서 처리하게 하는 것이다.

```
def divide(a, b):
    try:
        return a / b
    except ZeroDivisionError as e:
        Raise ValueError('Invalid inputs') from e

```
