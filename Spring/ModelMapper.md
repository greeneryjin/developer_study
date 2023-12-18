
#### ModelMopper

: entity <-> dto로 변환해주는 라이브러리

gradle 설정

    implementation 'org.modelmapper:modelmapper:3.1.0'

pom.xml 설정

    <dependency>
        <groupId>org.modelmapper</groupId>
        <artifactId>modelmapper</artifactId>
        <version>3.1.0</version>
    </dependency>


spring bean 설정(전역적으로 사용 가능)

```java
@Configuration
public class AppConfig {

    @Bean
    public ModelMapper modelMapper(){
        return new ModelMapper();
    }
}
```

---

java example 

```java
@Entity
@Getter @Setter
public class Member {

    @Id @GeneratedValue
    @Column
    private Long id;

    private String name;
}

@Getter
public class MemberDto {
    private String name

    public MemberResponseDto(Posts entity) {
        this.name = entity.getName();
    }
}

ModelMapper modelMapper = new ModelMapper();
MemberDto memberDto = modelMapper.map(member, MemberDto.class);
System.out.println(MemberDto.getName());
```

