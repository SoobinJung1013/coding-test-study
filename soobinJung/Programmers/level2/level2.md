
## ๐ท ์ ํ๋ฒํธ ๋ชฉ๋ก
```java
import java.util.HashMap;
import java.util.Map;

class Solution { 
    public boolean solution(String[] phoneBook) { 
        boolean answer = true; 
        HashMap<String, Integer> map = new HashMap<>(); 
        for(int i = 0; i < phoneBook.length; i++) 
            map.put(phoneBook[i], i); 
        for(int i = 0; i < phoneBook.length; i++) { 
            for(int j = 1; j < phoneBook[i].length(); j++) { 
                if(map.containsKey(phoneBook[i].substring(0,j))) { 
                    answer = false; return answer; 
                } 
            } 
        } 
        return answer; 
    } 
}
// ์์ ์ฝ๋ ์ฑ๊ณตํจ.

import java.util.*;

class Solution {
    public boolean solution(String[] phone_book) {
        boolean answer = true;
        for (String phoneIndex : phone_book) {
            for (String phoneCompare : phone_book) { // ์๊ธฐ์์  ๋น๊ต ์ ๊ฑฐ
                if (phoneIndex.length() < phoneCompare.length()) {
                    // ๋ฌธ์์ด ๋น๊ตํ  ๋, == ๋ equals๋น๊ตํด์ ์ ์ฐ๊ธฐ
                    if (phoneIndex.equals(phoneCompare.substring(0, phoneIndex.length()))) {
                        answer = false;
                        return answer;
                    }
                }
            }
        }
        return answer;
    }
}
// ์์ ์ฝ๋ ์คํ ์๊ฐ ์๋ฌ ๋ธ.

class Solution {
    public boolean solution(String[] phoneBook) {
        for (int i = 0; i < phoneBook.length - 1; i++) {
            for (int j = i + 1; j < phoneBook.length; j++) {
                if (phoneBook[i].startsWith(phoneBook[j])) {
                    return false;
                }
                if (phoneBook[j].startsWith(phoneBook[i])) {
                    return false;
                }
            }
        }
        return true;
    }
}
// ํจ์จ์ฑ ์จ๋ฐ ๋ญ๋ฐ
```

## ๐ท ์์ฅ

```java
import java.util.HashMap;

class Solution {
    public int solution(String[][] clothes) { // 2์ฐจ์ ๋ฐฐ์ด vs 1์ฐจ์๋ฐฐ์ด
        int answer = 1;
        HashMap<String, Integer> hm = new HashMap();
        for (int i = 0; i < clothes.length; i++)
            hm.put(clothes[i][1], hm.getOrDefault(clothes[i][1], 1) + 1);
        for (String kinds : hm.keySet())
            answer *= hm.get(kinds);
        return answer - 1;
    }
}

// import java.util.*;
// import java.util.HashMap;

// // ๋ฌธ์ ๋ ํ์๋๋ฐ, ์๋๊ฐ ๋๋ฆผ
// class Solution {
// public int solution(String[][] clothes) { // 2์ฐจ์ ๋ฐฐ์ด vs 1์ฐจ์๋ฐฐ์ด
// int answer = 0;
// Map<String, Integer> hm = new HashMap();

// for (int i = 0; i < clothes.length; i++) {
// hm.put(clothes[i][1], 1);
// }
// for (int i = 0; i < clothes.length; i++) {
// hm.put(clothes[i][1], hm.get(clothes[i][1]) + 1);
// }

// int xCal = 1;
// for (String kinds : hm.keySet()) {
// xCal = xCal * hm.get(kinds);
// }
// answer = answer + xCal;
// answer += xCal;
// answer = answer - 1;

// return answer;
// }
// }

// import java.util.HashMap;

// class Solution {
// public int solution(String[][] clothes) { // 2์ฐจ์ ๋ฐฐ์ด vs 1์ฐจ์๋ฐฐ์ด
// int answer = 1;
// HashMap<String, Integer> hm = new HashMap();
// for (int i = 0; i < clothes.length; i++) {
// hm.put(clothes[i][1], 1);
// }
// for (int i = 0; i < clothes.length; i++) {
// hm.put(clothes[i][1], hm.get(clothes[i][1]) + 1);
// }
// for (String kinds : hm.keySet()) {
// answer *= hm.get(kinds);
// }
// return answer - 1;
// }
// }

// ์ฝ๋ ๋๊ฐ์๋ฐ, ๊ธธ์ด ์ค์ธ๊ฑฐ

// import java.util.HashMap;
// import java.util.Iterator;
// class Solution {
// public int solution(String[][] clothes) {
// int answer = 1;
// HashMap<String, Integer> map = new HashMap<>();
// for(int i=0; i<clothes.length; i++){
// String key = clothes[i][1];
// if(!map.containsKey(key)) {
// map.put(key, 1);
// } else {
// map.put(key, map.get(key) + 1);
// }
// }
// Iterator<Integer> it = map.values().iterator();
// while(it.hasNext()) {
// answer *= it.next().intValue()+1;
// }
// return answer-1;
// }
// }

// ํ์ด๋ ๋๊ฐ์๋ฐ ๋ค๋ฅด๊ฒ ํํ

// import java.util.*;
// import static java.util.stream.Collectors.*;

// class Solution {
// public int solution(String[][] clothes) {
// return Arrays.stream(clothes)
// .collect(groupingBy(p -> p[1], mapping(p -> p[0], counting())))
// .values()
// .stream()
// .collect(reducing(1L, (x, y) -> x * (y + 1))).intValue() - 1;
// }
// }

// new
```

## ๐ท ๊ณ ์์ด์ ๊ฐ๋ ๋ช ๋ง๋ฆฌ ์์๊น

```sql
-- ์ฝ๋๋ฅผ ์๋ ฅํ์ธ์
SELECT ANIMAL_TYPE, COUNT(ANIMAL_TYPE) as count
FROM ANIMAL_INS
GROUP BY ANIMAL_TYPE
ORDER BY ANIMAL_TYPE
```

## ๐ท ๋๋ช ๋๋ฌผ ์ ์ฐพ๊ธฐ

```sql
-- ์ฝ๋๋ฅผ ์๋ ฅํ์ธ์
SELECT NAME, COUNT(NAME) as COUNT
FROM ANIMAL_INS
GROUP BY NAME
HAVING COUNT(NAME) > 1
ORDER BY NAME
```

## ๐ท ์์ ์๊ฐ ๊ตฌํ๊ธฐ

```sql
-- ์ฝ๋๋ฅผ ์๋ ฅํ์ธ์
SELECT HOUR(DATETIME), COUNT(HOUR(DATETIME)) as COUNT
FROM ANIMAL_OUTS
WHERE HOUR(DATETIME) > 8 AND HOUR(DATETIME) < 20
GROUP BY HOUR(DATETIME)
# HAVING HOUR(DATETIME) > 8 AND HOUR(DATETIME) < 20
ORDER BY HOUR(DATETIME)
```

## ๐ท NULL ์ฒ๋ฆฌํ๊ธฐ

```sql
-- ์ฝ๋๋ฅผ ์๋ ฅํ์ธ์
SELECT ANIMAL_TYPE, IFNULL(NAME, 'No name') AS NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

## ๐ท ์ค๋ณต ์ ๊ฑฐํ๊ธฐ

```sql
SELECT COUNT(DISTINCT NAME)
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
```

## ๐ท ๋๋ฌผ ์ ๊ตฌํ๊ธฐ

```sql
-- ์ฝ๋๋ฅผ ์๋ ฅํ์ธ์
SELECT COUNT(*) as 'count'
FROM ANIMAL_INS
```

## ๐ท ์ต์๊ฐ
```sql
-- ์ฝ๋๋ฅผ ์๋ ฅํ์ธ์
SELECT min(DATETIME) as '์๊ฐ' FROM ANIMAL_INS;
```

## ๐ท ๋ฃจ์์ ์๋ผ ์ฐพ๊ธฐ
```sql
-- ์ฝ๋๋ฅผ ์๋ ฅํ์ธ์
SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
WHERE NAME IN ('Lucy', 'Ella', 'Pickle', 'Rogan', 'Sabrina', 'Mitty')
ORDER BY ANIMAL_ID
```

## ๐ท ์ด๋ฆ์ el ๋ค์ด๊ฐ๋ ๋๋ฌผ ์ฐพ๊ธฐ 
```sql
-- ์ฝ๋๋ฅผ ์๋ ฅํ์ธ์
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE LOWER(NAME) LIKE LOWER('%el%') AND ANIMAL_TYPE='Dog'
ORDER BY NAME
```

## ๐ท DATETIME์์ DATE๋ก ํ๋ณํ
```sql
-- ์ฝ๋๋ฅผ ์๋ ฅํ์ธ์
SELECT ANIMAL_ID, NAME, DATE_FORMAT(DATETIME, '%Y-%m-%d') as ๋ ์ง
FROM ANIMAL_INS
```