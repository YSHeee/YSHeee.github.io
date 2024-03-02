해시, 스택/큐, 힙, 정렬, 완전탐색, ...

## 2024.03.01

### 전화번호 목록
전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.
(큰일났다 자바 기억 안난다 ^^!;;)

=== "PYTHON"
    ``` python
    # startswith
    def solution(phone_book):
        phone_book.sort()
        
        for idx in range(len(phone_book)-1):
            number = phone_book[idx]
            if number == phone_book[idx+1][:len(number)]:
                return False
            
        return True
    ```
=== "JAVA"
    ``` java
    import java.util.Arrays;
    class Solution {
        public boolean solution(String[] phone_book) {
            Arrays.sort(phone_book);
            
            for (int i=0; i<phone_book.length-1; i++){
                if (phone_book[i+1].startsWith(phone_book[i])) {
                    return false;
                }
            }
            
            return true;
        }
    }
    ```
=== "OTHERS"
    ``` python
    def solution(phone_book):
        answer = True
        hash_map = {}
        for phone_number in phone_book:
            hash_map[phone_number] = 1
        for phone_number in phone_book:
            temp = ""
            for number in phone_number:
                temp += number
                if temp in hash_map and temp != phone_number:
                    answer = False
        return answer
    ```

### 의상
코니가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.

=== "PYTHON"
    ``` python
    from collections import defaultdict
    def solution(clothes):
        
        list_dict = defaultdict(int)
        for e in clothes:
            list_dict[e[1]] += 1

        result = 1
        for num in list_dict.values():
            result *= num + 1
        
        return result - 1 
    ```
=== "JAVA"
    ``` java
    import java.util.HashMap;
    import java.util.Map;
    class Solution {
        public int solution(String[][] clothes) {
            
            Map<String, Integer> counter = new HashMap<>();
            for (String[] item: clothes){
                if (counter.containsKey(item[1])){
                    counter.put(item[1], counter.get(item[1])+1);
                } else {
                    counter.put(item[1], 1);
                }
            }
            
            int answer = 1;
            for (Integer num: counter.values()){
                answer *= num+1;
            }
            
            return answer-1;
        }
    }
    ```

## 2024.03.01

### 같은 숫자는 싫어
배열 arr에서 연속적으로 나타나는 숫자는 제거하고 남은 수들을 return 하는 solution 함수를 완성해 주세요.

=== "PYTHON"
    ``` python
    def solution(arr):
        result = [arr[0]]
        for num in arr[1:]:
            if result[-1] != num:
                result.append(num)
        return result     
    ```
=== "JAVA"
    ``` java
    import java.util.*;

    public class Solution {
        public ArrayList<Integer> solution(int []arr) {
            ArrayList<Integer> answer = new ArrayList<>();
            
            answer.add(arr[0]);
            for (int i=1; i<arr.length; i++){
                if (answer.get(answer.size()-1) != arr[i]) {
                    answer.add(arr[i]);
                }
            }

            return answer;
        }
    }
    ```