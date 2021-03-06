# ♟ 3 : Programmers level 1

coding test site : programmers

- array, string, 함수, 반복문, 조건문
<!-- - 해시
- map
- indwx기준 14번 코드 개선점 찾아보기 -->

![문제](https://github.com/SoobinJung1013/coding-test-study/blob/main/image/level1.png)

# JAVA

## 🏷 로또의 최고 순위와 최저 순위

```java
// import java.util.*;
// import java.io.*;
// import static java.util.Arrays.*;
// import java.util.stream.IntStream;

class Solution {
    public int[] solution(int[] lottos, int[] win_nums) {
        int[] answer = new int[2];
        int zeroNum = 0;
        int correct = 0;

        for (int i =0; i < lottos.length; i++)
            if (lottos[i] == 0)
                zeroNum++;

        for (int i = 0; i < win_nums.length; i++){
            for (int k = 0; k < lottos.length; k++)
                if (win_nums[i] == lottos[k]){
                    correct++;
                }
        }

        int maxPrize = 7 - (correct + zeroNum);
        int minPrize = 7 - correct;

        if (minPrize == 7)
            minPrize = 6;
        if (maxPrize == 7)
            maxPrize = 6;

        answer[0] = maxPrize;
        answer[1] = minPrize;

        return answer;
    }
}
```

예외처리 존나 실패함 -## 6,6 즉, 0하나도 없고 하나도 당첨 안되는 경우 7 -## 6으로 바꿔주는 코드 빼먹음 ㅅㅂ
코드 왤케 더러운지 모르겠음
레벨 1인데 왤케 오래 걸리는지 개빡침ㅂㅅㅂㅅ

## 🏷 없는 숫자 더하기 : 해시맵

```java
import java.util.Arrays;
import java.util.stream.IntStream;

class Solution {
    public int solution(int[] numbers) {
        int answer = 0;
        int n = 1;

        for ( n=1; n<10; n++ ) {
            // int i = n;
            if (IntStream.of(numbers).anyMatch(x -## x == n)) {
                answer += 0;
            } else {
                answer =+ n;
            }
        }
        return answer;
    }
}
```

실상 스트림 못씀. 실제로는 아래처럼 해시맵 써서 품

```java
import java.util.*;
import java.util.stream.*;

class Solution {
    public static String solution(String[] participant, String[] completion) {
        String answer = "";

        List<String## lParticipant = (List<String##) Arrays.asList(participant).stream().sorted().collect(Collectors.toList());
        List<String## lCompletion = (List<String##) Arrays.asList(completion).stream().sorted().collect(Collectors.toList());

        int iCompSize = lCompletion.size();
        int idx = lParticipant.size()-1;;

        for(int i = 0; i < iCompSize ; i++ ) {
            if(!lCompletion.get(i).equals(lParticipant.get(i))) {
                idx = i;
                break;
            }
        }

        answer = lParticipant.get(idx);

        return answer;
    }
}
```

## 🏷 완주하지 못한 선수 : 해시맵

```java
import java.util.*;
import java.util.HashMap;

class Solution {
    public static String solution(String[] participant, String[] completion) {
        String answer = "";
        // HashSet<String## duplicatedName = new HashSet<String##();
        Map<String, Boolean## checkCompletion = new HashMap();
        Map<String, Integer## duplicatedName = new HashMap();
        for (String p : participant) {
            duplicatedName.put(p, 0);
        }
        for (String p: participant) {
            if (checkCompletion.containsKey(p)) {
                duplicatedName.put(p, duplicatedName.get(p) + 1);
            }
            checkCompletion.put(p, false);
        }
        for (String c : completion) {
            if (checkCompletion.get(c) == true) {
                duplicatedName.put(c, duplicatedName.get(c) - 1);
            }
            checkCompletion.put(c, true);
        }
        for (String key : checkCompletion.keySet()) {
            if (checkCompletion.get(key) == false) {
                answer = key;
            }
        }
        if (answer == "") {
            for (String d : duplicatedName.keySet()) {
                if (duplicatedName.get(d) != 0) {
                    answer = d;
                }
            }
        }
        return answer;
    }
}
```

## 🏷 신규아이디 추천

```java
//시발
```

## 🏷 음양 더하기

```java
class Solution {
    public int solution(int[] absolutes, boolean[] signs) {
        int answer = 0;
        for (int i = 0; i < absolutes.length; i++) {
            if (signs[i])
                answer += absolutes[i];
            else
                answer -= absolutes[i];
        }
        return answer;
    }
}
```

## 🏷 K번쨰수

```java
import java.util.Arrays;
class Solution {
    public int[] soluktion(int[] array, int[][] commands) {
        int[] answer;
        final int COMMANDSNUM = commands.length;
        answer = new int[COMMANDSNUM];
        int[] cut = {};
        //index 기준
        int i =0 ;
        int j =0;
        int k =0;

        for (int c =0; c < commands.length; c ++) {
            i = commands[c][0] -1;
            j = commands[c][1] -1;
            k = commands[c][2] -1;
            cut = Arrays.copyOfRange(array, i, j+1);
            Arrays.sort(cut);
            answer[c] = cut[k];
        }
        return answer;
    }
}
```

리팩토링 후 . . .

```java
import java.util.Arrays;
class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];

        for(int i=0; i<commands.length; i++){
            int[] temp = Arrays.copyOfRange(array, commands[i][0]-1, commands[i][1]);
            Arrays.sort(temp);
            answer[i] = temp[commands[i][2]-1];
        }

        return answer;
    }
}
```

## 🏷 체육복

```java
import java.util.*;
class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        int answer = n;
        int l = 0; //lost index
        int r = 0; //reverse index
        answer = n  - lost.length; // 기본으로 도난당하지 않은 학생 수로 체육수업에 디폴트로 참여가능

        Arrays.sort(lost);
        Arrays.sort(reserve);

        for (int i=0; i<lost.length; i++) {
            for (int j=0; j<reserve.length; j++) {
                if (lost[i] == reserve[j]) { // 여분의 체육복이 있지만 잃어버린 학생 제외하기
                    lost[i] = -1;
                    reserve[j] = -1;
                    answer++;
                    break;
                }
            }
        }

        while (l < lost.length && r < reserve.length) { // || 쓰면 안되고 && 써야함 ㅁㅊ아
            // lost : [] or reserve : []
            if (lost.length == 0 || reserve.length == 0)
                break;

            if (lost[l] == -1) {
                l++;
                continue;
            }
            if (reserve[r] == -1) {
                r++;
                continue;
            }
            int diff = lost[l] - reserve[r];

            // lost :  [3, 4] reserve : [1, 2]
            if (diff ##= 0) {
                if (diff == 1 || diff == 0) {
                    answer++;
                    r++;
                    l++;
                } else{
                    r++;
                }
            }
            else {
                if (diff == -1){
                    answer++;
                    r++;
                    l++;
                } else {
                    l++;
                }
            }

        }

        return answer;
    }
}
```

> 다른 사람들이 푼거

```java
class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        int[] people = new int[n];
        int answer = n;

        for (int l : lost)
            people[l-1]--;
        for (int r : reserve)
            people[r-1]++;

        for (int i = 0; i < people.length; i++) {
            if(people[i] == -1) {
                if(i-1##=0 && people[i-1] == 1) {
                    people[i]++;
                    people[i-1]--;
                }else if(i+1< people.length && people[i+1] == 1) {
                    people[i]++;
                    people[i+1]--;
                }else
                    answer--;
            }
        }
        return answer;
    }
}
```

## 🏷 두 개 뽑아서 더하기

```java
import java.util.*;
class Solution {
    public int[] solution(int[] numbers) {
        int[] answer = {};
        ArrayList<Integer> temp = new ArrayList<>();

        int s = 0;

        for (int i = 0; i < numbers.length; i++) {
            for (int j = 0; j < numbers.length; j++){
                if (i == j)
                    continue;
                if(!temp.contains(numbers[i]+numbers[j])){
                    temp.add(numbers[i]+numbers[j]);
                }
            }
        }
        // temp 크기로 answer 배열 크기 설정
        answer = new int[temp.size()];

        for (Integer t: temp ){
            answer[s] = t;
            s++;
        }
        Arrays.sort(answer);

        return answer;
    }
}
```

> 다른 사람들이 푼거

```java
import java.util.HashSet;
import java.util.Set;

class Solution {
     public int[] solution(int[] numbers) {
        Set<Integer> set = new HashSet<>();

        for(int i=0; i<numbers.length; i++) {
            for(int j=i+1; j<numbers.length; j++) {
                set.add(numbers[i] + numbers[j]);
            }
        }

        return set.stream().sorted().mapToInt(Integer::intValue).toArray();
    }
}
```

> 다른 사람들이 푼거

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashSet;
import java.util.Iterator;

class Solution {
    public static ArrayList<Integer> solution(int[] numbers) {
        ArrayList<Integer> answer = new ArrayList<>();
        HashSet<Integer> set = new HashSet<>();

        for (int i = 0; i < numbers.length - 1; i++) {
            for (int j = i + 1; j < numbers.length; j++) {
                set.add(numbers[i] + numbers[j]);
            }
        }

        Iterator<Integer> iter = set.iterator();
        while(iter.hasNext()) {
            answer.add(iter.next());
        }

        Collections.sort(answer);
        return answer;
    }
}
```

> 다른 사람들이 푼거

```java
import java.util.Iterator;
import java.util.Set;
import java.util.TreeSet;

class Solution {
    public int[] solution(int[] numbers) {
        Set<Integer> sumNumber = new TreeSet();

        for(int i = 0; i < numbers.length-1; i++){
            for(int j = i+1; j < numbers.length; j++){
                sumNumber.add(numbers[i] + numbers[j]);
            }
        }

        int[] answer = new int[sumNumber.size()];
        int index = 0;
        Iterator itor = sumNumber.iterator();
        while(itor.hasNext()){
            answer[index] = (int)itor.next();
            index++;
        }

        return answer;
    }
}
```

## 🏷 가운데 글자 가져오기

```java
import java.util.*;
class Solution {
    public String solution(String s) {
        String answer = "";
        if ( s.length() % 2 == 1) {
            answer = s.substring(s.length() / 2, (s.length() / 2)+1);
        } else {
            answer = s.substring((s.length() / 2)-1, (s.length() / 2)+1);
        }
        return answer;
    }
}
```

## 🏷 직사각형 별 찍기

```java
import java.util.Scanner;

class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();
        String start = "*".repeat(a);
        for (int i = 0; i < b; i++){
            System.out.println(start);
        }
    }
}
```

> 다른 사람들이 푼거

```java
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();

        for (int i = 0; i < b; i++) {
            for (int j = 0; j < a; j++) {
                System.out.print("*");
            }
            System.out.println();
        }
    }
}

```

> 다른 사람들이 푼거

```java
import java.util.Scanner;
import java.util.stream.IntStream;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();

        StringBuilder sb = new StringBuilder();
        IntStream.range(0, a).forEach(s -> sb.append("*"));
        IntStream.range(0, b).forEach(s -> System.out.println(sb.toString()));
    }
}
```

## 🏷 하사드 수

```java
import java.util.*;
class Solution {
    public boolean solution(int x) {
        boolean answer = true;
        int length = (int)(Math.log10(x)+1);
        int add = 0;
        double temp = x;
        double i = Math.pow(10,length-1);

        for (int k = 0; k < length; k++){
            add += temp/i;
            temp = temp%i;
            i /= 10;
        }

        if(x%add != 0)
            answer = false;

        return answer;
    }
}
```

> 다른 사람 풀이 : stream 사용

```java
class Solution {
    public boolean solution(int x) {
        int sum = String.valueOf(x).chars().map(ch -> ch - '0').sum();
        return x % sum == 0;
    }
}
```

## 🏷 핸드폰 번호 가리기

```java
class Solution {
    public String solution(String phone_number) {
        String last = phone_number.substring(phone_number.length()-4,phone_number.length());
        int fn = phone_number.length() - 4;
        String first = "*".repeat(fn);
        return first + last;
    }
}
```

> 다른 사람 풀이 : ch

```java
class Solution {
  public String solution(String phone_number) {
     char[] ch = phone_number.toCharArray();
     for(int i = 0; i < ch.length - 4; i ++){
         ch[i] = '*';
     }
     return String.valueOf(ch);
  }
}
```

```java
class Solution {
  public String solution(String phone_number) {
    return phone_number.replaceAll(".(?=.{4})", "*");
  }
}
```

## 🏷 행렬의 덧셈

```java
class Solution {
    public int[][] solution(int[][] arr1, int[][] arr2) {
        int[][] answer = {};
        answer = new int[arr1.length][arr1[0].length];
        for (int i = 0; i < arr1.length; i++){
            for(int j = 0; j < arr1[i].length; j++){
                answer[i][j] = arr1[i][j] + arr2[i][j];
            }
        }
        return answer;
    }
}
```

> 다른 사람 풀이

```java
class Solution {
    public int[][] solution(int[][] arr1, int[][] arr2) {
        int[][] answer = {};
        answer = arr1;
        for(int i=0; i<arr1.length; i++){
            for(int j=0; j<arr1[0].length; j++){
                answer[i][j] += arr2[i][j];
            }
        }
        return answer;
    }
}
```

## 🏷 x만큼 간격이 있는 n개의 숫자

> 입력의 int x를 long으로 바꿔줌

```java
class Solution {
    public long[] solution(long x, int n) {
        long[] answer = new long[n];

        for (int i = 0; i < n; i++) {
            answer[i] = x * (i+1);
        }
        return answer;
    }
}
```

## 🏷 평균 구하기

> 업캐스팅 다운캐스팅 나누기 할 때 주의

```java
class Solution {
    public double solution(int[] arr) {
        double total = 0;
        for (int i = 0; i < arr.length; i++){
            total += arr[i];
        }
        return total/arr.length;
    }
}
```

## 🏷 콜라츠 추측

> int 와 long 의 maximum, minimum value가 다름 temp값을 int로 하면 몇몇 테스트 케이스 통과 못함

```java
class Solution {
    public int solution(int num) {
        int answer = 0;
        double temp = num;

        while (answer <= 500){
            if (temp == 1){
                return answer;
            }
            else if (temp % 2 == 0){
                temp = temp/2;
            }
            else {
                temp = temp*3 +1;
            }
            answer++;
        }

        return -1;
    }
}
```

## 🏷 짝수와 홀수

```java
class Solution {
    public String solution(int num) {
        String answer = "";
        if (num == 0)
            answer = "Even";
        else if (num%2 == 0)
            answer = "Even";
        else
            answer = "Odd";
        return answer;
    }
}
```

## 🏷 두 정수 사이의 합

```java
class Solution {
    public long solution(int a, int b) {
        long answer = 0;

        if (a > b) {
            int temp = a;
            a = b;
            b = temp;
        }

        for (int i = a; i <= b; i++){
            answer += i;
        }

        return answer;
    }
}
```

> 다른 사람 풀이

```java
class Solution {

    public long solution(int a, int b) {
        return sumAtoB(Math.min(a, b), Math.max(b, a));
    }

    private long sumAtoB(long a, long b) {
        return (b - a + 1) * (a + b) / 2;
    }
}
```

## 🏷 약수의 합

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        for (int i =1; i <= n; i++){
            if (n%i == 0) {
                answer += i;
            }
        }
        return answer;
    }
}
```

## 🏷 문자열 내림차순으로 배치하기

```java
import java.util.*;

class Solution {
  public String solution(String s) {
      String answer = "";

      char[] cr = s.toCharArray();
      Arrays.sort(cr);
      answer = String.valueOf(cr);

      StringBuffer sb = new StringBuffer(answer);
      String rv = sb.reverse().toString();

      answer = rv;

      return answer;
  }
}
```

## 🏷 문자열 내 p와 y의 개수

```java
class Solution {
    boolean solution(String s) {
        boolean answer = true;
        int p = 0;
        int y = 0;
        for (int i = 0; i < s.length(); i++) {
            if(s.charAt(i) == 'p' || s.charAt(i) =='P')
                p++;
            if(s.charAt(i) == 'y' || s.charAt(i) =='Y')
                y++;
        }
        if (p != y)
            answer = false;

        return answer;
    }
}
```

> 다른 사람 풀이

```java
class Solution {
    boolean solution(String s) {
        s = s.toUpperCase();

        return s.chars().filter( e -> 'P'== e).count() == s.chars().filter( e -> 'Y'== e).count();
    }
}
```

```java
class Solution {
    boolean solution(String s) {
        s = s.toLowerCase();
        int count = 0;

        for (int i = 0; i < s.length(); i++) {

            if (s.charAt(i) == 'p')
                count++;
            else if (s.charAt(i) == 'y')
                count--;
        }

        if (count == 0)
            return true;
        else
            return false;
    }
}
```

## 🏷 문자열 다루기 기본

```java
class Solution {
    public boolean solution(String s) {
        boolean answer = true;
        int len = s.length();

        if (!(len== 4) && !(len == 6))
            return false;
        answer = s.chars().allMatch( Character::isDigit );
        return answer;
    }
}
```

> 다른 사람 풀이

```java
import java.util.*;

class Solution {
  public boolean solution(String s) {
        if (s.length() == 4 || s.length() == 6) return s.matches("(^[0-9]*$)");
        return false;
  }
}
```

```java
class Solution {
  public boolean solution(String s) {
      if(s.length() == 4 || s.length() == 6){
          try{
              int x = Integer.parseInt(s);
              return true;
          } catch(NumberFormatException e){
              return false;
          }
      }
      else return false;
  }
}
```

## 🏷 서울에서 김서방 찾기

```java
class Solution {
    public String solution(String[] seoul) {
        int x = 0;
        for (int i=0; i < seoul.length; i++){
            if (seoul[i].equals("Kim")) { //seoul[i] == "Kim" 문자열은 equals로 비교해줘야함 ㅂㅅㅂㅅ
                x = i;
                break;
            }
        }
        return "김서방은 " + x + "에 있다";
    }
}
```

## 🏷 수박수박수박수박수박수박수박?

```java
class Solution {
    public String solution(int n) {
        String answer = "";
        for (int i =0; i< n; i++){
            if (i%2==0){
                answer = answer + "수";
            } else {
                answer = answer + "박";
            }
        }
        return answer;
    }
}
```

## 🏷 문자열을 정수로 바꾸기

```java
class Solution {
    public int solution(String s) {
        int answer = 0;

        if (s.charAt(0) == '+'){
            answer = Integer.parseInt(s.substring(1,s.length()));
        }
        else if (s.charAt(0) == '-'){
            answer = Integer.parseInt(s.substring(1,s.length()));
            answer = -answer;
        }
        else {
            answer = Integer.parseInt(s.substring(0, s.length()));
        }

        return answer;
    }
}
```

> 다른 사람 풀이

```java
class Solution {
    public int solution(String s) {
        String answer = s;
        return Integer.parseInt(answer);
    }
}
```

## 🏷 자릿수 더하기

```java
import java.util.*;

public class Solution {
    public int solution(int n) {
        int answer = 0;

        int length = (int)(Math.log10(n)+1);
        double temp = n;
        double i = Math.pow(10,length-1);

        for (int k = 0; k < length; k++){
            answer += temp/i;
            temp = temp%i;
            i /= 10;
        }

        return answer;
    }
}
```

```java
import java.util.*;

public class Solution {
    public int solution(double n) {
        int answer = 0;
        int length = (int)(Math.log10(n)+1);
        double i = Math.pow(10,length-1);

        for (int k = 0; k < length; k++){
            answer += n/i;
            n = n%i;
            i /= 10;
        }
        return answer;
    }
}
```

> 다른사람 풀이

```java
import java.util.*;

public class Solution {
    public int solution(int n) {
        int answer = 0;

        while (n != 0) {
            answer += n % 10;
            n /= 10;
        }

        return answer;
    }
}
```

```java
import java.util.*;

public class Solution {
    public int solution(int n) {
        int answer = 0;

        while(true){
            answer+=n%10;
            if(n<10)
                break;

            n=n/10;
        }
        return answer;
    }
}

```

```java
import java.util.*;

public class Solution {
    public int solution(int n) {
        int answer = 0;
        String[] array = String.valueOf(n).split("");
        for(String s : array){
            answer += Integer.parseInt(s);
        }
        return answer;
    }
}
```

## 🏷 나누어 떨어지는 숫자 배열

```java
import java.util.*;
class Solution {
    public int[] solution(int[] arr, int divisor) {
        int[] answer;
        ArrayList<Integer> al = new ArrayList<>();
        Arrays.sort(arr);

        for (Integer i : arr) {
            if( i % divisor == 0)
                al.add(i);
        }

        if (al.size() == 0){
            al.add(-1);
        }
        answer = new int[al.size()];

        int i = 0;
        for (Integer temp : al){
            answer[i] = temp;
            i++;
        }
        return answer;
    }
}
```

```java
import java.util.Arrays;

class Solution {
  public int[] solution(int[] arr, int divisor) {
          int[] answer = Arrays.stream(arr).filter(factor -> factor % divisor == 0).toArray();
          if(answer.length == 0) answer = new int[] {-1};
          java.util.Arrays.sort(answer);
          return answer;
  }
}

```

## 🏷 제일 작은 수 제거하기

```java
import java.util.*;
class Solution {
    public int[] solution(int[] arr) {
        int[] answer;
        // 1
        if (arr.length == 1){
            answer = new int[1];
            answer[0] = -1;
            return answer;
        }
        // 아래처럼 수정 가능
        // if(arr.length == 1){
        //   int[] answer = {-1};
        //   return answer;
        // }
        //2
        answer = new int[arr.length -1];
        // 2-1
        int [] temp = new int[arr.length];
        for (int i = 0; i < arr.length; i++) {
            temp[i] = arr[i];
        }
        Arrays.sort(temp);
        int min = temp[0];
        // 2-2
        int k = 0;
        for (int i =0; i < arr.length-1; i++){
            if (arr[k] == min){
                i--;
                k++;
                continue;
            }
            answer[i] = arr[k];
            k++;
        }
        return answer;
    }
}

```

> 다른 사람이 푼 코드 : 내거랑 속도 차이 개많이 남 개빠름

```java
class Solution {
  public int[] solution(int[] arr) {
      if(arr.length == 1){
          int[] answer = {-1};
          return answer;
      }


      int[] answer = new int[arr.length-1];
      int minIndex=0;

      for(int i=0;i<arr.length;i++){
          if(arr[minIndex]>arr[i]){
              minIndex = i;
          }
      }
      for(int i=minIndex+1;i<arr.length;i++){
          arr[i-1] = arr[i];
      }
      for(int i=0;i<answer.length;i++){
          answer[i] = arr[i];
      }
      return answer;
  }
}
```

> 다름 사람이 푼 코드 : 이건 길이는 짧은데 속도가 느림

```java
import java.util.Arrays;
import java.util.stream.Stream;
import java.util.List;
import java.util.ArrayList;

class Solution {
  public int[] solution(int[] arr) {
      if (arr.length <= 1) return new int[]{ -1 };
      int min = Arrays.stream(arr).min().getAsInt();
      return Arrays.stream(arr).filter(i -> i != min).toArray();
  }
}
```

> Arraylist 사용한 코드

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
class Solution {
  public int[] solution(int[] arr) {
      if (arr.length == 1) {
            arr[0] = -1; //여기서 기존의 arr 그대로 활용하심. 메모리 아낄 수 있을듯
            return arr;
        } else {
            ArrayList<Integer> arrayList = new ArrayList<Integer>();
            for (int a : arr) {
                arrayList.add(a);
            }
            Integer minimum = Collections.min(arrayList);
            arrayList.remove(minimum); // arraylist 난 왜 안썼지 ㅂㅅㅂㅅ..
            int[] resultArray = new int[arr.length - 1];
            for (int i = 0; i < arrayList.size(); ++i) {
                resultArray[i] = arrayList.get(i);
            }
            return resultArray;
        }
  }
}
```

## 🏷 정수 내림차순으로 배치하기

> 처음에 string -> array -> stringbuffer -> string -> long하니까 무슨 [] 이 기호까지 따라옴 ㅅㅂㅅㅂ

```java
import java.util.*;

class Solution {
    public long solution(long n) {
        long answer = 0;
        String temp = Long.toString(n);
        char[] StringtoChar = temp.toCharArray();
        Arrays.sort(StringtoChar);

        StringBuilder sbf = new StringBuilder("");

        sbf.append(StringtoChar);

        String reversedTemp = sbf.reverse().toString();
        answer = Long.parseLong(reversedTemp);
        return answer;


    }
}
```

> 다른 사람 풀이 : 0.10ms 정도 빠름

```java
import java.util.*;

class Solution {
  public long solution(long n) {
        String[] list = String.valueOf(n).split("");
        Arrays.sort(list);

        StringBuilder sb = new StringBuilder();
        for (String aList : list) sb.append(aList);

        return Long.parseLong(sb.reverse().toString());
  }
}

```

> 스트림이 코드길이는 짧은데 시간 공간 측면 둘 다 개구림

```java
import java.util.*;

class Solution {
    public long solution(long n) {
        return Long.parseLong(String.valueOf(n).chars().mapToObj(ch -> (char) ch)
                .sorted(Comparator.reverseOrder())
                .collect(StringBuilder::new, StringBuilder::appendCodePoint, StringBuilder::append)
                .toString());
    }
}

```

> 버퍼나 딴거 안쓰고 array로 정렬만 해준 다음에 for 문으로 거꾸로 출력해도 될거같음 -> 근데 아래 코드도 시간이랑 공간 효율성 많이 안좋음.
> 일단 string, int[], stringBuffer, stringBuilder 가능한 행위 (오름차순, 내림차순, 더하기, 등등) 정리 해놓기
> array랑 arraylist도 같이

```java
import java.util.Arrays;

class Solution {
    public long solution(long n) {
        long answer = 0;
        String str = "" + n;
        int[] arr = new int[str.length()];
        int count = 0;

        while(n > 0) {
            arr[count++] = (int)(n%10);
            n/=10;
        }

        Arrays.sort(arr);

        String s = "";
        for(int i=str.length() - 1; i>=0; i--) {
            s += arr[i];
        }

        answer = Long.parseLong(s);

        return answer;
    }
}

```

## 🏷 이상한 문자 만들기

```java
class Solution {
    public String solution(String s) {
        String answer = "";
        String[] words = s.split(" ", -1); //여기여기여기 ㅠㅜㅠㅜㅠㅜㅠㅜ

        int cnt = 0;
        for (String word : words) {
            StringBuffer sb = new StringBuffer();
            // sb.append(word);
            for (int i =0; i < word.length(); i++){
                if(i%2 == 0 ){
                    sb.append(Character.toUpperCase(word.charAt(i)));
                }
                else{
                    sb.append(Character.toLowerCase(word.charAt(i)));
                }
            }
            words[cnt] = sb.toString();
            cnt++;
        }
        answer = String.join(" ", words);
        return answer;
    }
}
```

> 다른 사람 풀이 : 시간 ㅈㄴ 빠름

```java
class Solution {
  public String solution(String s) {
        char[] chars = s.toCharArray();
        int idx = 0;

        for (int i = 0; i < chars.length; i++) {
            if (chars[i] == ' ')
                idx = 0;
            else
                chars[i] = (idx++ % 2 == 0 ? Character.toUpperCase(chars[i]) : Character.toLowerCase(chars[i]));
        }

        return String.valueOf(chars);
  }
}

```

> 다른 사람 풀이 : 시간은 느림

```java
class Solution {
  public String solution(String s) {

        String answer = "";
        int cnt = 0;
        String[] array = s.split("");

        for(String ss : array) {
            cnt = ss.contains(" ") ? 0 : cnt + 1;
            answer += cnt%2 == 0 ? ss.toLowerCase() : ss.toUpperCase();
        }
      return answer;
  }
}
```

## 🏷 자연수 뒤집어 배열로 만들기

> long -> string(char가져옴) -> arraylist(reverse) -> array : Integer[] -> array int[] : 정리 일도 안되어 있도 시간 공간 비효율적

> 🍄 long -> array (array 하나 더 만들어서(answer) for문으로 거꾸로 원소 집어넣기)

```java
import java.util.*;
class Solution {
    public int[] solution(long n) {
        Integer[] answer;
        String s = n + "";
        List<Integer> arrayList = new ArrayList<>();

        for (int i = 0; i < s.length(); i++){
            arrayList.add(Integer.parseInt(String.valueOf(s.charAt(i))));
        }
        Collections.reverse(arrayList);
        answer = new Integer[arrayList.size()];
        answer = arrayList.toArray(answer);
        int b[] = Arrays.stream(answer).mapToInt(Integer::intValue).toArray();
        return b;
    }
}
```

> 다른 분 풀이 : 효율 제일 뛰어남

> long -> string ->> stringbuffer -> array : int[]

```java
class Solution {
  public int[] solution(long n) {
      String s = String.valueOf(n);
      StringBuilder sb = new StringBuilder(s);
      sb = sb.reverse();
      String[] ss = sb.toString().split("");

      int[] answer = new int[ss.length];
      for (int i=0; i<ss.length; i++) {
          answer[i] = Integer.parseInt(ss[i]);
      }
      return answer;
  }
}

```

> 다른 분 풀이

> long -> string -> stringbuilder(reverse) -> array : String[] -> array : int[]

> 🍄 wrapper class, boxing, unboxing

```java
class Solution {
  public int[] solution(long n) {
        // long → String
        String s = String.valueOf(n);

        // reverse()메소드를 이용하기 위하여
        // StringBuilder 인스턴스 생성
        StringBuilder sb = new StringBuilder(s);

        // reverse()로 문자열 뒤집기
        sb = sb.reverse();

        // String.split("")로 한 글자씩 잘라 배열에 담기
        String[] stringArr = sb.toString().split("");

        // 문자열 길이 만큼 배열 길이 할당
        int[] answer = new int[sb.length()];

        // String → int → int[]
        for (int i=0; i < sb.length(); i++) {
            answer[i] = Integer.parseInt(stringArr[i]);
        }

        return answer;
  }
}
```

> 🍄 다른분 풀이

```java
class Solution {
  public int[] solution(long n) {

        // 문자열 + 숫자 = 문자열
        String a = "" + n;

        int[] answer = new int[a.length()];

        int cnt = 0;

        while (n > 0) {

            // 1) 12345 % 10 = 5
            // 2) 1234 % 10 = 4
            // 3) 123 % 10 = 3
            // 4) 12 % 10 = 2
            // 5) 1 % 10 = 1
            answer[cnt] = (int) (n % 10);

            // 12345 = 1234
            // 1234 = 123
            // 123 = 12
            // 12 = 1
            // 1 = 0 ( 0.1 )
            n /= 10;

            cnt++;
        }
        return answer;
  }
}

```

## 🏷 같은 숫자는 싫어

> 내 풀이 : 수정 전 -> stream 있어서 개느림

```java
import java.util.*;

public class Solution {
    public int[] solution(int []arr) {
        Integer[] answer;
        ArrayList<Integer> a = new ArrayList<Integer>();
        int k = 0;

        for (int i =0; i < arr.length; i++){
            if (i == 0){
                a.add(arr[i]);
                k++;
                continue;
            }
            if (arr[i] == a.get(k-1)) {
                continue;
            } else {
                a.add(arr[i]);
                k++;
            }
        }
        answer = new Integer[a.size()];
        // answer = Arrays.stream(a).mapToInt(Integer::intValue).toArray();
        answer = a.toArray(answer);

        int[] real = Arrays.stream(answer).mapToInt(Integer::intValue).toArray();

        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("Hello Java");

        return real;
    }
}
```

> 내풀이 : 수정후 -> 훨씬 빨라짐 !!

```java
import java.util.*;

public class Solution {
    public int[] solution(int []arr) {
        int[] answer;
        ArrayList<Integer> a = new ArrayList<Integer>();
        int k = 0;

        for (int i =0; i < arr.length; i++){
            if (i == 0){
                a.add(arr[i]);
                k++;
                continue;
            }
            if (arr[i] == a.get(k-1)) {
                continue;
            } else {
                a.add(arr[i]);
                k++;
            }
        }
        answer = new int[a.size()];
        for(int i=0; i<answer.length; i++) {
            answer[i] = a.get(i).intValue();
        }

        return answer;
    }
}
```

> 다른 사람 풀이

```java
import java.util.*;

public class Solution {
    public int[] solution(int []arr) {
        ArrayList<Integer> tempList = new ArrayList<Integer>();
        int preNum = 10;
        for(int num : arr) {
            if(preNum != num)
                tempList.add(num);
            preNum = num;
        }
        int[] answer = new int[tempList.size()];
        for(int i=0; i<answer.length; i++) {
            answer[i] = tempList.get(i).intValue();
        }
        return answer;
    }
}
```

## 🏷 시저 암호

```java
import java.util.*;
class Solution {
    public String solution(String s, int n) {
        String answer = "";
        char[] c = new char[s.length()];
        c = s.toCharArray();

        for (int i = 0; i < s.length(); i++) {
            int temp = (int)c[i] + n;
            if (c[i] == ' ')
                temp = 32;
            if ((int)c[i] > 96 && temp > 122) {
                temp = temp - 122 + 96;
            }
            if ((int)c[i] < 91 && temp > 90){
                temp = temp - 90 + 64;
            }

            c[i] = (char)(temp);
        }

        StringBuilder sbf = new StringBuilder("");
        sbf.append(c);

        answer = sbf.toString();
        return answer;
    }
}
```

> 다른 사람 풀이 : % 사용함

```java
class Solution {
        public String solution(String s, int n) {
            String answer = "";
            for(char ch : s.toCharArray()) {
                if(ch==' ') {
                    answer += ch;
                }else if(ch>='a'&& ch<='z'){
                    answer += (char)('a' + (ch+n-'a')%26);
                }else {
                    answer += (char)('A' + (ch+n-'A')%26);
                }
            }
            System.out.println(answer);
            return answer;
        }
    }
```

## 🏷 최대공배수와 최소공약수

```java
class Solution {
    public int[] solution(int n, int m) {
        int[] answer = new int[2];
        int min = n;
        int max = m;
        if (n == m){
            answer[0] = n;
            answer[1] = n;
        } else if (n > m) {
            max = n;
            min = m;
        } else {}
        // 최대공약수
        for (int i = min; i > 0; i--) {
            if (n%i == 0 && m%i == 0){
                answer[0] = i;
                break;
            }
        }
        // 최소공배수
        for (int i = max; ;i++) {
            if(i%n == 0 && i%m == 0) {
                answer[1] = i;
                break;
            }
        }
        return answer;
    }
}
```

> 다른분 풀이

```java
class Solution {
    public int[] solution(int n, int m) {
        int[] answer = new int[2];
        for (int i = 1; i < n + m; i++) {
            if (n % i == 0 && m % i == 0) {
                answer[0] = i;
                answer[1] = n * m / answer[0];
            }
        }
        return answer;
    }

}

```

## 🏷 나머지가 1이 되는 수 찾기

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        for (int i = 1; i < n; i++) {
            if (n%i == 1) {
                answer = i;
                break;
            }
        }
        return answer;
    }
}

```

## 🏷 문자열 내 마음대로 정렬하기

```java
import java.util.*;
class Solution {
    public String[] solution(String[] strings, int n) {
        String[] answer = new String[strings.length];
        ArrayList<String> list = new ArrayList<>();

        for(String s : strings){
            list.add(s.charAt(n) + s);
        }
        Collections.sort(list);

        int i = 0;
        for (String s : list){
            answer[i] = s.substring(1,s.length());
            i++;
        }

        return answer;
    }
}
```

## 🏷 연습문제

```java
import java.util.*;
class Solution {
    public int[] solution(int[][] v) {
        int[] answer = new int[2];

        HashMap<Integer, Integer> x = new HashMap<>();
        HashMap<Integer, Integer> y = new HashMap<>();

        for (int i = 0; i < v.length; i++ ){
            if (x.containsKey(v[i][0]))
                x.put(v[i][0], x.get(v[i][0]) - 1 );
            else
                x.put(v[i][0], x.getOrDefault(v[i][0], 0) + 1);

            if (y.containsKey(v[i][1]))
                y.put(v[i][1], y.get(v[i][1]) - 1 );
            else
                y.put(v[i][1], y.getOrDefault(v[i][1], 0) + 1);
        }
        //이제 x, y 값 1인거 키값을 각각 answer에 넣어주면 끝 !

        for (Integer i : x.keySet()){
            if(x.get(i) == 1)
                answer[0] = i;
        }
        for (Integer i : y.keySet()){
            if(y.get(i) == 1)
                answer[1] = i;
        }

        // System.out.println("Hello Java");

        return answer;
    }
}
```

# sql

## 🧬 모든 레코드 조회하기 : SELECT

```sql
-- 코드를 입력하세요
SELECT * FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

## 🧬 최댓값 구하기 : SUM, MAX, MIN

```sql
SELECT datetime as 시간
from animal_ins
where datetime = (select max(datetime) from animal_ins);
```

## 🧬 이름 없는 동물의 아이디 : IS NULL

```sql
-- 코드를 입력하세요
SELECT ANIMAL_ID FROM ANIMAL_INS
WHERE NAME IS NULL
```

## 🧬 이름 있는 동물의 아이디 : IS NULl

```sql
-- 코드를 입력하세요
SELECT ANIMAL_ID FROM ANIMAL_INS
WHERE NAME IS NOT NULL
```

## 🧬 역순 정렬하기 : SELECT

```sql
-- 코드를 입력하세요
SELECT NAME, DATETIME FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC
```

## 🧬 아픈 동물 찾기 : SELECT

```sql
-- 코드를 입력하세요
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
WHERE INTAKE_CONDITION = 'Sick'
ORDER BY ANIMAL_ID
```

## 🧬 어린 동물 찾기 : SELECT

```sql
-- 코드를 입력하세요
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
WHERE INTAKE_CONDITION NOT IN ('Aged')
ORDER BY ANIMAL_ID
```

## 🧬 동물의 아이디와 이름 : SELECT

```sql
-- 코드를 입력하세요
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

## 🧬 여러 기준으로 정렬하기 : SELECT

```sql
-- 코드를 입력하세요
SELECT ANIMAL_ID, NAME, DATETIME
FROM ANIMAL_INS
ORDER BY NAME ASC, DATETIME DESC
```

## 🧬 상위 n개 레코드 : SELECT

```sql
-- 코드를 입력하세요
SELECT NAME FROM ANIMAL_INS
ORDER BY DATETIME ASC LIMIT 1
```

tqtqtqtqtqtqtqtqtqtqtqtqtqtqtq <br>
배열은 length [] <br>
문자열은 length(),charAt()
