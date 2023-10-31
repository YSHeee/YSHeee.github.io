---
comments: true
---
# MSA-3기 코테 소그룹 공간 😃

### [10월 1주차 Level2] 올바른 괄호

=== "java"
    ``` java
    import java.util.Stack;
    class Solution {
        boolean solution(String s) {
            
            Stack<Character> charStack = new Stack<>();
            
            for (char c : s.toCharArray()){
                if (c == ')' && !charStack.isEmpty()) {
                    charStack.pop();
                } else {
                    charStack.push(c);
                }
            }
            return charStack.isEmpty() ? true : false ;
        }
    }
    ```
=== "python"
    ``` python
    def solution(s):
        result = []
        for bracket in s:
            if (bracket == ')' and result):
                result.pop()
            else:
                result.append(bracket)

        return False if result else True
    ```

---

### [23.10.30 Level0] 배열 만들기 2
정수 l과 r이 주어졌을 때, l 이상 r이하의 정수 중에서 숫자 "0"과 "5"로만 이루어진 모든 정수를 오름차순으로 저장한 배열을 return 하는 solution 함수를 완성해 주세요. 만약 그러한 정수가 없다면, -1이 담긴 배열을 return 합니다.

=== "python"
    ``` python
    def solution(l, r):
        result = []
        for i in range(1, 64): # 2진수 1~111111
            num = 5 * int(bin(i)[2:])
            if num > r:
                break
            if num >= l and num <= r:
                result.append(num)
        return result if result else [-1]
    ```
=== "java ArrayList"
    ``` java
    import java.util.ArrayList;
    class Solution {
        public ArrayList<Integer> solution(int l, int r) {
            ArrayList<Integer> answer = new ArrayList<>();
            int num;
            for (int i=1; i<64; i++){
                num = 5 * Integer.parseInt(Integer.toBinaryString(i));
                if (num >= l && num <= r)
                    answer.add(num);
                if (num > r)
                    break;
            }
            if (answer.size() == 0)
                answer.add(-1);
            
            return answer;
        }
    }
    ```
=== "java int[]"
    ``` java
    import java.util.ArrayList;
    class Solution {
        public int[] solution(int l, int r) {
            ArrayList<Integer> answer = new ArrayList<>();
            int num;
            for (int i=1; i<64; i++){
                num = 5 * Integer.parseInt(Integer.toBinaryString(i));
                if (num >= l && num <= r)
                    answer.add(num);
                if (num > r)
                    break;
            }
    
            return answer.isEmpty() ? new int[]{-1} : answer.stream().mapToInt(i->i).toArray(); 
        }
    }
    ```