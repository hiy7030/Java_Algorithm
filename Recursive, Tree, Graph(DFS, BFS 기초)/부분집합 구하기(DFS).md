# 부분집합 구하기(DFS)
### 설명
자연수 N이 주어지면 1부터 N까지의 원소를 갖는 집합의 부분집합을 모두 출력하는 프로그램을 작성하세요.

### 입력
첫 줄은 자연수 N(1<=N<=10)이 입력된다.
<p>3</p>

### 출력
첫 번째 줄부터 각 줄에 하나씩 부분집합을 아래 출력예제와 같은 순서로 출력한다.

단, 공집합은 출력하지 않는다.
<p>
1 2 3<br>
1 2<br>
1 3<br>
1<br>
2 3<br>
2<br>
3<br>
</p>

### 풀이
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

class Main {
    public void solution(int n, int[] check){
        // n = 0일때, check배열의 값이 1인 인덱스 번호만 출력
        if(n == 0) {
            String str = "";
            for(int i = 1; i < check.length; i++) {
                if(check[i] == 1) {
                    str += (i + " ");
                }
            }
            if(str.length()>0) System.out.println(str);
        } else {
            check[n] = 1;
            // 좌측 순회
            solution(n-1, check);
            check[n] = 0;
            // 우측 순회
            solution(n-1, check);
        }
    }
    public static void main(String[] args) throws IOException {
        Main T = new Main();
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int[] check = new int[n+1];

        T.solution(n, check);
    }
}
```