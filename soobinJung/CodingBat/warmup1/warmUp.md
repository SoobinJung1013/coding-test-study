- [coding bat : warm up1](https://codingbat.com/java/Warmup-1)

## π· sleepIn

```java
class Solution {
    public static boolean sleepIn(boolean weekday, boolean vacation) {
        // 1. vacation : true -> sleepIn : true
        // 2. weekday : false -> sleepIn : true
        // 3. μμΈμ²λ¦¬
        if (vacation == false) {
            if (weekday == false) {
                return true;
            } else {
                return false;
            }
        }
        return true;
    }
}
```

## π· sumDouble

```java
class Solution {
    public int sumDouble(int a, int b) {
        if (a == b) {
            return (a + b) * 2;
        } else {
            return a + b;
        }
    }

}

// λ΄κ° μκ°ν λ¬Έμ  μλ
// νμ΄ μ€λͺ
// λ€λ₯Έ νμ΄
/*
 * public int sumDouble(int a, int b) { // Store the sum in a local variable int
 * sum = a + b;
 *
 * // Double it if a and b are the same if (a == b) { sum = sum * 2; }
 *
 * return sum; }
 */
// νμ΄λ€ λ³΄λ©΄ if-else λ‘ μκΌ¬μλ 
// λΌλ¦¬λ μ’μλ°, μ§κ΄μ μ΄κ² ννμ ν¨.
// νμ΄λ λΉκ΅νλ©΄ λ΄κ° μ΄ λ΅μ λΉκ΅μ  κ°λμ±μ΄ λ¨μ΄μ§
// μ€μ²©μ΄λ if-else μ€μ΄κ³  μ§κ΄μ μΌλ‘ μκ°νκ³  μμ± γ± γ±
```

## π· monkeyTrouble

```java
class Solution {
    public boolean monkeyTrouble(boolean aSmile, boolean bSmile) {
        if (aSmile == bSmile) {
            return true;
        } else {
            return false;
        }
    }
}

// λ΄κ° μκ°ν λ¬Έμ  μλ
// νμ΄ μ€λͺ
// λ€λ₯Έ νμ΄
/*
 * public boolean monkeyTrouble(boolean aSmile, boolean bSmile) { if (aSmile &&
 * bSmile) { return true; } if (!aSmile && !bSmile) { return true; } return
 * false; // The above can be shortened to: // return ((aSmile && bSmile) ||
 * (!aSmile && !bSmile)); // Or this very short version (think about how this is
 * the same as the above) // return (aSmile == bSmile); }
 */

// λμ²΄λ‘ μ€μ²©μ΄λ if else μ μμ γ γ μ±λ₯μμ λΈλ¦¬λλ΄ γ γ
// μμ§ λ΄κ° μ°λ νμ΄λ μ λ΅λ³΄λ€ κ°λμ±μ΄ νμ ν λ¨μ΄μ§.
// νμ΄ μκ°νκ³  κ°κ²°νκ² μ½λ μΈ μ μλ λ°©λ²μ μλμ§ μκ° γ± γ±
```

## π· diff21

```java
class Solution {
    public int diff21(int n) {
        int diff;
        diff = 21 - n;
        if (diff >= 0) {
            return diff;
        } else {
            return (-diff) * 2;
        }
    }
}

// λ΄κ° μκ°ν λ¬Έμ  μλ
// νμ΄ μ€λͺ
// λ€λ₯Έ νμ΄
```

## π· parrotTrouble

```java
class Solution {
    public boolean parrotTrouble(boolean talking, int hour) {
        // 0~ 7 && 20 ~23 ==> talking : flase ==. return true
        // talking time ==>
        if (7 <= hour && hour <= 20) { // talking time
            return false;
        } else { // not talking time
            if (talking == true) {
                return true;
            } else {
                return false;
            }
        }
    }

}

// λ΄κ° μκ°ν λ¬Έμ  μλ
// νμ΄ μ€λͺ

/*
 * λ€λ₯Έ νμ΄ public boolean parrotTrouble(boolean talking, int hour) { return
 * (talking && (hour < 7 || hour > 20)); // Need extra parenthesis around the ||
 * clause // since && binds more tightly than || // && is like arithmetic *, ||
 * is like arithmetic + }
 */
/*
 * not talking time -> talk ==> true μ΄μΈμ μΌμ΄μ€λ Problem false λ¦¬ν΄κ° true, flase
 * κ΅¬λΆμνκΈ°
 */
```

## π· makes10

```java
class Solution {
    public boolean makes10(int a, int b) {
        int sum;
        sum = a + b;

        if (a == 10 || b == 10 || sum == 10) {
            return true;
        } else {
            return false;
        }
    }

}

/*
 * public boolean makes10(int a, int b) { return (a == 10 || b == 10 || a+b ==
 * 10); }
 */

// 5λ² λ¬Έμ  6λ² λ¬Έμ  if μμ°κ³  return λΆλΆμμ λ°λ‘ true, false λ°νν΄μ€.
```

## π· nearHundred

```java
class Solution {
    public boolean nearHundred(int n) {
        int near100 = Math.abs(100 - n);
        int near200 = Math.abs(200 - n);
        // near value have to be 0~10
        if (near100 <= 10 || near200 <= 10) {
            return true;
        }

        return false;
    }

}
/*
 * public boolean nearHundred(int n) { return ((Math.abs(100 - n) <= 10) ||
 * (Math.abs(200 - n) <= 10)); }
 */

// ... if λΆλΆμ΄ κ°λ¨νλ©΄ return μμ λ°λ‘ λκ²¨μ£Όμ₯ ~
// Math.abs(200 - n)
```

## π· posNeg

```java
class Solution {
    public boolean posNeg(int a, int b, boolean negative) {
        // one is + one is - ==> true

        // both are - && negative ==> true
        // + + ==> false
        int multiplication = a * b;

        if (multiplication < 0 && negative == true) {
            return false;
        }

        if (multiplication >= 0 && (a > 0 || negative == false)) {
            return false;
        }

        return true;
    }

}

/*
 * public boolean posNeg(int a, int b, boolean negative) {
 *
 * // new // 1. -, + && negative == false // 2. -, - int multiplication = a*b;
 *
 * if ( multiplication < 0 && negative == false) { return true; }
 *
 * if (multiplication > 0 && a < 0 && negative == true ) { return true; }
 *
 * return false; }
 */

// λ¬Έμ κ° μ’ μ΄ν΄ μλ¨
// μμ§ μ λͺ¨λ₯΄κ² λλ° μμμμ true λμ€λ μλ€λ§ λ³΄μ¬μ€ : μ΄κ±° μ°Έκ³  γ± γ±

/*
 * public boolean posNeg(int a, int b, boolean negative) { if (negative) {
 * return (a < 0 && b < 0); } else { return ((a < 0 && b > 0) || (a > 0 && b <
 * 0)); } }
 */
// μ°μ  κ²½μ°μ μκ° λ μ μ negative μ€μ¬μΌλ‘ λΆλ₯ν¨
```

## π· notString

```java
class Solution {
    public String notString(String str) {
        // not + str
        String[] ext = str.split(" ");

        if (ext[0].equals("not")) {
            return str;
        }

        return "not " + str;
    }

}

/*
 * public String notString(String str) { if (str.length() >= 3 &&
 * str.substring(0, 3).equals("not")) { return str; }
 *
 * return "not " + str; }
 */

// str.substring(0, 3).equals("not")

```

## π· missingChar

```java
public String missingChar(String str, int n) {
        // index of array
        // subString(a, b) = aλΆν° bμ κΉμ§μ μμΉμ λ¬Έμμ΄μ κ°μ Έμ¨λ€.
        // substring(a, b)

        return str.substring(0, n) + str.substring(n + 1, str.length());
}


// subStingμΌλ‘ νλλ° μλ¨
// substringμΌλ‘ νλκΉ λ¨
// μκ·Έλ¬λμ§ λͺ¨λ₯΄κ² μ γγ
// substing(0, n)μΌλ‘ν  λ 0μ΄μ n μ κΉμ§ κ°μ Έμ€λ κ±°μ

// java string λ©μλ μ λ¦¬νκ±° μ½μ΄λ³΄κΈ°
```

## π· backAround

```java
public String backAround(String str) {
    int len = str.length();
    char lastChar = str.charAt(len-1);
    return lastChar + str + lastChar;
  }


//   public String backAround(String str) {
//     // Get the last char
//     String last = str.substring(str.length() - 1);
//     return last + str + last;
//   }
```

## π· or35

```java
public boolean or35(int n) {

    return n % 3 == 0 || n % 5 == 0;
  }


//   public boolean or35(int n) {
//     return (n % 3 == 0) || (n % 5 == 0);
//   }
```

## π· front22

```java
public String front22(String str) {

    String twoChar;

    if ( str.length() >= 2 ) {
        twoChar = str.substring(0,2);
        return twoChar + str + twoChar;
    } else {
      return str + str + str;
    }

  }


// Solution:
//   public String front22(String str) {
//     // First figure the number of chars to take
//     int take = 2;
//     if (take > str.length()) {
//       take = str.length();
//     }

//     String front = str.substring(0, take);
//     return front + str + front;
//   }
```

## π· startHi

```java
public boolean startHi(String str) {
    if ( str.length() < 2 ) {
      return false;
    }

    return str.substring(0,2).equals("hi");
  }


//λμμ§ μμκ±°κ°μ. μμΈμ²λ¦¬ ν΄μ€κ±° μνμ.
```

## π· icyHot

```java
public boolean icyHot(int temp1, int temp2) {

    int checkMinus = temp1 * temp2;

    if (checkMinus >= 0) {
      return false;
    }

    if ( temp1 > 100 || temp2 > 100 ){
      return true;
    }

    return false;
  }


// λ΄κ° λλ¬΄ μ΄λ ΅κ² μκ°νκ±°κ°μ. λ©λͺ¨λ¦¬λ μκ° λͺ»λ³΄λ­ ..? γ γγ γγ 

// Solution:
// public boolean icyHot(int temp1, int temp2) {
//   if ((temp1 < 0 && temp2 > 100) || (temp1 > 100 && temp2 < 0)) {
//     return true;
//   } else {
//     return false;
//   }
//   // Could be written as: return ((temp1 < 0 && ...));
// }
```

## π· frontBack

```java
public String frontBack(String str) {

    int len = str.length();

    if ( len < 2 ) {
      return str;
    }

    String front = str.substring(0,1);
    String back = str.substring(len-1, len);

    return back + str.substring(1, len - 1) + front;
  }



// Solution:
// public String frontBack(String str) {
//   if (str.length() <= 1) return str;

//   String mid = str.substring(1, str.length()-1);

//   // last + mid + first
//   return str.charAt(str.length()-1) + mid + str.charAt(0);
// }



// μλ€λ§ λ°κΎΈλ©΄λ¨. λ¬Έμμ΄ λ€ λ°κΏ
// StringBuffer sb = new StringBuffer(str);
// String reversedStr = sb.reverse().toString();
// return reversedStr; // edcba

```

## π· front3

```java
public String front3(String str) {

    if (str.length() < 3) return str + str +str ;

    String first3 = str.substring(0,3);
    return first3 + first3 + first3;
}


//repeat( ) μλ¨.
// public String front3(String str) {
//     int len = str.length();

//     if (len < 3) return str.repeat(3);

//     return str.substring(0,3).repeat(3)
//   }

```
