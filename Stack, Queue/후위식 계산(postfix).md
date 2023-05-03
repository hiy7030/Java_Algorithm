# 후위식 연산(postfix)
### 설명
후위연산식이 주어지면 연산한 결과를 출력하는 프로그램을 작성하세요.

만약 3*(5+2)-9 을 후위연산식으로 표현하면 352+*9- 로 표현되며 그 결과는 12입니다.
### 입력
첫 줄에 후위연산식이 주어집니다. 연산식의 길이는 50을 넘지 않습니다.

식은 1~9의 숫자와 +, -, *, / 연산자로만 이루어진다.
<p>352+*9-</p>

### 출력
연산한 결과를 출력합니다.
<p>12</p>

### 풀이
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;


class Main {
    public int solution(String str) {
        // str의 문자를 순회하며 숫자와 문자를 구분해서 스택에 집어 넣는다?
        // 연산자를 만나면 직전에 넣었던 숫자 두개를 꺼낸 연산을 진행한다.
        // 연산의 결과는 다시 stack에 넣는다.
        Stack<Integer> stack = new Stack<>();

        for(int i = 0; i <str.length(); i++) {
            char c = str.charAt(i);

            if(c == '+') {
                stack.push(stack.pop() + stack.pop());
            } else if (c == '-') {
                stack.push(-(stack.pop() - stack.pop()));
            } else if (c == '*') {
                stack.push(stack.pop() * stack.pop());
            } else if (c == '/') {
                stack.push(stack.pop() / stack.pop());
            } else {
                stack.push(Character.getNumericValue(c));
            }
        }
        return stack.pop();
    }

    public static void main(String[] args) throws IOException {
        Main T = new Main();
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();

        int answer = T.solution(str);

        System.out.println(answer);
    }
}

```