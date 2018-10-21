---
title: Effective Java 05
categories:
 - Java
tags: Java EffectiveJava
---

## 5. 불필요한 객체는 만들지 말라

summary
```
- 기능적으로 동일한 객체는 필요할 때마다 만드는 것보다 재사용하는 것이 바람직하다.
```



#### 기억할 것

- 변경 불가능 객체를 생성할 때 생성자 대신 정적 팩터리 메서드를 이용하는 것이 낫다. (생성자는 호출할 때마다 새로운 객체를 생성하므로)
- 변경 가능 객체도 변경할 일이 없다면 재사용 할 수 있다.
- 메서드가 호출될 때마다 비효율적으로 객체를 생성한다면, 정적 초기화 블록 (static initializer)을 통해 개선하는 것이 좋다.
- **자동 객체화 (autoboxing)**
 -- primitive type 과 wrapper type 간의 변환이 자동으로 이루어짐. 자동으로 객체를 생성하므로 불필요한 객체가 생성될 가능성이 있다.
 *객체 표현형 대신 원시 자료형을 사용하고, 생각지 못한 자동 객체화가 발생하지 않도록 유의해야 한다*

- 객체 풀 (object pool) 방식은 객체 생성 비용이 극단적으로 높은 경우에 사용하는 것이 좋다.
 (ex. 데이터베이스 연결)



