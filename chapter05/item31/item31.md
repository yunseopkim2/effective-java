# Item31. 한정적 와일드카드를 사용해 API 유연성을 높이라 

## 핵심
- 널리 쓰이는 라이브러리를 작성한다면 와일드카드 타입을 적절히 사용하면 좋다.
- PECS 공식을 기억해 적절하게 와일드카드 타입을 선언한다. 

## PECS와 생산자와 소비자 

PECS는 한정적 와일드카드를 사용할 때 적용할 수 있는 공식이다. 해당 모듈(객체, 메서드)가 생산자의 역할을 한다면 extends 키워드를 사용한다. 반면에 소비자의 역할을 한다면 super 키워드를 사용한다. 두 키워드를 적절하게 사용하므로 유연하게 API를 작성할 수 있다. 

### 생산자 = 원소를 새롭게 추가하는 역할
- 매개변수가 생산하는 역할이라는 의미는 단순하게는 기존 인스턴스에 (책에서는 Stack) 새로운 원소를 추가(생산)한다는 의미이다. 그래서 기존 인스턴스에서 새로운 원소가 추가되서 문제없이 사용하려면 추가되는 원소의 타입이 기존 인스턴스의 원소 타입보다 **하위 타입**이어야 한다. 그래야 리스코프 치환이 적용되서 문제없이 사용. 

예를 들어, Stack<Animal>이라는 기존 인스턴스가 있고, 새로 추가되는 원소들이 List<Dog>라면 문제없이 스택에 추가될 수 있다. 왜냐하면 Dog는 animal을 상속한 하위타입이기 때문이다 (Dog extends Animal -> ? extends Animal) 

### 소비자 = 기존 원소를 사용하는 역할

- 매개변수가 소비하는 역할이라는 의미는 단순하게는 기존 인스턴스의 원소를 사용한다는 의미이다. 기존 인스턴스에서 기존 원소를 사용해 매개변수 리스트에 넣으려면 매개변수 리스트의 타입이 기존 인스턴스의 원소 타입보다 상위타입이어야 문제없이 들어간다.

예를 들어, Stack<Animal>이라는 기존 인스턴스가 있고, 기존 원소들이 삭제되고 특정 매개변수 리스트에 담기려면 그 특정 매개변수 리스트는 Animal 타입을 다 담을 수 있게 Animal의 상위타입이어야 한다. List<Mammal> 처럼 말이다. ( Mammal super Animal -> ? super Animal)