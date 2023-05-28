# 송아지 찾기
### 설명
현수는 송아지를 잃어버렸다. 다행히 송아지에는 위치추적기가 달려 있다.

현수의 위치와 송아지의 위치가 수직선상의 좌표 점으로 주어지면 현수는 현재 위치에서 송아지의 위치까지 다음과 같은 방법으로 이동한다.

송아지는 움직이지 않고 제자리에 있다.

현수는 스카이 콩콩을 타고 가는데 한 번의 점프로 앞으로 1, 뒤로 1, 앞으로 5를 이동할 수 있다.

최소 몇 번의 점프로 현수가 송아지의 위치까지 갈 수 있는지 구하는 프로그램을 작성하세요.

### 입력
첫 번째 줄에 현수의 위치 S와 송아지의 위치 E가 주어진다. 직선의 좌표 점은 1부터 10,000까지이다.
<p>5 14</p>

### 출력
첫 번째 줄에 현수의 위치 S와 송아지의 위치 E가 주어진다. 직선의 좌표 점은 1부터 10,000까지이다.
<p>3</p>

### 풀이
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

class Main {
    Queue<Integer> que = new LinkedList<>();
    int[] num = new int[]{1, -1, 5};
    int[] check;
    public int solution(int s, int e){
        // 현수는 한번의 점프로 +1, -1, +5 -> 값이 레벨 1의 값
        check = new int[10001];
        check[s] = 1;
        que.offer(s);
        int l = 0;
        // que가 다 빌때까지 반복하며... que.poll한 값이 e와 같으면 return l
        while (!que.isEmpty()) {
            int len = que.size();
            for(int i = 0; i < len; i++) {
                int cur = que.poll();
                if(cur == e) return l;
                // 최근 값이 check 배열에 있는 값이면 진행 x
                // 없는 값이면 offer 진행, check배열에 저장
                for(int j = 0; j < num.length; j++) {
                    int ch = cur + num[j];
                    // ch값이 chenk 범위를 벗어나면 안됨
                    if(1 <= ch && ch <= 10000 && check[ch] == 0) {
                        que.offer(ch);
                        check[ch] = 1;
                    }
                }
            }
            l++;
        }
        return l;
    }
    public static void main(String[] args) throws IOException {
        Main T = new Main();
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        // 현수의 위치
        int s = Integer.parseInt(st.nextToken());
        // 송아지의 위치
        int e = Integer.parseInt(st.nextToken());

        int answer = T.solution(s, e);
        System.out.println(answer);
    }
}

```