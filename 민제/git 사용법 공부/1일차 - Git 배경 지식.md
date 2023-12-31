# git의 역사

- 유닉스(Unix) : 유닉스(Unix)는 벨 연구소에서 개발한 운영 체제입니다.
    - 유닉스의 특징
        - 다양한 종류의 시스템 사이에서 서로 **이식 가능**
        - **다중 사용자** 및 **다중 작업**을 지원
- 리눅스(LINUX) : 리눅스(LINUX)라는 용어는 리눅스 커널만을 뜻하지만, 리눅스 커널과 GNU 프로젝트의 라이브러리와 도구들이 포함된, 전체 운영체제를 나타내는 말로 흔히 쓰인다. 리눅스는 유닉스에서 파생된 운영체제이고, 유닉스와는 다르게 리눅스 OS 소스코드를 무료로 배포했다.
    - 대표적인 리눅스 배포판 : Ubuntu, Radhat, debian
- GNU(GNU’s not Unix) : GNU는 운영체제이며 온전한 자유 소프트웨어로 이루어져 있다. 그 중 대부분이 GPL로 라이센스된다. GNU와 리눅스는 결합하여 사용되지만 이를 통틀어 리눅스라 부른다. 리처드 스톨먼의 소스를 공개하지 못하거나 기술의 상업화에 대한 반감으로 GNU프로젝트가 시작되었다.
- GPL(General Public License) : 자유 소프트웨어 재단에서 만든 자유 소프트웨어 라이선스로, 소프트웨어의 실행, 연구, 공유, 수정의 자유를 최종 사용자에게 보장한다.
    - 주요 특징
        - 프로그램을 어떠한 목적으로든지 사용할 수 있다. (상업적 이용, 배포, 특허에 이용, 개인적 이용)
        - 프로그램의 [소스 코드](https://namu.wiki/w/%EC%86%8C%EC%8A%A4%20%EC%BD%94%EB%93%9C)를 용도에 따라 변경 이용 (개작 가능)
        - 원본 및 변경된 프로그램의 소스 코드 배포 및 동일 라이선스 조건 (원본 및 파생 소스코드 라이선스)
        - 법적 책임을 지지 않음. 보증하지 않음
        - 라이선스 및 저작권 고지 포함
    - GPL은 배포 소프트웨어에만 적용되며 웹서버에 GPL 프로그램이나 소스코드를 이용 시 소스코드 배포 의무가 없다.
- BitKeeper : 리눅스 커널이 사용하던 분산 버전 관리 시스템, 리눅스는 BitKeeper를 무료로 사용하지 못하게 되자 Bitkeeper의 장점과 단점을 보완한 git을 출시함.

# 버전 관리 시스템(VSC)

- VCS(Version Controll System) : 파일 변화를 시간에 따라 기록했다가 나중에 특정 시점의 버전을 다시 불러올 수 있는 시스템
- VCS를 사용하면 선택한 파일을 이전 상태로 되돌릴 수 있고, 변경 사항을 비교하고, 변경한 사람 및 변경시기를 추적할 수 있으며 파일을 잃어버리거나 잘못 고쳤을 때도 쉽게 복구할 수 있다.

## 중앙 집중식 버전 관리(CVCS)

- CVCS(Centrallized Version Controll System) : 서버가 별도로 있고 중앙의 서버가 파일들과 이들의 변경 이력을 관리, 클라이언트가 중앙 서버에서 파일을 받아서 사용
- 중앙 서버에 문제가 발생한다면 치명적이다.

## **분산 버전관리 시스템 (DVCS)**

- 분산식 버전 관리 시스템에서는 각 클라이언트들이 모두 서버의 백업본을 가진다.
- 분산식 버전 관리 시스템에서는 서버가 죽거나 오프라인 상태에서도 버전 관리를 할 수 있고, 일부 사용자의 데이터가 날아가도 복구가 가능하다. 그리고 대부분의 버전 관리가 로컬에서 이루어지므로 속도도 빠르다.
- 중앙 집중식 버전 관리 시스템에 비해 복잡하고, 동기화 문제가 있다는 단점이 있다.
- 대표적으로는 Git이 있다.
