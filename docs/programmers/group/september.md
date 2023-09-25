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
=== "java Others"
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

### [23.09.11 Level0] 주사위 게임 2 
1부터 6까지 숫자가 적힌 주사위가 세 개 있습니다. 
<br>세 주사위를 굴렸을 때 나온 숫자를 각각 a, b, c라고 했을 때 얻는 점수는 다음과 같습니다.

1. 세 숫자가 모두 다르다면 a + b + c 점을 얻습니다.
2. 세 숫자 중 어느 두 숫자는 같고 나머지 다른 숫자는 다르다면 (a + b + c) × (a2 + b2 + c2 )점을 얻습니다.
3. 세 숫자가 모두 같다면 (a + b + c) × (a2 + b2 + c2 ) × (a3 + b3 + c3 )점을 얻습니다.

세 정수 a, b, c가 매개변수로 주어질 때, 얻는 점수를 return 하는 solution 함수를 작성해 주세요.

=== "java"
    ``` java
    import java.util.HashSet;
    class Solution {
        public int solution(int a, int b, int c) {
            HashSet<Integer> numList = new HashSet<>();
            numList.add(a);
            numList.add(b);
            numList.add(c);
            
            int stNum = 4;
            int answer = 1;
            
            for (int i=stNum-numList.size(); i>0; i--)
                answer *= Math.pow(a,i)+Math.pow(b,i)+Math.pow(c,i);
            
            return answer;
        }
    }
    ```
=== "python"
    ``` python
    def solution(a, b, c):
        check = len({a,b,c})
        result = 1
        for num in range(4-check):
            result *= a**(num+1)+b**(num+1)+c**(num+1)
        return result
    ```

---
### [23.09.12 Level0] 옹알이 (1)
머쓱이는 태어난 지 6개월 된 조카를 돌보고 있습니다. 조카는 아직 "aya", "ye", "woo", "ma" 네 가지 발음을 최대 한 번씩 사용해 조합한(이어 붙인) 발음밖에 하지 못합니다. 문자열 배열 babbling이 매개변수로 주어질 때, 머쓱이의 조카가 발음할 수 있는 단어의 개수를 return하도록 solution 함수를 완성해주세요.

- babbling의 각 문자열에서 "aya", "ye", "woo", "ma"는 각각 최대 한 번씩만 등장합니다.
- 문자열은 알파벳 소문자로만 이루어져 있습니다.

=== "java"
    ``` java
    class Solution {
        public int solution(String[] babbling) {
            int count = 0;
            for (String word:babbling) {
                if (word.matches("(aya|ye|woo|ma)+"))
                    count ++;
            }
            return count;
        }
    }
    ```
=== "python"
    ``` python
    import re
    def solution(babbling):
        pattern = re.compile("aya|ye|woo|ma")
        count = 0
        for word in babbling:
            if re.sub(pattern, '', word) == '':
                count += 1
        return count
    ```


---
### [23.09.13 Level1] 정수 제곱근 판별
임의의 양의 정수 n에 대해, n이 어떤 양의 정수 x의 제곱인지 아닌지 판단하려 합니다.
n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 양의 정수 x의 제곱이 아니라면 -1을 리턴하는 함수를 완성하세요.

=== "java"
    ``` java
    class Solution {
        public long solution(long n) {
            double x = Math.sqrt(n);
            return x%1==0 ? (long)(Math.pow(x+1,2)) : -1 ;
        }
    }
    ```
=== "python"
    ``` python
    def solution(n):
        num = n**0.5
        return (num+1)**2 if num%1==0 else -1
    ```

---
### [23.09.14 Level1] 하샤드 수
양의 정수 x가 하샤드 수이려면 x의 자릿수의 합으로 x가 나누어져야 합니다. 예를 들어 18의 자릿수 합은 1+8=9이고, 18은 9로 나누어 떨어지므로 18은 하샤드 수입니다. 자연수 x를 입력받아 x가 하샤드 수인지 아닌지 검사하는 함수, solution을 완성해주세요.

=== "My code"
    ``` java
    class Solution {
        public boolean solution(int x) {
            int numSum = 0;
            String numStr = Integer.toString(x);
            
            for (int i=0; i<numStr.length(); i++)
                numSum += Character.getNumericValue(numStr.charAt(i));
            
            return x % numSum == 0;
        }
    }
    ```
=== "Others"
    ``` java 
    // 내 코드가 약 3-4배 정도 더 빠르다 왜지
    class Solution {
        public boolean solution(int x) {
            int numSum = 0;
            String [] tmp = String.valueOf(x).split("");
            
            for (String ch:tmp)
                numSum += Integer.parseInt(ch);
    
            return x%numSum==0;
        }
    }
    ``` 

---
### [23.09.15 Level1] 수박수박수박수박수박수?
길이가 n이고, "수박수박수박수...."와 같은 패턴을 유지하는 문자열을 리턴하는 함수, solution을 완성하세요. 예를들어 n이 4이면 "수박수박"을 리턴하고 3이라면 "수박수"를 리턴하면 됩니다.

=== "java"
    ``` java
    import java.util.ArrayList;
    class Solution {
        public String solution(int n) {
            ArrayList<String> tmp = new ArrayList<>();
            for (int i=1; i<=n; i++){
                tmp.add(i%2==0 ? "박" : "수");
            }
            String str = String.join("", tmp);
            return str;
        }
    }
    ```
=== "python"
    ``` python
    def solution(n):
        answer = ["박" if i%2==0 else "수" for i in range(1, n+1)]
        return ''.join(answer)
    ```
=== "python Others"
    ``` python
    def solution(n):
        return "".join(["수박"[i%2] for i in range(n)])
    ```

---
### [9월 2주차 Level1] 기사단원의 무기
기사단원의 수를 나타내는 정수 number와 이웃나라와 협약으로 정해진 공격력의 제한수치를 나타내는 정수 limit와 제한수치를 초과한 기사가 사용할 무기의 공격력을 나타내는 정수 power가 주어졌을 때, 무기점의 주인이 무기를 모두 만들기 위해 필요한 철의 무게를 return 하는 solution 함수를 완성하시오.
=== "java"
    ``` java
    class Solution {
        public int solution(int number, int limit, int power) {
            int answer = 1;
            int num;
            double square_root;

            for (int knight=2; knight <= number; knight++){
                num = 0;
                square_root = Math.sqrt(knight);
                for (int weapon=1; weapon <= (int)square_root; weapon++){
                    if (knight % weapon == 0)
                        num += 2;
                }
                if (square_root % 1 == 0)
                    num--;
                
                if (num > limit)
                    num = power;
                
                answer += num;
                
            }
            return answer;
        }
    }
    ```
=== "python"
    ``` python
    def solution(number, limit, power):
        result = 0
        for knight in range(2, number+1):
            num = 0
            square_root = knight**0.5 
            
            for weapon in range(1, int(square_root)+1):
                if knight % weapon == 0:
                    num+=2
                    
            if square_root % 1 == 0:
                num -= 1
                
            if num > limit:
                num = power
                
            result += num
        return result + 1
    ```

---
### [23.09.18 Level1] 신고 결과 받기
이용자의 ID가 담긴 문자열 배열 id_list, 각 이용자가 신고한 이용자의 ID 정보가 담긴 문자열 배열 report, 정지 기준이 되는 신고 횟수 k가 매개변수로 주어질 때, 각 유저별로 처리 결과 메일을 받은 횟수를 배열에 담아 return 하도록 solution 함수를 완성해주세요.
=== "Java"
    ``` java

    ```
=== "Python"
    ``` python
    from collections import Counter
    def solution(id_list, report, k):
        count_table = {key:0 for key in id_list}
        name_table = {key:[] for key in id_list}
        
        for val in set(report):
            id = val.split(" ")
            count_table[id[1]] += 1
            name_table[id[0]].append(id[1])
            
        reports = {key for key,val in count_table.items() if val>=k}

        return [len(set(val)&reports) for val in name_table.values()]
    ```

---
### [23.09.19 Level0] 겹치는 선분의 길이
선분 3개가 평행하게 놓여 있습니다. 세 선분의 시작과 끝 좌표가 [[start, end], [start, end], [start, end]] 형태로 들어있는 2차원 배열 lines가 매개변수로 주어질 때, 두 개 이상의 선분이 겹치는 부분의 길이를 return 하도록 solution 함수를 완성해보세요.

=== "Java"
    ``` python
    class Solution {
        public int solution(int[][] lines) {
            int[] table = new int[201];
            int count = 0;
            
            for (int[] line: lines)
                for (int c=line[0]; c<line[1]; c++)
                    table[c+100] += 1;

            for (int cnt: table){
                if (cnt > 1)
                    count += 1;
        }     
            return count;
        }
    }
    ```
=== "Python"
    ``` python
    from collections import Counter
    def solution(lines):
        tmp = []
        for line in lines:
            tmp.extend([(i, i+1) for i in range(line[0], line[1])])
        return len([1 for i in Counter(tmp).values() if i>1])
    ```
=== "Python-JSH"
    ``` python
    def solution(lines):
        cnt_list = [0] * 200
        for line in lines:
            for i in range(line[0], line[1]):
                cnt_list[i+100] += 1
        over_one = [cnt for cnt in cnt_list if cnt > 1]
        return len(over_one)
    ```

---
### [23.09.20 Level0] 연속된 수의 합
연속된 세 개의 정수를 더해 12가 되는 경우는 3, 4, 5입니다. 두 정수 num과 total이 주어집니다. 연속된 수 num개를 더한 값이 total이 될 때, 정수 배열을 오름차순으로 담아 return하도록 solution함수를 완성해보세요.

=== "Python"
    ``` python
    def solution(num, total):
        quot = total // num 
        result = [i for i in range(quot-num-1, quot+num+1)]
        for i in range(len(result)-num):
            if sum(result[i:i+num]) == total:
                return result[i:i+num]
    ```

---
### [23.09.21 Level1] 크레인 인형뽑기 게임

=== "Python"
    ``` python
    def solution(board, moves):
        count=0
        basket=[-2, -1] # fake value
        
        for idx in moves:
            for row in range(len(board)):
                doll = board[row][idx-1]
                if doll != 0:
                    basket.append(doll)
                    board[row][idx-1] = 0
                    break
            if basket[-2] == basket[-1]:
                count += 2
                del basket[-2:]
        return count
    ```

---
### [23.09.22 Level1] 핸드폰 번호 가리기
프로그래머스 모바일은 개인정보 보호를 위해 고지서를 보낼 때 고객들의 전화번호의 일부를 가립니다.
전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 *으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.

=== "Java"
    ``` java
    class Solution {
        public String solution(String phone_number) {
            String change_str = phone_number.substring(0, phone_number.length()-4);
            change_str = change_str.replaceAll("[0-9+]", "*");
            String answer = change_str + phone_number.substring(phone_number.length()-4);
            return answer;
        }
    }
    ```
=== "Java Others"
    ``` java
    class Solution {
        public String solution(String phone_number) {
            return phone_number.replaceAll(".(?=.{4})", "*");
        }
    }
    ```
=== "Python"
    ``` python
    def solution(phone_number):
        change_str = phone_number[:-4]
        phone_number = phone_number.replace(change_str, "*"*len(change_str))
        return phone_number
    ```
=== "Python Others"
    ``` python
    def solution(phone_number):
        return "*"*(len(phone_number)-4) + phone_number[-4:]
    ```




---
### [9월 3주차 Level1] 숫자 문자열과 영단어
네오와 프로도가 숫자놀이를 하고 있습니다. 네오가 프로도에게 숫자를 건넬 때 일부 자릿수를 영단어로 바꾼 카드를 건네주면 프로도는 원래 숫자를 찾는 게임입니다.
숫자의 일부 자릿수가 영단어로 바뀌어졌거나, 혹은 바뀌지 않고 그대로인 문자열 s가 매개변수로 주어집니다. s가 의미하는 원래 숫자를 return 하도록 solution 함수를 완성해주세요.

=== "Java"
    ``` java
    import java.util.*;
    class Solution {
        public int solution(String s) {
            String result = s;
            Map<String, String> table = Map.of(
                "zero", "0",
                "one", "1",
                "two", "2",
                "three", "3",
                "four", "4",
                "five", "5",
                "six", "6",
                "seven", "7",
                "eight", "8",
                "nine", "9"     
            );
            
            for (String word: table.keySet()){
                result = result.replace(word, table.get(word));
            }
            return Integer.parseInt(result);
        }
    }
    ```
=== "Python"
    ``` python 
    import re
    def solution(s):   
        
        fa = re.findall("zero|one|two|three|four|five|six|seven|eight|nine|[0-9]", s)
        table = {"zero":"0", "one":"1", "two":"2", "three":"3", "four":"4", "five":"5", "six":"6", "seven":"7", "eight":"8", "nine":"9"}
        
        for idx, word in enumerate(fa):
            if word in table:
                fa[idx] = table[word]
                
        return int(''.join(fa))
    ```

---
### [23.09.25 Level0] 다음에 올 숫자
등차수열 혹은 등비수열 common이 매개변수로 주어질 때, 마지막 원소 다음으로 올 숫자를 return 하도록 solution 함수를 완성해보세요.

=== "Java"
    ``` java
    class Solution {
        public int solution(int[] common) {
            int d1 = common[1] - common[0];
            int d2 = common[2] - common[1];
            int leng = common.length;
            return d1==d2 ? common[leng-1]+d1 : common[leng-1]*(d2/d1);
        }
    }
    ```
=== "Python"
    ``` python
    def solution(common):
        d1 = common[1] - common[0]
        d2 = common[2] - common[1]
        return common[-1] + d1 if d1 == d2 else common[-1] * (d2/d1)
    ```
