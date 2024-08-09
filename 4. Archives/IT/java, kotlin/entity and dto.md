---
text: Entity & DTO
date: 2024-07-11
tags:
---
### **- Entity**

Entity 클래스는 실제 DB 테이블과 매핑되는 핵심 클래스로, 데이터베이스의 테이블에 존재하는 컬럼들을 필드로 가지는 객체입니다.

(DB의 테이블과 1:1로 매핑되며, 테이블이 가지지 않는 컬럼을 필드로 가져서는 안 됩니다.)

Entity는 데이터베이스 영속성(persistent)의 목적으로 사용되는 객체이며, 때문에 요청(Request)이나 응답(Response) 값을 전달하는 클래스로 사용하는 것은 좋지 않습니다.

또 많은 서비스 클래스와 비즈니스 로직들이 Entity 클래스를 기준으로 동작하기 때문에 Entity 클래스가 변경되면 여러 클래스에 영향을 줄 수 있습니다.

*******

Entity에서는 setter 메서드의 사용을 지양해야 합니다.

이유는 변경되지 않는 인스턴스에 대해서도 setter로 접근이 가능해지기 때문에 객체의 일관성, 안전성을 보장하기 힘들어집니다.

(setter 메서드가 있다는 것은 불변하지 않다는 것이 됩니다.)

따라서 Entity에는 setter 대신 Constructor(생성자) 또는 Builder를 사용하게 되는데요.

setter 메서드가 아닌 생성자(Constructor)를 이용해서 초기화하는 경우 불변 객체로 활용할 수 있고, 불변 객체로 만들면 데이터를 전달하는 과정에서 데이터가 변조되지 않음을 보장할 수 있습니다.

그리고 아래 코드처럼 Builder를 사용하면 멤버 변수가 많아지더라도 어떤 값을 어떤 필드에 넣는지 코드를 통해 확인할 수 있고, 필요한 값만 넣는 것이 가능하다는 장점이 있습니다.

```java
@Builder
@Getter
@Entity
@NoArgsConstructor
public class Membmer {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long idx;
    private String name;
    private String email;
 
    public Member(Long idx, String name, String email) {
        this.idx = idx;
        this.name = name;
        this.email = email;
    }
}

// 사용 방법
Member member = Member.builder()
        .name("Jan")
        .email("Jan@Jan.com")
        .build();
```

_(Builder Pattern 사용)_

---

### **- DTO (Data Transfer Object)**

DTO는 계층(Layer) 간 데이터 교환이 이루어질 수 있도록 하는 객체로 JSON serialization과 같은 직렬화에도 사용되는 객체입니다. DTO는 원래 DAO(Data Access Object) 패턴에서 유래된 단어로 DAO에서 DB 처리 로직을 숨기고 DTO라는 결괏값을 내보내는 용도로 활용했습니다.

Controller 같은 클라이언트 단과 직접 마주하는 계층에서는 Entity 대신 DTO를 사용해서 데이터를 교환하며, Controller 외에도 여러 레이어 사이에서 DTO를 사용할 수 있지만 주로 View와 Controller 사이에서 데이터를 주고받을 때 활용성이 높습니다.
DTO는 getter, setter 메서드를 포함하며, 이 외의 비즈니스 로직은 포함하지 않습니다.

*******

setter 메서드를 가지는 경우 가변 객체로 활용할 수 있습니다.

``` java
public class MemberDTO {

    pulic MemberDTO() { }

    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

*******

자바는 데이터 자동화 처리를 위해 리플렉션 기법을 사용합니다. 예시의 DTO에서 프로퍼티(Property)가 name이라면 name의 키값으로 들어온 데이터는 리플렉션 기법으로 setter를 실행시켜 데이터를 넣을 수 있습니다.

(직접 setter를 요청하는 것이 아닌 프레임워크 내부에서 setter가 실행된다는 것이 중요한 포인트)
특히 레이어 간(View에서 Controller로 이동)에 데이터를 넘길 때 DTO를 사용하면 편하다는 것이 이런 이유에서 입니다.

_(View에서 name 필드 값을 프로퍼티에 맞춰서 넘겼을 때, 받아야 하는 곳에서 하나하나 처리하는 것이 아니라 name 속성의 이름과 매칭 되는 프로퍼티에 자동적으로 DTO가 인스턴스화 되어 MemberDTO의 자료형으로 값을 받을 수 있습니다.)_

*** 프로퍼티(Property) 개념,**

객체지향 언어인 자바에서 객체는 고유한 속성(특징)을 가지는데, 그 속성을 칭하는 단어를 프로퍼티(Property)라고 합니다. 프로퍼티는 필드(데이터 멤버)와 메서드의 중간에 있는 클래스 멤버의 특수한 유형입니다.

프로퍼티의 읽기와 쓰기는 일반적으로 getter, setter 메소드 호출로 변환되며, 이 속성의 실제 값을 담는 곳을 필드(field, 멤버 변수)라고 합니다.

_위에 MemberDTO 클래스를 예로 들면 MemberDTO는 name의 속성을 가지고 있는 객체이고, 자바 빈 정의에 의해 getter(), setter() 메서드로 실제 값(field)에 접근할 수 있습니다._  

*** 자바 빈(JavaBean)이란,**

JavaBean 규약에 따라 작성된 자바 클래스로 클래스 외부에서 필드에 접근할 때는 반드시 메서드를 통해 접근해야 하며, 이때 get, set 으로 시작하는 메소드를 이용합니다.

---

### **'Entity와 DTO를 분리하는 이유는 DB와 View 사이의 역할 분리를 위해서'**

DTO(Data Transfer Object)는 Entity 객체와 달리 각 계층끼리 주고받는 우편물이나 상자의 개념입니다. 순수하게 데이터를 담고 있다는 점에서 Entity 객체와 유사하지만, 목적 자체가 전달이므로 읽고, 쓰는 것이 모두 가능하고, 일회성으로 사용되는 성격이 강합니다.

특히 JPA를 이용하게 되면 Entity 객체는 단순히 데이터를 담는 객체가 아니라 실제 데이터베이스와 관련된 중요한 역할을 하며, 내부적으로 EM(EntityManager)에 의해 관리되는 객체라는 것을 알 수 있습니다.

또한 DTO가 일회성으로 데이터를 주고받는 용도로 사용되는 것과 다르게 Entity의 생명주기(Life Cycle)도 전혀 다르다는 점도 분리해야 하는 이유가 됩니다.

그리고 테이블에 매핑되는 정보와 실제 View에서 요청되는 정보가 다를 경우 테이블에 필요한 정보에 맞게 데이터를 변환하는 로직이 필요할 수 있는데, 해당 로직이 Entity에 들어가게 되는 것은 일반적으로 생각해도 깔끔하지 못합니다.

DB로부터 조회된 Entity를 그대로 View로 넘기게 되었을 때 불필요한 정보 및 노출되면 안 되는 정보까지 노출될 수 있고, 이를 막기 위한 로직을 따로 구현해야 한다는 점도 이유가 됩니다.
결론적으로 Entity와 DTO는 이러한 개념 및 역할을 하지만 실무에서는 회사마다 또는 프로젝트마다 스타일이 다르기 때문에 이러한 개념을 기반으로 하여 전체 작업 규칙에 맞춰서 개발하는 것이 가장 유동적인 방법이 될 것 같습니다.

---

### **- VO (Value Object)** 

VO는 값 자체를 표현하는 객체입니다. VO는 객체들의 주소 값이 달라도 데이터 값이 같으면 동일한 것으로 여깁니다.

getter 메서드와 비즈니스 로직은 포함할 수 있지만, setter 메서드는 가지지 않습니다. 또한 필요한 경우 값 비교를 위해 equals()와 hashCode() 메서드를 오버라이딩 해줘야 합니다. 

내용물이 값 자체를 의미하기 때문에 'read only'의 특징을 가지고 있습니다.

*******

equals(), hashCode() 참고 자료
#### Reference
[entity 와 dto의 차이](https://wildeveloperetrain.tistory.com/101)
[[java] DAO, DTO, VO 차이](https://lemontia.tistory.com/591)
[DTO vs VO vs Entity](https://tecoble.techcourse.co.kr/post/2021-05-16-dto-vs-vo-vs-entity/)
