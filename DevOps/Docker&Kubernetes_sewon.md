# 도커(Docker)
![image](https://user-images.githubusercontent.com/55613591/159166032-17c6dc03-c1ee-4b09-b55a-51d6f0b74872.png)

```
도커 소프트웨어는 리눅스 컨테이너를 만들고 사용할 수 있도록 하는 컨테이너화 기술이다.   
컨테이너 기반의 오픈소스 가상화 플랫폼이라고 불리는데, 그렇다면 여기서 말하는 컨테이너는 무엇일까?   
```

<br>

📦 **컨테이너** : 애플리케이션과 이를 구동하는 환경을 Host OS로 부터 격리한 공간(이미지를 실행한 상태)
* 응용 프로그램의 종속성과 함께 응용 프로그램 자체를 패키징 또는 캡슐화해서 격리된 공간에서 프로세스를 동작시키는 기술
* 컨테이너는 일반적으로 마이크로 서비스로 사용됨
  * 마이크로 서비스는 전체 애플리케이션 서비스를 기능별로 나눈 것 -> 변경과 조합이 가능
  * 기능별로 나누어져있는 각각의 마이크로 서비스는 빠르게 배포가 가능함
  * 분리해서 사용하기 때문에 개별 변경사항이 분리된 다른 기능들에 영향을 미치지 않음

🖼 **이미지** : 도커에서 서비스 운영에 필요한 서버 프로그램, 소스코드 라이브러리, 컴파일된 실행 파일을 묶는 형태
* 특정 프로세스를 실행하기 위한 모든 파일과 설정값(환경)을 가지는 것 -> 이 이상의 의존성 파일의 컴파일과 설치등이 필요 없어짐
  * 도커의 이미지는 용량이 큰 편이지만, 가상머신의 이미지에 비하면 적은 용량
  * 이미지는 변하지 않음
  * 이미지는 컨테이너를 만드는 도구 같은 것이기 때문에, 하나의 이미지로 여러 컨테이너를 만드는 것이 가능(컨테이너가 삭제되어도 이미지는 남음)

<hr>

### 도커 컨테이너의 이점
1. 모듈성
    * 도커의 컨테이너화 접근 방식은 전체 애플리케이션을 분해할 필요없이 애플리케이션의 일부만 분해가 가능하고, 이를 업데이트 또는 복구하는 능력에 집중
    * 사용자는 기본적으로 마이크로 서비승 기반 접근 방식을 이용하지만, 
      이 외에도 [SOA](https://en.wikipedia.org/wiki/Service-oriented_architecture)의 작동방식과 동일하게 멀티플 애플리케이션 사이에서 프로세스 공유 가능   
    
2. 계층 및 이미지 버전 제어
    * 각 도커의 이미지 파일은 일련의 계층으로 이루어져 있으며 이 계층들은 단일 이미지로 결합됨
    * 이미지가 변경될 때 계층이 생성되고, 사용자가 실행 또는 복사와 같은 명령을 지정할 때 마다 새 계층이 생성
    * 도커는 새로운 컨테이너를 구축할 때 이런 계층을 재사용하기 때문에 구축 프로세스에 드는 시간이 단축됨
    * 계층화에는 버전관리가 내재되어 있으며, 변경로그가 기본적으로 적용되므로 제어가 용이

3. 롤백
    * 계층화가 되어있기 때문에 롤백이 쉬움
    * 현재 상태가 적절하지 않은 경우 이전 버전으로 롤백 가능

4. 신속한 배포
    * 배포 시간을 몇 초로 단축 가능!
    * 각 프로세스에 대한 컨테이너를 생성함으로써 사용자는 유사한 프로세스를 새 앱과 빠르게 공유 가능
    * 컨테이너를 추가하거나 이동하기 위해 OS를 재부팅 할 필요가 없으므로 배포 시간이 크게 단축


### 도커 사용시 주의할 점
```
기본적으로 도커는 단일 컨테이너 관리에 적합하도록 만들어져있다.
이 때문에 많은 양으로 세분화된 컨테이너와 컨테이너화된 앱들을 관리하기가 어려워질 수 있다.
따라서 컨테이너들을 그룹화해서 관리할 필요가 생기는데, 이때 필요한 것이 쿠버네티스이다.
```


<hr>

# 쿠버네티스(Kubernetes)
![image](https://user-images.githubusercontent.com/55613591/159167881-0c0b5517-2428-4d65-9cea-f118ec8049e9.png)

```
쿠버네티스는 '컨테이너 오케스트레이션 툴'이다.
여기서 오케스트레이션이란 무엇일까?
```
🛠 **오케스트레이션** : 다수의 컨테이너 실행을 관리하고 조율하는 시스템
* 컨테이너가 많아질 수록 관리가 어려워짐에 따라 이를 해결하고자 등장
* 오케스트레이션 엔진을 통해, 컨테이너의 생성과 소멸, 시작 및 중단 시점 제어, 스케줄링, 로드 밸런싱등 컨테이너로 어플리케이션을 구성하는 모든 과정 관리 가능

<hr>

### 쿠버네티스의 이점

* 클라우드를 위한 애플리케이션 개발을 최적화하는 중인 경우, 물리 또는 가상 머신의 클러스트에서 컨테이너를 예약하고 실행할 수 있는 플랫폼이 확보
* 다음과 같은 작업을 수행할 수 있음
  * 여러 호스트에 걸쳐 컨테이너를 오케스트레이션
  * 하드웨어를 최대한 활용하여 엔터프라이즈 애플리케이션을 실행하는 데 필요한 리소스를 극대화
  * 애플리케이션 배포 및 업데이트를 제어하고 자동화
  * 스토리지를 장착 및 추가해 스테이트풀(stateful) 애플리케이션을 실행
  * 컨테이너화된 애플리케이션과 해당 리소스를 즉시 확장
  * 선언적으로(Declaratively) 서비스를 관리함으로써, 배포한 애플리케이션이 항상 배포 목적대로 실행되도록 함
  * 자동 배치, 자동 재시작, 자동 복제, 자동 확장을 사용해 애플리케이션 상태 확인과 셀프 복구를 수행


<hr>

#### 참고 문헌
https://www.redhat.com/ko/topics/containers/what-is-docker   
https://www.redhat.com/ko/topics/containers/what-is-kubernetes   
https://hoon93.tistory.com/48   
https://wooono.tistory.com/109   
 