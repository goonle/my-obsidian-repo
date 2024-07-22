# 복습
### S - 단일 책임 원칙
- 하나의 책임을 갖는 객체로 만들어 복잡도를 떨어트리고 다른 수정된 코드에 영향을 덜 받게 하는 것
### O - 개방-폐쇄 원칙
- 기존 코드를 변경하지 않으며서 기능을 추가하는 원칙
### L - 리스코프 치환 원칙
- 부모 클래스를 자식 클래스로 변환하여도 기능 상 차이가 없게 만드는 것
### I - 인터페이스 분리 원칙
- 하나의 객체에서 수정이 이루어졌을 때,  내가 사용하는 기능에 문제가 없어야 하기에 인터페이스를 기능 별로 분리하여 작성하는 원칙
### D - 의존 역전 원칙
- 변하는 것과 변하지 않는 것을 구분하여 변하지 않는 것을 의존 관계로 삼으라는 원칙

# 잘 모르겠던 부분
### '개방 폐쇄 원칙'과 '리스코프 치환 원칙'의 차이

'개방 폐쇄 원칙'은 가방 할인 가격 코드 예제를 생각하면 이해가 잘 된다. 기존의 코드는 그대로 두고 기능하도록 하고 추가 기능을 만드는 것. 그리하여 다음에 추가되는 기능 또한 기존의 코드를 수정하지 않도록 하는 것.

'리스코프 치환 원칙'은 부모의 Override를 하지 않고 작성하여 부모클래스를 자식클래스로 변경하여도 기능 상의 차이가 없게 하는 원칙으로 이해했다.

그렇다면 개념이 **'기존 코드를 수정하지 않는 확장'** 이라는 관점에서 같지만 리스코프 치환 원칙은 상속에서, 개방 폐쇄 원칙은 하나의 클래스 안에서 기능의 추가가 이루어진다는 점만 다른가 싶었다.

그래서 두 가지 원칙의 차이가 무엇인지 찾아보니
- 상속을 사용하여 자식 클래스를 통해 기능을 확장하면서도 부모 클래스를 대체 가능하게 유지한다면, 이는 LSP를 준수하는 것입니다.
- 동일한 클래스에 기능을 추가하되, 기존 코드를 수정하지 않고 확장 가능하게 설계한다면, 이는 OCP를 준수하는 것입니다

찾아보고 나니 SOLID 원칙이 기존의 코드를 수정하지 않고 확장을 이뤄내는 원칙들을 새운 것이기 때문에 **기존 코드를 수정하지 않는 확장**이 같은 것은 당연하고 원칙을 세우는 대상이 *상속*에 있으면 리스코프 치환 원칙, *클래스의 확장*에 있으면 개방-폐쇄 원칙이라고 이해했다.

### 단일 책임 원칙을 활용한 코드 작성
실 업무에서는 정형화된 객체를 만들어 사용하는 것을 지양하다보니 이 개념이 어려워 GPT에게 물어봤다.

##### 비교
```python
단일 책임 원칙을 지키지 않은 코드
class Employee:
    def __init__(self, name, position, salary):
        self.name = name
        self.position = position
        self.salary = salary

    def calculate_pay(self):
        # 급여 계산 로직
        return self.salary * 1.2

    def generate_report(self):
        # 보고서 생성 로직
        return f"Employee Report for {self.name}"

    def save_to_database(self):
        # 데이터베이스 저장 로직
        print(f"Saving {self.name} to database")

# 사용 예시
emp = Employee("John Doe", "Developer", 5000)
print(emp.calculate_pay())
print(emp.generate_report())
emp.save_to_database()
```

```python
단일 책임 원칙을 지킨 코드
class Employee:
    def __init__(self, name, position, salary):
        self.name = name
        self.position = position
        self.salary = salary

class PayCalculator:
    @staticmethod
    def calculate_pay(employee):
        # 급여 계산 로직
        return employee.salary * 1.2

class ReportGenerator:
    @staticmethod
    def generate_report(employee):
        # 보고서 생성 로직
        return f"Employee Report for {employee.name}"

class DatabaseManager:
    @staticmethod
    def save_to_database(employee):
        # 데이터베이스 저장 로직
        print(f"Saving {employee.name} to database")

# 사용 예시
emp = Employee("John Doe", "Developer", 5000)
print(PayCalculator.calculate_pay(emp))
print(ReportGenerator.generate_report(emp))
DatabaseManager.save_to_database(emp)

```