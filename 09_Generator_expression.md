## 컴프리헨션이 클 때는 제너레이터 표현식을 고려하자

컴프리헨션은 입력 시퀀스에 대한 데이터를 일괄 생성하기 때문에 많은 양의 데이터가 입력되는 경우 메모리를 많이 소모하는 문제가 발생할 수 있다.

* 다음은 파일을 읽어서 각 줄에 있는 문자의 개수를 파악하는 예제이다

```
value = [len(x) for x in open('/tmp/my_file.txt')]
print(value)
>>>
[100, 57, 15,1 12, 75, 5, 86, 89, 11]
```
파이썬은 메모리의 과도한 소모를 막기 위하여 리스트 컴프리헨션과 제너레이터를 일반화 한 제너레이터 표현식(generator expression)을 제공한다.  제너레이터는 한번에 데이터를 생성하는게 아니라 순서대로 아이템을 내어줄 수 있는 이터레이터(iterator)를 반환한다.
**제너레이터 표현식은 () 문자 사이에 리스트 컴프리헨션과 비슷한 문법**으로 생성한다.


```
it = (len(x) for x in open('/tmp/my_file.txt'))
print(it)
>>>
<generator object <genexpr> at 0x101b81480>
```

* 필요할 때 제너레이터 표현식에서 다음 출력을 생성하려면 내장 함수 **next**로 데이터를 추출할 수 있다.

```
print(next(it))
print(next(it))
>>>
100
57
```

제너레이터 표현식의 특징중 하나로 **한 제너레이터 표현식의 결과를 다른 제너레이터 표현식의 입력으로 사용**할 수 있다. 루프의 **도미노 효과**로 내부 이터레이터의 전진과 함께 결과를 출력하는 원리이다.

```
roots = ((x, x**0.5) for x in it)
print(next(roots))
>>>
(15, 3.8.8729383346207417)
```
