## range보다는 enumerate를 사용하자
* 내장함수 range는 정수 집합의 list를 생성하는 함수로 주로 for문을 작동시킬 때 유용하다.

```
random_bits = 0
for i in range(64):
    If randint(0,1):
        random_bits |= 1 << i # 이부분의 | 이게아니라 다른 특수문자인데 무엇을 말하는지 잘 모르겠습니다.
```
참고로 문자열 리스트를 for 루프에 직접 사용할 수 있다.
```
flavor_list = ['vanilla', 'chocolate', 'pecan', 'strawberry']
for flavor in flavor_list:
    print('%s is delicious' %flavor)
```
직접적으로 문자열 리스트를 사용할 수 있지만 인덱스를 사용하고자 하는 경우 아래와 같이 사용할 수 있다.
```
for i in range(len(flavor_list)):
    flavor = flavor_list[i]
    print('%d : %s'  % (i+1, flavor))
```
위의 코드는 리스트의 길이를 알아내고 인덱스로 접근하는 등 깔끔하지 못한데 내장 함수 enumerate를 사용하는 것으로 이를 해결할 수 있다. enumerate는 인덱스와 값을 한쌍으로 가져오는 함수이다. 세기 시작하는 숫자를 지정할 수도 있다.

```
for i, flavor in enumerate(flavor_list, 2):
    print('%d : %s' % (i + 1, flavor))
```
