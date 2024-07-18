Java 객체지향 디자인 패턴 - 124p ~ 127p
# 인터페이스 분리 법칙(Interface segregation principle)

내가 사용할 기능과 무관하게 발생한 변화로 인해 내가 사용할 기능에는 영향을 받지 않아야 한다. 그렇게 하기 위해서는 내가 사용할 기능만 들어있는 인터페이스를 사용하는 것이 모든 기능을 망라한 인터페이스를 사용하는 것보다 낫다. 즉, 내게 필요한 기능만 들어있는 인터페이스를 사용할 때, 영향을 받을 가능성이 줄어든다.

예를 들어 복합기라는 클래스가 있고 이 클래스는 프린터, 팩스, 복사기의 기능을 가지고 있다. 내가 현재 사용할 기능이 프린터라고 가정을 할 때, 팩스의 기능이 수정되면 복합기 클래스를 사용하는 경우 수정이 이루어져 기능 상의 문제가 있거나 코드를 수정할 경우가 생긴다. 

하지만 복합기 기능 중 프린터의 기능 만을 모은 프린터 인터페이스를 사용하면 팩스 기능이 수정 되더라도 내가 사용하는 인터페이스에는 영향이 없다.

ISP에 맞는 예제입니다.

### 예제 1
##### 1) 여러 기능이 포함된 인터페이스 생성
```java
interface MultiFunctionDevice {
    void print(String document);
    void sendFax(String document, String faxNumber);
    void copy(String document);
}
```
##### 2) 기능 별로 나눈 인터페이스 생성
```java
interface Printer {
    void print(String document);
}

interface Fax {
    void sendFax(String document, String faxNumber);
}

interface Copier {
    void copy(String document);
}
```
##### 3) 사용성의 편리를 위한 구체화 클래스 생성 
```java
class 복합기 implements Printer, Fax, Copier {
    @Override
    public void print(String document) {
        System.out.println("Printing document: " + document);
    }

    @Override
    public void sendFax(String document, String faxNumber) {
        System.out.println("Sending fax to " + faxNumber + ": " + document);
    }

    @Override
    public void copy(String document) {
        System.out.println("Copying document: " + document);
    }
}
```
##### 4) 인스턴스화 하여 사용할 기능만을 포함한 인터페이스만 사용
```java
public class Main {
    public static void main(String[] args) {
        Printer printer = new 복합기();
        printer.print("Test Document");
        // 다른 기능은 사용하지 않기 때문에 영향을 받지 않습니다.
    }
}
```

인터페이스의 기능을 모아둔 복합기 class를 통해 인터페이스들의 기능을 따로 인스턴스화해서 사용할 수 있습니다. 다만 이렇게 되면 복합기의 설계가 먼저 되는 것이 아니라 각자의 기능을 먼저 설계한 후, 설계된 기능을 한번에 사용하기 위한 복합기 클래스를 만들면서 구체화해야 할 것 같습니다. 처음부터 기능의 분리를 생각하고 만들어야 가능한 코드인 것 같지만 가독성이 좋습니다.

### 예제 2
##### 1) 복합기 클래스 생성
```java
class 복합기 {
    public void print(String document) {
        System.out.println("Printing document: " + document);
    }

    public void sendFax(String document, String faxNumber) {
        System.out.println("Sending fax to " + faxNumber + ": " + document);
    }

    public void copy(String document) {
        System.out.println("Copying document: " + document);
    }
}
```
##### 2) 기능 분리를 위한 기능별 인터페이스 생성
```java
interface Printer {
    void print(String document);
}

interface Fax {
    void sendFax(String document, String faxNumber);
}

interface Copier {
    void copy(String document);
}
```
##### 3) 구체화 클래스 생성
```java
class 복합기PrinterProxy implements Printer {
    private 복합기 복합기;

    public 복합기PrinterProxy(복합기 복합기) {
        this.복합기 = 복합기;
    }

    @Override
    public void print(String document) {
        복합기.print(document);
    }
}

class 복합기FaxProxy implements Fax {
    private 복합기 복합기;

    public 복합기FaxProxy(복합기 복합기) {
        this.복합기 = 복합기;
    }

    @Override
    public void sendFax(String document, String faxNumber) {
        복합기.sendFax(document, faxNumber);
    }
}

class 복합기CopierProxy implements Copier {
    private 복합기 복합기;

    public 복합기CopierProxy(복합기 복합기) {
        this.복합기 = 복합기;
    }

    @Override
    public void copy(String document) {
        복합기.copy(document);
    }
}
```

##### 4) 사용
```java
public class Main {
    public static void main(String[] args) {
        복합기 복합기 = new 복합기();
        
        Printer printer = new 복합기PrinterProxy(복합기);
        printer.print("Test Document");

        Fax fax = new 복합기FaxProxy(복합기);
        fax.sendFax("Test Document", "123-456-7890");

        Copier copier = new 복합기CopierProxy(복합기);
        copier.copy("Test Document");
    }
}
```

먼저 복합기가 만들어진 후에 원하는 기능을 묶은 interface를 생성하고 인터페이스를 사용할 구체화 클래스를 만들어 사용을 하면 코드 상 인터페이스의 구체화 클래스를 만들어야 해서 코드의 양이 늘어나는 단점이 있지만 설계 이후 기능의 확장을 통해 리펙토링이 되는 경우에는 이렇게 사용하면 될 것 같습니다.

#solid 
#lnterfaceSegregationPrinciple