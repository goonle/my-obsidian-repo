# ****1. 컬렉션(collection)이란?****

```
컬렉션(collection)은 많은 데이터 요소를 효율적으로 관리하기 위한 자료구조를 말하며, ArrayList, LinkedList, HashMap 등이 여기에 포함됩니다. 그리고 이 컬렉션들은 제네릭(generics) 형식으로 구현되어 있어 컬렉션과 함께 제네릭에 대해서도 알아둘 필요가 있습니다. 
```
![[Pasted image 20231108150416.png]]
---

### **Collection 인터페이스의 주요 메서드**

1. boolean add(E e) : 현재 컬렉션에 데이터 객체 e를 추가합니다.
2. boolean addAll(Collection<? extends E> c) : 현재 컬렉션에 컬렉션 c의 모든 데이터를 추가합니다
3. boolean contains(Object o) : 현재 컬렉션에 객체 o의 포함 여부를 반환합니다.
4. boolean containsAll(Collection<?> c) : 현재 컬렉션에 컬렉션 c의 모든 데이터가 포함되어있는지 여부를 반환합니다
5. boolean remove(Object o) : 현재 컬렉션에서 객체 o를 삭제합니다
6. boolean removeAll(Collection<?> c) : 현재 컬렉션에서 컬렉션 c와 일치하는 데이터를 삭제합니다
7. boolean retainAll(Collection<?> c) : 현재 컬렉션에서 컬렉션 c와 일치하는 데이터만 남기고 나머지는 삭제합니다
8. void clear( ) : 현재 컬렉션의 모든 데이터를 삭제합니다
9. int size( ) : 현재 컬렉션에 포함된 데이터 개수를 반환합니다

## Collection의 특징
---
Collection class들이 데이터를 다룰 때, 그 데이터는 기본적으로 **객체**만 가능합니다.
그렇기에 기본 자료형인 char , int, float를 사용하지 못하고 Wrapper class를 사용해야 합니다.
"하지만 auto boxing 과 auto unboxing을 통해 사용자는 기본형을 다루듯이 사용가능 합니다."

>[!info]
> Colection과 관련된 인터페이스 또는 클래스가 정의되어 있는 코드를 살펴보면 아래와 같이 generics의 형태로 구현되어 있는 것을 확인할 수 있스빈다. 따라서 사용자는 사용하고자 하는 데이터 타입을 지정하여 사용할 수 있습니다.
> 

[출처 : KADOSHoly](https://kadosholy.tistory.com/117)
