---
comments: true
---
# MSA-3기 코테 소그룹 공간 😃

![1](../images/jython_1.png){:style width=50%;height=50%}

---

### [23.09.06 Level0] 181943 문자열 겹쳐쓰기 [note](../../language/java/note/1.md)
문자열 my_string, overwrite_string과 정수 s가 주어집니다. 문자열 my_string의 인덱스 s부터 overwrite_string의 길이만큼을 문자열 overwrite_string으로 바꾼 문자열을 return 하는 solution 함수를 작성해 주세요.

| my_string | overwrite_string |    s   |  result
| :-------: | :--------------: | :----: | :-----:
|"He11oWor1d" | "lloWorl" | 2 | "HelloWorld" |
|"Program29b8UYP" | "merS123" | 7 | "ProgrammerS123" |

=== "java"
    ``` java
    class Solution {
        public String solution(String my_string, String overwrite_string, int s) {
            return my_string.substring(0,s) + overwrite_string + my_string.substring(overwrite_string.length()+s);
        }
    }
    ```
=== "java_Others"
    ``` java
    class Solution {
        public String solution(String my_string, String overwrite_string, int s) {
            String answer = "";
            StringBuffer sb = new StringBuffer(my_string);
            sb.replace(s, s+overwrite_string.length(), overwrite_string);
            answer = sb.toString();
            return answer;
        }
    }
    ```
=== "python"
    ``` python
    # replace 쓰려다가 index를 기준으로 분리하는 데에 쓰는 건 아니라는 것을 깨달았다..
    # 함수의 기능을 잘 생각해보고 쓰자 
    def solution(my_string, overwrite_string, s):
        return my_string[0:s] + overwrite_string + my_string[s+len(overwrite_string):]
    ```

---

### [23.09.07 Level0] 181936 공배수 [note](../../language/java/note/1.md)
정수 number와 n, m이 주어집니다. number가 n의 배수이면서 m의 배수이면 1을 아니라면 0을 return하도록 solution 함수를 완성해주세요.
=== "java"
    ``` java
    class Solution {
        public int solution(int number, int n, int m) {
            return (number%n==0 && number%m==0) ? 1 : 0;
        }
    }
    ```
=== "python"
    ``` python
    solution = lambda number,n,m: int(not(number%n | number%m))
    ```

---