# Level 1 

## 2023.09.08

### 하샤드 수
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
    // 내 코드가 약 3-4배 정도 더 빠르다 왤까?
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
