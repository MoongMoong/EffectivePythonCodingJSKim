## 리스트를 반환하는 대신 제너레이터를 고려하자
- Sequence를 반환할 때 가장 간편한 방법은 list를 반환하는 것이다.
- 문자열에 포함된 모든 단어의 인덱스를 출력하는 예제를 보자
```
def index_words(text):
    result = []
    if text:
        result.append(0)
    for index, letter in enumerate(text):
        if letter == ' ':
            result.append(index + 1)
    return result

address = 'Four score and seven years ago'
result = index_words(address)
print(result[:3])

>>>
[0, 5, 11]
```
- 샘플 입력이 적을 때는 위와 같이 문제없이 동작하지만 이 코드는 다음과 같은 문제를 갖는다.
    - 코드가 약간 복잡하고 깔끔하지 않다.
      - 새로운 결과가 나올 때 마다 append method를 호출해야한다.
      - result.append의 호출이 많고, list를 생성 및 반환하는데 코드의 비중이 크다.

- 이 문제를 해결하기 위하여 제너레이터(generator)를 사용할 수 있다.
    - yield 표현식을 상요하는 함수
    - 제너레이터 함수는 실제로 실행하지 않고 이터레이터(iterator)를 반환한다.
    - 내장함수 enxt를 호출할 때마다 이터레이터는 제너레이터가 다음 yield 표현식으로 진행하게 한다.
    - 제너레이터는 yield에 전달한 값을 이터레이터가 호출하는 곳으로 반환한다.

- 위의 예제를 제너레이터 함수로 구성해보겠다.
```
def index_words_iter(text):
    if text:
        yield 0
    for index, letter in enumerate(text):
        if letter == ' ':
            yield index + 1
index_words_iter(address)
result_iter = list(index_words_iter(address)) # 내장함수 list에 generator를 입력하면 list로 만들 수 있다.
```

- 리스트와 연동하는 부분이 사라져서 읽기가 쉬워졌다.
- 이터레이터를 next가 아닌 list함수로 list로 변환할 수도 있다.

- list를 출력으로 반환할때는 모든 결과를 리스트에 저장해야만 하는 문제가 있다
    - 이는 자칫 큰 입력이 저장될 때 메모리가 고갈될수 있는 문제가 있다.
    - 제너레이터로 작성한 버전은 다양한 길이의 입력에 적용이 가능하다.

- 다음은 제너레이터를 활용하여 파일에서 한줄 단위로 읽어드린 후 그 줄에서도 한 단어단위로 출력하는 제너레이터이다.
    - 이 함수가 동작할때 사용하는 메모리는 입력된 줄의 최대 길이이다.

```
def index_file(handle):
    offset = 0
    for line in handle:
        if line:
            yidle offset
        for letter in line:
            offset +=1
            if letter == ' ':
                yield offset

with open('/tmp/address.txt', 'r') as f:
    it = index_file(f)
    results = islice(it, 0, 3)
    print(list(results))
    
>>>
[0, 5, 11]
```
- 
