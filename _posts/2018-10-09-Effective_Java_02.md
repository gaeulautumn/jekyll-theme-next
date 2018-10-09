---
title: Effective Java 02
categories:
 - Java
tags: Java EffectiveJava
---

## 2. 생성자 인자가 많을 때는 Builder 패턴 적용을 고려하라

summary
```
#Builder 패턴
 - 인자가 많은 생성자나 정적 팩터리가 필요한 클래스를 설계할 때, 특히 대부분의 인자가 선택적 인자인 상황에 유용하다.

장점
1. 인자에 불변식을 적용할 수 있다. build 메소드 안에서 해당 불변식이 위반되었는지 검사할 수 있다. (불변식을 위반한 경우, IllegalStateException 을 던져야 한다) 

2. 빌더 객체는 여러 개의 varargs 인자를 받을 수 있다.

3. 유연하다. 하나의 빌더 객체로 여러 객체를 만들 수 있다.


단점
1. 객체를 생성하려면 우선 빌더 객체를 생성해야 한다. 성능이 중요한 상황에서는 오버헤드가 문제가 될 수 있다. 

2. 점층적 생성자 패턴보다 많은 코드를 요구하기 때문에 인자가 충분히 많은 상황에서 이용해야 한다.
  **lombok 등의 라이브러리를 사용하면 코드양을 줄일 수 있다.

```



#### 모르는 것
 - 불변식 (invariant)
 - 한정적 와일드카드 자료형 (bounded wildcard type)


#### 기억할 것
 - 정적 팩토리나 생성자 모두 **선택적 인자** 가 많은 상황에 잘 적응하지 못한다는 문제가 있다.  
 이에 대한 대안으로는 **점층적 생성자 패턴**, **자바빈(JavaBeans) 패턴**, **빌더(Builder) 패턴** 이 있다.
 > **점층적 생성자 패턴** : 인자 수에 따라 생성자를 쌓아올리듯 추가하는 패턴. 인자 수 가 늘어나면 코드를 작성하기 어려워지고 가독성이 떨어진다.  

 > **자바빈(JavaBeans) 패턴** : 인자 없는 생성자를 호출하여 객체를 만든 다음, setter 를 호출하여 선택적 필드의 값을 채운다. 하지만 1회 함수 호출로 객체 생성을 끝낼 수 없으므로, 객체 일관성(consistency)이 깨질 수 있다. 변경 불가능(immutable) 클래스를 만들 수 없다. (no thread-safety)  

 > **빌더(Builder) 패턴** : 점층적 생성자 패턴의 안전성에 자바빈 패턴의 가독성을 결합한 패턴. 필요한 객체를 직접 생성하는 대신, 필수 인자들을 생성자에 전달하여 빌더 객체를 만들고 빌더 객체에 정의된 setter 를 호출하여 선택적 인자들을 추가해 나간다. 그리고 마지막으로 build 메소드를 호출하여 immutable 객체를 만든다.


 ```java

NutritionFacts cocalCola = new NutritionFacts.Builder(240, 8)
                            .calories(100)
                            .sodium(35)
                            .build();
 ```

 ```java
//자료형이 T 인 객체에 대한 빌더
public interface Builder<T> {
    public T build();
}
 ```
