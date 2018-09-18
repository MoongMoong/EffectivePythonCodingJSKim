# for와 while 루프 뒤에는 else 블록을 쓰지 말자

파이썬 루프는 루프 블록 바로 다음에 else블록을 둘 수 있는 기능이 있다.
```
for i in range(3):
    print('Loop %d' % i)
else:
    print('Else block!')
>>>
Loop 0
Loop 1
Loop 2
Else block!
```
*else 문은 앞의 문법에 따라서 다양한 의미로 실행될 수 있다.
    - if/else문의 else는 이전 블록이 실행되지 않을 때 실행한다.
    - try/except문에서 except의 except는 이전 블록에서 실패하면 실행된다.
    - try/except/else 의 else은 이전 블록이 실패하지 않으면 실행한다.
    - try/finally의 finally는 이전 블록을 실행하고 마지막에 실행한다.
    - for/else 이전 블록이 모두 완료되면 이 블록을 실행한다.(break 문으로 탈출 가능)

```
for i in range(3):
    print('Loop %d' % i)
    if i==1:
        break
else:
    print('Else block!')
>>>
Loop 0
Loop 1
```
for/else 혹은 while/else문의 else는 finally와 같이 앞의 루프가 한번도 실행되지 않는 경우에도 반드시 실행된다.	
다음은 for/else문이 유용할수도 있지만... 다음 예제를 보자. 두 수가 서로소인지 판별하는 코드이다


```
a = 4
b = 9
for i in range(2, min(a,b) +1):
    print('Testing', i)
    if a % i == 0 and b % i == 0:
        print('Not coprime')
        break
else :
    print('Coprime')
>>>

```
*이런 경우 쓸 수도 있지만.. 한번 쓸게 아닌 이상 헬퍼함수를 작성하는 것이 타당하다.

```
def coprime(a,b):
    for i in range(2, min(a,b) +1):
        if a % i == 0 and b % i == 0:
            return False
    return True
```

