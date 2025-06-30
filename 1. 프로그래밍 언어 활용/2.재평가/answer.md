## 1.
```txt
abstract class는 객체를 생성할 수 없는 추상 클래스이며, 공통적인 기능을 일부 구현한 상태로 제공한다. 자식 클래스는 이를 상속받아 나머지를 구현한다. 반면 interface는 모든 메서드가 기본적으로 추상 메서드로 선언되어 있으며, 다중 구현을 통해 객체 간의 통신 방식이나 계약(규격)을 정의할 때 사용된다. 추상 클래스는 계층 구조에서 공통적인 기능을 공유할 때 사용하며, 인터페이스는 서로 관련 없는 클래스들이 특정 동작을 강제하도록 할 때 적합하다.
```
## 2.
```txt
public: 어디서든 접근이 가능하다.
protected: 같은 패키지 또는 상속받은 클래스에서 접근 가능하다.
default(접근 제한자가 없을 때): 같은 패키지 내에서만 접근 가능하다.
private: 같은 클래스 내부에서만 접근 가능하다.
이러한 접근 제어자는 클래스의 멤버 변수와 메서드의 접근 범위를 제한하여 객체지향의 캡슐화를 구현할 수 있도록 도와준다.
```

## 3.
```txt
StringBuilder와 StringBuffer는 둘 다 문자열을 동적으로 조작할 수 있는 클래스다. 차이점은 StringBuffer는 멀티스레드 환경에서도 안전하게 사용할 수 있도록 동기화가 되어 있는 반면, StringBuilder는 동기화를 제공하지 않아 단일 스레드 환경에서 더 빠른 성능을 보인다.
예를 들어, 반복문에서 문자열을 반복적으로 연결할 때 StringBuilder를 사용하면 성능이 좋고, 여러 스레드가 동시에 접근할 수 있는 환경에서는 StringBuffer를 사용해야 데이터의 무결성을 보장할 수 있다.
```

## 4.
```java
public static int[] processArray(int[] nums) {
    return Arrays.stream(nums)
                 .distinct()
                 .sorted()
                 .toArray();
}
```

## 5.
```java
public static List<Integer> extractEvenNumbers(int[] numbers) {
    return Arrays.stream(numbers)
                 .filter(n -> n % 2 == 0)
                 .boxed()
                 .collect(Collectors.toList());
}
```

## 6.
```java
public class Book {
    private String title;
    private String author;
    private int price;

    public Book(String title, String author, int price) {
        this.title = title;
        this.author = author;
        this.price = price;
    }

    public void printInfo() {
        System.out.println("제목: " + title);
        System.out.println("저자: " + author);
        System.out.println("가격: " + price);
    }
}

// Main 클래스 예시
public class Main {
    public static void main(String[] args) {
        Book book = new Book("자바의 정석", "남궁성", 30000);
        book.printInfo();
    }
}
```

## 7.
```java
public static void countWords(String str) {
    String[] words = str.split(" ");
    Map<String, Integer> freq = new HashMap<>();
    for (String word : words) {
        freq.put(word, freq.getOrDefault(word, 0) + 1);
    }

    for (Map.Entry<String, Integer> entry : freq.entrySet()) {
        System.out.println(entry.getKey() + " : " + entry.getValue());
    }
}
```

## 8.
```java
true
false
true
```

## 9.
```java
public static int squareDigitSum(int num) {
    int sum = 0;
    while (num > 0) {
        int digit = num % 10;
        sum += digit * digit;
        num /= 10;
    }
    return sum;
}
```

## 10.
```java
public class Pair<T, U> {
    private T key;
    private U value;

    public void setKey(T key) {
        this.key = key;
    }

    public void setValue(U value) {
        this.value = value;
    }

    public T getKey() {
        return key;
    }

    public U getValue() {
        return value;
    }
}

// Main 테스트
public class Main {
    public static void main(String[] args) {
        Pair<String, Integer> pair1 = new Pair<>();
        pair1.setKey("age");
        pair1.setValue(25);
        System.out.println(pair1.getKey() + " : " + pair1.getValue());

        Pair<Integer, String> pair2 = new Pair<>();
        pair2.setKey(101);
        pair2.setValue("홍길동");
        System.out.println(pair2.getKey() + " : " + pair2.getValue());

        Pair<String, String> pair3 = new Pair<>();
        pair3.setKey("language");
        pair3.setValue("Java");
        System.out.println(pair3.getKey() + " : " + pair3.getValue());
    }
}
```