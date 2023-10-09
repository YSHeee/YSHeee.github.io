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