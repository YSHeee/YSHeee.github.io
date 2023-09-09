# String (문자열)
``` python
S = "Hello, world!"
```

### 문자열 변경
- replace("바꿀 문자열", "새 문자열") : 문자열 안의 해당 문자열을 다른 문자열로 변경 (문자열 자체는 변경하지 않고, 바뀐 결과만 반환)
``` python
S = S.replace('world!', 'Python') # S = "Hello, Python"
```

### 문자 바꾸기
- str.maketrans(’바꿀 문자’, ‘새 문자’) : 변환 테이블 생성
- translate(테이블) : 문자를 테이블 따라 바꾼 뒤 결과 반환
``` python
table = str.maketrans('aeiou', '12345')
'apple'.translate(table) # '1ppl2'
```

### 문자열 분리
- split(’기준문자열’) : () 속 문자 기준으로 문자열을 분리하여 리스트로 변환
``` python
'apple pear grape'.split()  # ['apple', 'pear', 'grape']
```

### JOIN 문자열 리스트 연결
- join(리스트) : 구분자 문자와 문자열 리스트의 요소를 연결하여 문자열로 변환
``` python
' '.join(['apple', 'pear', 'grape'])  # 'apple pear grape'
'-'.join(['apple', 'pear', 'grape'])  # 'apple-pear-grape'
```

### 대문자/소문자로 바꾸기
- upper()
- lower()
``` python
'python'.upper() # 'PYTHON'
'PYTHON'.lower() # 'python'
```

### 공백 삭제
- strip() : 양쪽 공백 삭제
- rstrip() :  오른쪽 공백 삭제
- lstrip() :  왼쪽 공백 삭제
``` python
'   Python   '.lstrip()  # 'Python    '
'   Python   '.rstrip()  # '    Python'
'   Python   '.strip()   # 'Python'
', Python.'.strip(',.')  # ' Python' 특정 문자 삭제
```
- string 모듈의 punctuation
``` python
import string
string.punctuation  # '!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'
', python.'.strip(string.punctuation)  # ' python'
', python.'.strip(string.punctuation + ' ')  # 'python' 공백도 삭제
```
- 메서드 체이닝 : 메서드가 객체를 반환하면, 메서드의 반환 값인 객체를 통해 또 다른 함수를 호출하는 프로그래밍 패턴 (=메소드를 계속 연결해서 호출)
``` python
', python.'.strip(string.punctuation).strip()  # 'python'
```

### 문자열 정렬
- ljust(길이) : 문자열을 지정된 길이로 만든 뒤, 왼쪽으로 정렬하고, 남는 공간을 공백으로 채움
- rjust(길이) : 문자열을 지정된 길이로 만든 뒤, 오른쪽으로 정렬하고, 남는 공간을 공백으로 채움
- center(길이) : 문자열을 지정된 길이로 만든 뒤, 가운데로 정렬하고, 남는 공간을 공백으로 채움
``` python
'python'.ljust(10)  # 'python  - 총 10칸에 우측 공백 4칸
'python'.rjust(10)  # '    python'  - 총 10칸에 좌측 공백 4칸
'python'.center(10)  # '  python  '  - 총 10칸에 양쪽 공백 2칸씩
```

### 문자열 왼쪽에 0 채우기
- zfill(길이) : 지정된 길이에 맞춰서, 문자열의 왼쪽에 0을 채움
``` python
'35'.zfill(4)  # '0035'
'3.5'.zfill(6)  # '0003.5'
```

### 문자열 위치 찾기
- find(’찾을 문자열’) : 왼쪽부터 특정 문자열을 찾아 인덱스를 반환하고, 없으면 -1 반환
- rfind(’찾을 문자열’) : 오른쪽부터 특정 문자열을 찾아 인덱스 반환, 없으면 -1 반환
- index(’찾을 문자열’) : 왼쪽부터 특정 문자열을 찾아 인덱스 반환, 없으면 에러 
- rindex(’찾을 문자열’) : 오른쪽부터 특정 문자열을 찾아 인덱스 반환, 없으면 에러
``` python
'apple pineapple'.find('pl') # 2
'apple pineapple'.rfind('pl') # 12

'apple pineapple'.index('pl')  #2
'apple pineapple'.rindex('pl')  #12
```

### 문자열 개수 세기
- count(’문자열’) : 현재 문자열에서 특정 문자열이 몇 번 나오는지 
``` python
'apple pineapple'.count('pi')  # 1
```

### 서식지정자
- %.자릿수f % 숫자
``` python
'%.2f' % 2.3  # 2.30
'%f' % 2.3  # 2.300000
```
- ‘%10s’ % ‘python : 문자열을 지정된 길이로 만든 뒤, 오른쪽으로 정렬, 남는 공간은 공백
``` python
'%10s' % 'python'  # '    python' 오른쪽 정렬
'%-10s' % 'python'  # 'python    ' 왼쪽 정렬
```

### format 메서드
- ‘{인덱스}’.format(값)
``` python
‘{인덱스}’.format(값)
```
- 이름 지정
``` python
'Hello, {language} {version}'.format(lanugage='Python', version=3.6)
```
- Formatting
``` python
language = 'Python'
version = 3.6
f'Hello, {{language}} {version}' # 'Hello, {Python} 3.6'
```
- '{인덱스:<길이}'.format(값) : 문자열 정렬
``` python
'{0:<10}'.format('python')  # 'python    ' < 이므로 왼쪽으로 정렬, 남는 공간 공백
```
- '%0개수d' % 숫자
- '{인덱스:0개수d'}'.format(숫자)
``` python
'%03d' % 1  # '001'
'{0:08.2f}'.format(150.37)  # '00150.37'
```
- '{ 인덱스 : [ [채우기] [정렬] [길이] [.자릿수] [자료형] }'
``` python
# 0번째 인덱스, 길이 10, 오른쪽으로 정렬, 남는 공간 x로 채움 
'{0:x>10}'.format(15)  #'xxxxxxxx15'
# 0번째 인덱스, 길이 10, 오른쪽 정렬, 소수점 두 자리
'{0:0>10.2f}'.format(15)  # '0000015.00'
```
- format(숫자, ‘,’) : 천 단위로 콤마 넣기
``` python
format(1493500, ',')  # '1,493,500'
```

### 서식지정자 Table
|    자료형    |    설명   | 
| :-----------: | :-----------: |
s |	문자열
b |	2진수
c |	문자
d |	10진 정수
o |	8진 정수, 예) '%o' % 8은 '10’
x |	16진 정수, 0~9, a~f, 예) '%x' % 254는 'fe’
X |	16진 정수, 0~9, A~F, 예) '%X' % 254는 'FE’
e |	실수 지수 표기법, 예) '%e' % 2.3은 '2.300000e+00’
E |	실수 지수 표기법, 예) '%E' % 2.3은 '2.300000E+00’
f |	실수 소수점 표기
F |	실수 소수점 표기, f와 같음, nan은 NAN, inf는 INF로 표시<br>(nan은 숫자가 아니라는 뜻, inf는 무한대)
g |	실수 일반 형식, 예) '%g' % 2.3e-10은 '2.3e-10’
G |	실수 일반 형식, 예) '%G' % 2.3e-10은 '2.3E-10’
% |	% 문자 표시