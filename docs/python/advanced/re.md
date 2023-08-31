# Regular Expression
일정한 규칙을 가진 문자열을 표현하는 방법

- 복잡한 문자열 속에서 특정한 규칙으로 된 문자열을 검색한 뒤, 추출하거나 바꿀 때 사용
- 문자열이 정해진 규칙에 맞는지 판단할 때 사용

### 문자열 판단하기
- re.match(’패턴’, ‘문자열’)
```python
import re

re.match('Hello', 'Hello, world!') # <re.Match object; span=(0, 5), match='Hello'>
re.match('Hello', 'world!') # 반환되지 않음
```

### 문자열이 맨 앞 또는 맨 뒤에 오는 지 판단하기
- ^문자열
- 문자열$
```python
re.search('^Hello', 'Hello, world!') #<re.Match object; span=(0, 5), match='Hello'> 
re.search('^[A-Z]+', 'Hello') # <_sre.SRE_Match object; span=(0, 1), match='H'> # 대문자로 시작하므로 패턴에 매칭됨

re.search('world!$', 'Hello, world!') #<re.Match object; span=(7, 13), match='world!'> 
re.search('[0-9]+$', 'Hello1234') #<_sre.SRE_Match object; span=(5, 9), match='1234'> # 숫자로 끝나므로 패턴에 매칭됨
```

### 지정된 문자열이 하나라도 포함되는지 판단하기
- 문자열|문자열
- 문자열|문자열|문자열|문자열
```python
re.match('hello|world', 'hello') # <re.Match object; span=(0, 5), match='hello'> # hello 또는 world가 있으므로 패턴에 매칭됨
```

### 문자가 0~1개 이상 있는지 판단
- [0-9]*
- [0-9]+
: [ ] 대괄호 안에 숫자 범위 삽입
: *는 문자 또는 숫자가 0개 이상 있는지 확인
: +는 1개 이상 있는지 확인
``` python
# 1234는 0부터 9까지 숫자가 0개 이상 있으므로 패턴에 매칭됨
re.match('[0-9]*', '1234') # <re.Match object; span=(0, 4), match='1234'>

# 1234는 0부터 9까지 숫자가 1개 이상 있으므로 패턴에 매칭됨
re.match('[0-9]+', '1234') # <re.Match object; span=(0, 4), match='1234'>

re.match('[0-9]+', 'abcd') # abcd는 0~9까지 숫자가 1개 이상 없으므로 패턴에 매칭되지 않음
```

### 문자가 한 개만 있는지 판단
- 문자?
- [0-9]?
- .
: ?는 앞의 문자가 0개 또는 1개인지 판단
: .은 .이 있는 위치에 아무 문자가 1개 있는지 판단
```python
# abd에서 c 위치에 c가 0개 있으므로 패턴에 매칭됨
re.match('abc?d', 'abd') # <re.Match object; span=(0, 3), match='abd'>

# abd에서 c 위치에 c가 1개 있으므로 패턴에 매칭 안됨
re.match('abc?d', 'abc')

# [0-9] 위치에 숫자가 1개 있으므로 패턴에 매칭됨
re.match('ab[0-9]?c', 'ab3c') # <re.Match object; span=(0, 4), match='ab3c'>

# .이 있는 위치에 문자가 1개 있으므로 패턴에 매칭됨
re.match('ab.d', 'abxd') # <_sre.SRE_Match object; span=(0, 4), match='abxd'>
```

### 문자 개수 판단하기
- 문자{개수}
- (문자열){개수}

