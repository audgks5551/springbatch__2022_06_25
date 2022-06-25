# 2022.06.25

## 의존성 추가
 - jdbc
 - jpa
 - spring batch
 - mysql
 - lombok
 - h2


## 알아야할 사항

### 배치 핵심 패턴
 - Read: 데이터 조회
 - Process: 데이터 가공
 - Write: 수정된 데이터 저장

### 스프링 배치 초기화 설정 클래스
 ```
 << 실행 순서 >>
 
 @EnableBatchProcessing => SimpleBatchConfiguration => BatchConfigurerConfiguration(BasicBatchConfigurer, JpaBatchConfigurer) => BatchAutoConfiguration
 ```
 - `SimpleBatchConfiguration`는 `JobBuilderFactory`와 `StepBuilderFactory`를 생성 및 스프링 배치의 주요 구성 요소 생성(프록시 객체로 생성)
   1. JobRepository
   2. JobLauncher
   3. JobRegistry
   4. JobExplorer
   5. PlatformTransactionManager
 - `BatchConfigurerConfiguration`
   - `BasicBatchConfigurer`는 `SimpleBatchConfiguration`에서 생성한 프록시 객체의 실제 대상 객체를 생성
   - `JpaBatchConfigurer`는 JPA 관련 객체 생성
   > BatchConfigurer 인터페이스로 커스텀 가능
 - `BatchAutoConfiguration`은 `Job`을 수행하는 `JobLauncherApplicationRunner` 빈 생성