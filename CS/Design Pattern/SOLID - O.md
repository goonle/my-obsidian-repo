# Open Closed Principle
개방 - 폐쇄 원칙이란 뜻으로 기존 코드를 변경하지 않으면서 기능을 추가하는 설계를 의미한다.

```java
public class SomeClient {
    private 성적표 성적표;
    private 출석부 출석부;
    private 도서관대출증 도서관대출증; // 새로운 필드 추가

    public void set성적표(성적표 s) {
        this.성적표 = s;
    }

    public void set출석부(출석부 s) {
        this.출석부 = s;
    }

    public void set도서관대출증(도서관대출증 d) { // 새로운 setter 추가
        this.도서관대출증 = d;
    }

    public 성적표 get성적표() {
        return this.성적표;
    }

    public 출석부 get출석부() {
        return this.출석부;
    }

    public 도서관대출증 get도서관대출증() { // 새로운 getter 추가
        return this.도서관대출증;
    }

    public void print성적표() {
        if (this.성적표 != null) {
            System.out.println("성적표 출력");
        } else {
            System.out.println("출력할 성적표가 없습니다.");
        }
    }

    public void print출석부() {
        if (this.출석부 != null) {
            System.out.println("출석부 출력");
        } else {
            System.out.println("출력할 출석부가 없습니다.");
        }
    }

    public void print도서관대출증() { // 새로운 print 메서드 추가
        if (this.도서관대출증 != null) {
            System.out.println("도서관 대출증 출력");
        } else {
            System.out.println("출력할 도서관 대출증이 없습니다.");
        }
    }
}

```

위 코드처럼 기능이 추가될 때 도서관 대출증을 추가하려면 getter, setter 그리고 사용할 객체도 추가해야 하지만 OCP를 위해서 인터페이스인 printable을 받으면 아래처럼 추가하면 된다.

```java
public class SomeClient {
    private Printable printable;

    public void setPrintable(Printable p) {
        this.printable = p;
    }

    public void print() {
        if (this.printable != null) {
            this.printable.print();
        } else {
            System.out.println("출력할 내용이 없습니다.");
        }
    }
}
//=================================================
// Printable 인터페이스
public interface Printable {
    void print();
}

// 성적표 클래스
public class 성적표 implements Printable {
    public void print() {
        // 성적표를 출력하는 코드
        System.out.println("성적표 출력");
    }
}

// 출석부 클래스
public class 출석부 implements Printable {
    public void print() {
        // 출석부를 출력하는 코드
        System.out.println("출석부 출력");
    }
}

// 도서관 대출증 클래스
public class 도서관대출증 implements Printable {
    public void print() {
        // 도서관 대출증을 출력하는 코드
        System.out.println("도서관 대출증 출력");
    }
}

```

#solid 
#OCP
