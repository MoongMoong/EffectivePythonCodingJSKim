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
# try/except/else/finally에서 각 블록의 장점을 이용하자
파이썬은 try, except, else, finally 블록 기능으로 예외처리 과정에서 총 네번의 동작시점을 처리할 수 있다.
 finally 블록
예외를 전달하고 싶고, 예외가 발생해도 정리 코드를 실행하려 할 때 try/finally를 사용한다.
파일 핸들러를 제대로 종료하기 위해서 사용하면 좋다.
```
handle = open('/tmp/random_data.txt')
try :
    data = handle.read()
finally :
    handle.close()

```
2. else 블록
코드에서 예외를 처리하고 어떤 예외를 전달할지를 명확히 하기 위해서 try/except/else를 사용한다.
try블록이 예외를 일으키지 않으면 else블록이 실행된다.

```
def load_json_key(data, key):
    try :
        result_dict = json.loads(data)
    except ValueError as e:
        raise KeyError from e # raise 는 강제 에러함수로 해당 에러 문구를 표출하면서 에러 표시를 한다
    else :
        return result_dict[key]
```
다음은 네가지를 모두 활용하는 예문이다. 

```
UNDEFINED = object()

def divide_json(path):
    handle = open(path,'r+') # IOError 발생 가능
    try :
        data = handle.read() #UnicodeDecoderError 발생 가능
        op = json.loads(data) #Value Error 발생 가능
        value = (
            op['numerator']/
            op['denominator']) # ZeroDivisionError 발생 가능
    except ZeroDivisionError as e:
        return value
    finally :
        handle.close()

```
