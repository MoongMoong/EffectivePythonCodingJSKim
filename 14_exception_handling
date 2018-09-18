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
