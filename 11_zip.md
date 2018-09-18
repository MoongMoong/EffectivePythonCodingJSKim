## 이터레이터를 병렬로 처리하려면 zip을 사용하자
파이썬은 객체로 구성된 리스트를 많이 사용하는 특징이 있다. 
특히 리스트 컴프리헨셔늘 사용하여 소스 리스트(source list)를 활용하여 파생 리스트(derived list)를 쉽게 만들 수 있다.
소스 리스트와 파생 리스트는 인덱스로 연관되어 있는데 순회 리스트의 길이만큼 순회하는 것으로 두 리스트에 모두 접근할 수도 있다.

```
name = ['Cecilia', 'Lise', 'Marie']
letters = [len(n) for n in name]
lengest_name = None
max_letters = 0
for i in range(len(name)):
    count = letters[i]
    If count > max_letters:
        longest_name = names[i]
        max_letters = count
print(longest_name)
>>>
Cecilia
```
이제는 인덱스로 데이트에 접금하는 것이 보기에 좋지 않다는 것을 이해해야 한다.
enumerate함수로 1차적인 개선을 해보자

```
for i, name in enumerate(names):
    count = letters[i]
    if count> max_letters:
        longest_name = name
        max_letters = count
```
지연 제너레이터 zip을 활용하여 2개 이상의 이터레이터를 합하여 튜플을 반환하는 이터레이터를 만들 수 있는데 이것을 활용하여 깔끔하게 만들 수 있다.

```
for name, count in zip(names, letters):
    If count > mex_letters:
        longest_name = name
        max_letters = count
>>>

``` 
*zip은 편리하지만 두가지 문제를 갖고 있다
    - 파이썬 2에서 제공하는 zip이 제너레이터가 아니라서 큰 이터레이터를 입력하는 경우 프로그램이 망가질 수 있다. 내장모듈 itertoos의 izip을 사용하는 것으로 이를 방지할 수 있다.
    - 이터레이터들의 길이가 다르면 zip이 이상하게 동작할 수 있다. 길이가 다를 가능성이 있을 때 itertools의 zip_longest(izip_longest for python2)를 사용하는 방안을 고려해보자
