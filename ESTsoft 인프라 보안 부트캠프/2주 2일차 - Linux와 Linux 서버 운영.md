# 2주 2일차 - Linux와 Linux 서버 운영


### ☆ Linux와 Linux 서버 운영 ☆

---

## Linux 배포판 계열 비교 및 특징

- **Debian 계열:** Ubuntu가 대표적이며, 기본 데스크톱 환경으로 **GNOME**을 사용함 (KDE 환경은 파생판인 Kubuntu에서 사용). 확장자는 `~.deb` 형식을 쓰며, 설치 시 `dpkg -i ~.deb` 명령어를 사용하고 패키지 매니저는 `apt ~`를 이용함.
- **RedHat 계열:** Rocky가 대표적이며, 데스크톱 환경으로 **GNOME**을 사용함. 확장자는 `~.rpm` 형식을 쓰며, 설치 시 `rpm -ivh ~.rpm` 명령어를 사용하고 패키지 매니저는 `yum` 또는 `dnf`를 이용함.
- **OS 출시 배경 및 관계:**
    - CentOS 7.5 이후에 CentOS 8 대신 Rocky 8가 출시되었다.
    - **Fedora**는 대부분의 베타버전 프로그램들을 올려서 실행한 뒤, 안정적인(Stable) 도구들만 추출해서 올린 OS가 CentOS 및 Rocky이다.

---

## 보안 및 침투 테스트 (Penetration Test) 개념과 도구

- **보안 역할 및 해커 분류:**
    - **Pen Test / Pen Tester:** 모의 침투 테스트(Penetration Test) 및 이를 수행하는 화이트 해커(White Hat)를 의미함.
    - **Hacker (Black Hat):** 악의적인 목적을 가진 공격자.
    - **Blue Hat:** 조직에서 제품(솔루션)을 출품할 때 각종 상황에서 문제 발생을 사전에 점검하는 역할.
    - **기타 해커 분류:** Grey Hat, Purple Hat 등이 존재함.
- **Kali Linux / BackTrack 특징:**
    - 모의 침투 테스트(Pen Testing) 수행 시 필요로 하는 대부분의 도구로 무장된 Linux 머신임.
    - CentOS/Rocky/Ubuntu와 같은 일반 Linux에서 이런 침투 도구들을 사용하려면 먼저 설치하고 설정을 해주어야 함. 침투 Linux로 Kali/BackTrack 이외에 여러 도구들도 있음.
- **Kali 기본 탑재 주요 도구:**
    - **snort:** 상용되는 IDS(Intrusion Detection System, 침입 탐지 시스템) 및 IPS(Intrusion Prevention System, 침입 방지 시스템) 도구로, Kali에 이미 설치되어 있어서 사용하기만 하면 됨.
    - **BurpSuite:** 웹 프록시(Web Proxy) 도구로 이미 Kali에 설치되어 있음.
    - **Dirb, Cadaver 등:** 악성코드를 타겟에 올리는 도구들이 이미 설치되어 있음.
- **보안 위협 및 취약점 용어:**
    - **Virus Wall:** 악성코드(실행파일: `.exe`, `.bat`, `.com`, `.php` 등은 대부분 웹에서 받지 않음)를 타겟에 올리는 도구들을 막을 때 사용되는 도구임. (XSS(Cross Site Script) 공격의 가능성이 있기도 함)
    - **pwned (owned):** 타겟 서버 등이 해커에 의해 장악된 상태를 의미함.
    - **필수 숙지 용어:** Heart Bleed, Code Injection, SQL Injection, Shell Shock, Directory Traverse, Smurf, Land, Syn Flooding, Ping of Death 등의 용어도 잘 알고 있어야 함.
- **보안 핵심 분석 분야:** Digital Forensic(디지털 포렌식), Malicious Code Analysis(악성코드 분석), Packet Analysis(패킷 분석), Reverse Engineering(역공학) 도구들도 이미 설치되어 있음.

---

## 서버 인프라 운영 및 네트워크 관리

- **Time(시간) 설정의 중요성:**
    - 서버 설정에서 Time 설정은 매우 중요하다. 이를 위해서 LAN 네트워크 상에 **NTP(Network Time Protocol) 서버**를 별도로 설치해서 LAN의 모든 노드들이 동일한 시간을 가지게 한다.
    - 내부적 시간 이외에 '외부 공적인 Time Server'와 연계해서 시간을 맞추기도 한다. 이는 로그 확인, 작업 시간 확인, 침투 확인 등에서 매우 요긴하다.
- **네트워크 지연 및 속도 불만 처리 (CDN 및 인프라 구조):**
    - 회선, 연결 등이 느리다는 고객의 불평이 있다면 관리자는 **Packet Analysis(패킷 분석)**를 통해 원인을 파악한 뒤, **CDN 네트워크** 구축을 고려할 수 있다.
    - **CDN (Content Delivery Network) 구조:** 메인 서버(Origin)의 데이터를 여러 지역(예: 부산 ISP, 일본 ISP 등)의 엣지 서버로 동기화(Synchronized)해 두고, 사용자 접속 시 **Load Balancer(라운드로빈(R.R) 또는 Anycast 방식 등)**와 로컬 ISP를 거쳐 가장 가까운 곳에서 서비스를 제공함으로써 대역폭과 응답 속도를 개선한다. (예: Naver Server 구조)
- **일괄 설치와 형상서버 (Configuration Server) 구조:**
    - 여러 머신에 Linux OS를 일괄 설치하거나 관리할 때 특정 머신을 **'형상서버(Configuration Server)'**로 구성하여 네트워크(URL)를 통해 배포한다.
    - 내부 LAN 환경에서 조직원들이 형상서버를 이용해 일관된 기술/프로그램 운영을 수행하면 외부망 대역폭 소모를 줄일 수 있다.
    - 외부 인터넷과의 직접적인 연결을 통제함으로써 악성코드 유입 여지가 적어지고 오염(Contaminated)이나 XSS 공격 등 보안 취약점이 내부망 전체로 전이되는 것을 방지하는 이점이 있다.
- **Repository (저장소):** 설치 등에 필요한 파일들이 모여 있는 곳으로 웹 사이트거나 형상서버가 된다.
- **DHCP 서버:** 로컬 LAN에 있는 호스트들에게 자동으로 IP address, Subnet mask, Gateway address, DNS server, DHCP server의 정보를 할당한다. 나중에 관리자는 해당 호스트의 Hostname, Workgroup만 별도로 지정해주면 된다.
- **NIS (Network Information Service):**
    - Kerberos, RADIUS 서버 처럼 네트워크에 로그인하는 사용자를 인증하는 서버이다. 각 서비스(Mail, Web, FTP 등)에 일일이 로그인하는 대신 NIS 서버에 한 번 로그인 정보를 저장해두면 다른 서비스를 별도 로그인 없이 이용하게 한다. 최근에는 이곳이 가장 큰 취약점이 되기 때문에 거의 사용하지 않는다.
- **운영 참고 사항:** root 패스워드는 `rootoor`로 하며, 일부 프로그램 업데이트나 커널 업그레이드는 2~3시간 이상 소요될 수 있다.

---

## SDN (Software Defined Network) 및 가상화 인프라

- **SDN (소프트웨어 정의 네트워크) 개념:**
    - 과거 하드웨어(Cisco 등 물리적 라우터/스위치 장치) 중심의 네트워크 구조에서 벗어나, **소프트웨어 컨트롤러**를 통해 네트워크 경로 제어와 관리를 중앙 집중식으로 프로그래밍하고 제어하는 가상화 기술이다.
- **가상화의 발전 구조:**
    - **물리적 머신 (Physical M/C):** 물리 하드웨어 장치 위에 OS를 직접 구동하는 방식이다.
    - **VM (가상 머신):** 가상화 환경을 통해 호스트 가상 하드웨어 위에 독립된 OS(파일 형태)를 구동하는 방식이다. 물리 장치의 물리 파일 구조와 매핑된다.
    - **Docker (컨테이너 / Pod 환경):** VM보다 경량화된 가상화 기술로, OS 커널을 공유하며 프로세스 격리 형태로 가상1, 가상2, 가상3 공간(Pod/Container)을 신속하게 띄우고 관리한다.
- **클라우드 및 오픈소스 연계:** 가상화된 SDN 인프라는 M365와 같은 클라우드 서비스 환경 및 다양한 Open Source 프로토콜/플랫폼과 연계되어 유연하게 확장된다.

---

## 사용자 계정 권한 및 sudo 관리 (Ubuntu vs Rocky)

- **Ubuntu 사용자 전환 방식:**
    - 일반 사용자 `ubuntu`가 `sudo su root` 한 뒤, 자신의 패스워드 `ubuntu`를 넣으면 root 사용자로 전환된다. 자동으로 sudo가 가능한 상태이다. `id` 명령어로 확인하면 이미 `%sudo` 그룹에 자동으로 속해있다.
    - **보안 취약점:** root 전환 시 일반 사용자의 패스워드를 재사용한다는 점에서 보안상 취약할 수 있다.
- **Rocky 사용자 전환 방식:**
    - 일반 사용자 `rocky`가 `sudo su root` 하면 오류가 발생한다. 대신 `su root`를 실행하고 설치 시 지정했던 root의 독자적인 패스워드(`rootoor`)를 입력해야 전환된다. Ubuntu와 달리 설치 시 root 패스워드를 명확히 분리하여 지정하기 때문이다.
- **`/etc/sudoers` 파일 상세 설정:**
    - **100줄:** `root ALL=(ALL) ALL` ➔ 의미: **[사용자] [어디서나(호스트)] [모든 그룹으로] [모든 명령어]** 실행 권한 부여.
    - **101줄:** `rocky ALL=(ALL) ALL` 을 추가해주면 rocky 사용자도 `sudo` 명령어로 root 권한 대행이 가능하다.
    - 특정 명령어만 제한적으로 위임하려면 `SHUTDOWN, ADDUSER, .....` 등을 명시하며, 패스워드 검증을 생략하려면 `NOPASSWD: ALL` 설정을 사용한다.
- **권한 위임 (privilege delegation)의 중요성:**
    - 완전한 root 사용자로 상시 전환하여 작업하다가 **Session Hijacking(세션 하이재킹)**을 당하면 해커가 root 권한을 통째로 탈취하므로 매우 위험하다. 이를 방지하기 위해 일반 사용자에게 `sudo`를 통한 제한적 권한 위임을 적용하며, 일부 시스템은 root 프롬프트 로그인을 원천 차단하기도 한다. (Group 단위 권한 부여 후 사용자를 매핑하는 방식 권장)

---

## SSH 암호화 및 방화벽 관리

- **SSH 포트 및 보안:** SSH 연결은 **22번 포트**를 사용하며, 23번 포트를 쓰는 Telnet의 평문 전송 방식을 암호화한다. 세션 하이재킹이 발생하더라도 데이터가 암호화되어 있어 유출을 방지한다.
- **SSL(Secure Socket Layer) 확장:** SSL 암호화 키를 프로토콜에 적용하면 HTTPS, sFTP, SMTPs 처럼 `s`가 붙는 보안 서비스가 되며, 유효한 키가 있어야만 접근 가능하다.
- **방화벽 설정:** `sudo yum -y install firewall-config`로 GUI 설정 도구를 설치할 수 있다. Rocky Linux에서 `firewall-cmd`는 CLI 방식, `firewall-config`는 GUI 방식이며 가급적 GUI 처리가 직관적이고 안전하다.
- **sshd 데몬(Daemon)의 의미:** `service sshd start`로 실행한다. 여기서 `d`는 데몬을 뜻하며, 시스템 백그라운드에서 상주하면서 클라이언트의 접속 요청을 대기하는 프로세스 서비스를 의미한다. (`httpd`, `named`, `sshd` 등 서버 서비스 명칭 뒤에 주로 붙음)

---

## 모니터링 및 프로세스/터미널 제어 명령어

- **네트워크 상태 확인 및 필터링 (`netstat`, `grep`):** `netstat -nltp | grep ssh` (또는 포트 번호 `22`) 명령어로 서비스 구동 상태를 확인한다. `| grep`은 결과물에서 특정 문자열만 걸러주는 필터 역할을 한다.
- **SSH 원격 정보 추출:** `ssh rocky@192.168.100.100 cat /etc/passwd`와 같이 대상을 지정하면 원격 서버와 대화형 셸을 연결하지 않고도 단일 명령어를 실행하여 결과 정보만 즉시 추출해올 수 있다.
- **터미널 콘솔 및 접속자 확인 (`tty`, `w`, `wc`):** `tty` 명령어로 현재 터미널 콘솔 번호를 확인하여 외부 사용자의 혼선을 방지하며, `w` 명령어로 원격 접속한 호스트 목록을 모니터링한다. `| wc -l` 등을 조합해 출력 결과의 라인 수를 계산할 수 있다.
- **프로세스 확인 및 제어 (`ps`, `kill`):** `ps -ef`로 전체 프로세스의 PID(Process ID)와 PPID(Parent Process ID) 구조를 파악한다. 외부 불법 접속 세션이 발견되면 해당하는 PID를 확인한 뒤 `kill -9 PID` 명령을 내려 해당 연결 세션 프로세스를 강제 종료(SIGKILL)시켜 강퇴시킨다. 상세 매뉴얼은 `man kill`로 확인한다.
- **시스템 리소스 모니터링 (`top`, `free`):** `top`으로 CPU, RAM 사용량 및 NICE(우선순위 값: -20~19), PR(우선순위) 등을 실시간 모니터링하며, `free` 명령어로 RAM 정보 확인 및 캐시 메모리 관리를 수행한다.

---

## 사용자 추가 및 해시/암호화/부호화 보안 개념

- **사용자 생성 절차:** `useradd paul` 후 `passwd paul`로 패스워드를 지정한다. 사용자 정보는 `/etc/passwd`에 기록되며, 비밀번호는 해시 처리되어 `/etc/shadow` 파일에 안전하게 저장된다.
- **데이터 변환 기법 비교:**
    - **Hashed (해시):** 데이터의 무결성(Integrity) 증명을 위해 사용되며 비가역적(Non-reversable)이다. 예: `md5`, `sha1`, `sha256`, `sha512`
    - **Encrypted (암호화):** 데이터의 기밀성 및 은닉(Hidden)을 위해 암호 키를 사용한다. 예: `Cryptographic`, `rsa`, `des`, `3des`
    - **Encoded (부호화):** 데이터 표현 방식을 다른 형태로 변환한다. 예: `base64`
- **해시 패스워드 크래킹 원리:** 해시는 역연산이 불가능하므로 풀 수 없다. 흔히 해시를 푼다고 하는 것은 공격자가 수많은 평문 데이터를 미리 해시화해 둔 매핑 테이블(레인보우 테이블 등)을 만들어 두고, 대상 해시 값과 일치하는 항목을 찾아내어 평문을 역추적하는 방식이다.

---

## SELinux (Security-Enhanced Linux) 상세 설정 및 컨텍스트

- **설정 정책 수준:** 미 국방성 보안 표준에서 유래한 커널 보안 모듈로 Rocky Linux에 적용된다. `enforcing`(강제 통제), `permissive`(허용하되 경고 로그), `disabled`(비활성화) 모드가 있으며 `/etc/selinux/config`에서 설정한다.
- **보안 콘텍스트 통제 (`ls -lZ`, `chcon`):** 프로세스(httpd 등)와 파일 자원 간의 보안 콘텍스트 유형이 일치해야 접근을 허용한다. `ls -lZ` 명령어로 자원의 `[user:role:type:level]` 정보를 확인한다.
    - 예: 디폴트 웹 경로가 아닌 `/home/rocky/public_html/`에 새 웹 사이트를 개설할 경우, `chcon -Rt httpd_sys_content_t /home/rocky/public_html/` 명령을 실행해 파일 시스템의 Type 속성을 웹 서버 환경에 맞추어 주어야 `enforcing` 모드에서도 정상적으로 외부 접속이 허용된다. (맞추지 않을 경우 `permissive`나 `disabled`로 우회해야 함)

※ 주석 ※

** With Chat GPT **

---
