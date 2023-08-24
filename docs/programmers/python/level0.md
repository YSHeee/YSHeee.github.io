## 2023.08.24

### 대소문자 바꿔서 출력하기 
영어 알파벳으로 이루어진 문자열 str이 주어집니다. <br>
각 알파벳을 대문자는 소문자로 소문자는 대문자로 변환해서 출력하는 코드를 작성해 보세요.

=== "My code 1"
    ``` python 
    str = input()

    for ch in str:
        if ord(ch) < 97 :
            print(chr(ord(ch)+32), end="")
        else:
            print(chr(ord(ch)-32), end="")
    ``` 
=== "My code 2"
    ``` python 
    print(''.join(chr(ord(ch)+32) if ord(ch)<97 else chr(ord(ch)-32) for ch in input()))
    ``` 
=== "Others"
    ``` python 
    print(input().swapcase())

    print(''.join(x.upper() if x == x.lower() else x.lower() for x in input()))
    ``` 