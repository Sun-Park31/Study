# 2주 3일차 - NAS와 윈도우 백업

sub: 1
상태: 시작 전

### ☆ NAS와 윈도우 백업 ☆

---

## 스토리지 (Storage: NAS, DAS, SAN) 및 가상화 인프라

- **NAS (Network Attached Storage)**
    - LAN(네트워크)으로 연결된 외장 하드디스크 스택 개념이며, 최근의 클라우드 스토리지와 유사함.
    - 구조적으로 스토리지 서버를 단순·소형화하여 **개인 및 중소 조직**에서 주로 사용함.
    - 네트워크상에 노드로 연결되어 물리적 장치가 항상 온라인 상태여야 하며, 네트워크 프린터 연결과 방식이 비슷함.
- **DAS (Direct Attached Storage)**: 컴퓨터에 직접 연결하는 저장공간임. (예: 내장형 하드디스크, eSATA 외장 하드디스크)
- **SAN (Storage Area Network)**: 자체 운영체제와 별도 저장공간을 갖춘 **대규모 엔터프라이즈급 조직**에서 사용하며, 중소 조직에서 운영하는 경우는 드묾.
- **마운트 (Mount)**
    - Linux에서 외부 저장장치를 사용할 때는 마운트 포인트(기본값 `/mnt`)를 생성하고 연결해야 함. (예: `mount /dev/sdb1 /USB`)
    - 각 호스트가 네트워크상의 NAS 공간을 로컬 저장소처럼 마운트 해 사용하면, 특정 호스트가 다운되어도 데이터는 NAS 서버에 안전하게 보관됨.

---

## 가상화 및 운영체제 (OS) 특징과 GUI 리소스 공유

- **UNIX 운영**: 주로 UNIX 머신에 전용 OS(Solaris 등)를 탑재해 운영하지만, VMware 같은 가상화 환경에 Solaris나 Free BSD를 설치해 구동할 수도 있음.
- **Runlevel 변경과 X Window**: CLI 환경(Runlevel 3)에서 X 모듈(`X.org`, `X-모듈`)이 탑재되면 Graphic이 들어간 GUI 환경(Runlevel 5)이 되며, `startx` 명령어로 전환 가능함.
- **원격 리소스 공유를 통한 GUI 구현**
    - 타겟인 FreeNAS 호스트가 사양이 낮아(CPU, RAM 부족) 그래픽 인터페이스가 없는 **No Graphic** 상태여도 원격 제어가 가능함.
    - 연결하려는 클라이언트 호스트(Ubuntu, PC 등)의 리소스가 풍부하다면, 클라이언트의 자원(`CPU`, `RAM`, `Graphic 모듈`)을 빌려와 FreeNAS가 GUI 화면으로 보이도록 띄울 수 있음.
- **컨테이너 가상화 효율성 비교**:
    - Rocky/Ubuntu 등의 OS를 일반적인 가상머신(VM) GUI 형태로 구동하려면 약 **4.0 GB 정도의 리소스와 큰 설치 ISO 용량**이 필요함.
    - 반면, 동일한 기능의 Rocky/Ubuntu 이미지를 **클라우드 도커 환경(Docker Image)**으로 구동하면, 리소스 사용량이 획기적으로 줄어들어 단 **200 MB 수준**으로 가볍게 가동할 수 있음. (VDI 환경 및 향후 AI Agent/비서 시스템 활용 연계 가능)
- **Linux 기본 규칙**: 명령어나 파일/폴더 명에서 대소문자를 엄격히 구분함.
    - `mkdir A`: A 디렉터리 생성함.
    - `cp -arp A B`: 속성을 유지한 채 A를 B로 복사함.

---

## 디스크 및 파일 공유 기술

- **RAID (Redundant Array of Independent Disks)**
    - Windows/Linux 서버에서 여러 개의 HDD를 하나로 묶어 복구 능력을 키우는 기술임.
    - HDD가 1~2개 고장 나도 데이터 유지가 가능하며, 목적에 따라 RAID 0, 1, 5, 6, 10 등으로 구성함.
- **NFS 및 Samba**
    - **NFS (Network File Sharing)**: Linux 시스템에서 외부로 파일/디렉터리를 공유하는 기술임.
    - **Samba**: Windows와 연계하여 작업할 때 주로 사용하며, nmb와 smb 프로토콜을 이용함.
- **보안 취약점**: 웹상의 WebDAV나 파일/프린터 공유를 위한 SMB를 통한 해킹 기법이 많이 존재하므로 주의가 필요함.

---

## 백업 및 복원 정책 (Backup & Restore Calendar)

- **백업의 원칙**: 백업은 오직 **복원(Restore)**과 장애 조치(Trouble Advice)를 위해서 수행됨. 백업 데이터, 환경 설정 파일, 로그 파일 등은 유실 방지를 위해 **반드시 '다른 호스트'에 저장**해야 함.
- **달력 기준 백업 아키텍처**
    - **기본 설계**: 토요일에 기준이 되는 **전체 백업(Full)**을 수행하고, 일요일부터 금요일까지는 매일 변경된 내용만 **증가분 백업(Incremental)**을 쪼개서 수행하는 구조임.
    - 데이터 양이 우상향하며 누적(Full + Incremental)되다가, 주기(예: 4주 단위)가 지나면 다시 토요일에 전체 백업을 수행해 기준점을 갱신함.
    - **저장 매체(Media) 및 주기별 필요 개수**:
        - 최근에는 백업과 복원 작업을 동시에 유연하게 수행할 수 있는 장점 덕분에 **테이프 드라이브(Tape-Drive)를 다시 사용하는 추세**임.
        - **주간 백업**: 일간 매체 5개 + 주간 매체 1개 = **총 6개** 필요함.
        - **월간 백업**: 주간별 5개 + 각 주간 4개(4주) + 월간 1개 = **총 10개** 필요함.
        - **년간 백업**: 분기별 1개씩 = **총 4개** 필요함.
    - **OS별 자동화 도구**:
        - **Windows Server**: **작업 스케줄러(Windows Scheduler)**를 이용해 매주 토요일 등 특정 시간에 `wbadmin.msc` 백업 프로그램이 예약 실행되도록 트리거를 지정함 (**Windows Server 2016** 환경에서 기능 추가 후 설정 가능).
        - **Linux Server**: 주기적인 반복 작업에는 **Cron**, 단 한 번만 실행하는 작업에는 **AT**를 사용함.

---

## 라우팅 경로 지정 방식 (Routing)

라우터가 목적지(타겟 노드)까지 최적의 경로를 찾는 기법은 다음과 같이 분류됨.

- **동적 라우팅 (Dynamic Routing)**: 대규모 네트워크에서 사용하며, 오류 발생 시 자동 복구됨.
    - **디스턴스 벡터(Distance Vector)**: 경과하는 라우터의 수(Hop 수 = Metric)를 기준으로 판단함. (예: RIP, RIPv2, IGRP)
    - **링크 상태(Link States)**: Hop 수 외에도 지연 시간(Delay), 대역폭(Bandwidth) 등을 종합하여 판단함. (예: OSPF, EIGRP)
- **정적 라우팅 (Static Routing)**: 소규모 네트워크에서 관리자가 직접 경로를 설정하며, 오류 시 수동 복구해야 함.
- **디폴트 라우팅 (Default Route)**: 정적 라우팅의 일종으로, 경로가 하나뿐인 고립된 네트워크(**Stub network**)에서 사용함.
- **CDP (Cisco Discovery Protocol)**: 오직 Cisco 장비로만 직접 연결된 네트워크 환경에서 설정함.

---

## 이중화 및 루핑 방지 (Redundancy & Anti-Looping)

특정 호스트에 이르는 경로를 여러 개로 구성하는 이중화(Dual Link) 환경에서는 경로가 꼬여 도는 **루핑(Looping) 현상이 필연적으로 발생**하므로 이를 제어하는 프로토콜이 필수적임.

- **스위치(L2) 영역 루핑 방지 (STP)**
    - 이중화된 스위치 구조에서 루핑을 막기 위해 **STP(Spanning Tree Protocol)**를 사용함.
    - 특정 포트를 차단(Block)해 두었다가, 메인 링크에 장애가 발생하면 죽은 스위치 포트를 빠르게 활성화하는 **RSTP(Rapid STP)**를 활용해 최적의 경로비용(Path Cost)을 다시 계산함.
- **라우터(L3) 영역 게이트웨이 이중화 (HSRP / VRRP)**
    - 두 대 이상의 라우터를 묶어 하나의 가상 게이트웨이(DDG)로 운영함.
    - 평소에는 우선순위가 높은 **Active 라우터(R1, Priority 150)**가 패킷을 처리하고, **Standby 라우터(R2, Priority 100)**는 대기함.
    - 활성화된 라우터에 장애가 발생하면 라우팅 테이블에서 신속히 제거하고, **HSRP(Hot Standby Router Protocol)** 또는 **VRRP**의 헬로 패킷 응답 구조를 통해 Standby 장비가 즉시 Active 역할을 인계받아 중단 없는 통신을 보장함. 루핑 및 혼선 방지를 위해 **Split Horizon**(스플릿 호라이즌), **Reverse Poisoning**(포이즌 리버스) 등의 기법이 사용됨.

---

## 프로토콜 분류 및 향후 학습

- **네트워크 프로토콜 분류**
    - **라우팅 프로토콜 (Routing Protocol)**: 최적의 경로를 찾아주는 프로토콜임. (예: RIP, OSPF, EIGRP 등)
    - **라우티드 프로토콜 (Routed Protocol)**: 찾아낸 경로를 통해 실제 데이터를 실어 나르는 프로토콜임. (예: IP, IPX, AppleTalk 등)
- **보안**: SSL을 이용한 PKI/TLS 설정은 암호화 키(개인키, 공개키) 및 인증서(CA)와 연관됨.
- **향후 주요 학습**: 디지털 포렌식(Digital Forensic), 악성코드 분석(Malicious Code Analysis), 리버스 엔지니어링(Reverse Engineering), 패킷 분석(Packet Analysis)

※ 주석 ※

** With ChatGPT **

---

### ★ 오늘 새로 배운 중요 내용 ★

<aside>
❗

NAS/DAS, SAN

</aside>

<aside>
❗

WinSer 백업

</aside>

### ◎ 더 찾아본 내용 ◎

<aside>
🔎

NAS CLI가 GUI 되는 과정

</aside>

<aside>
🔎

NAS 와 VDI 차이점

</aside>

<aside>
🔎

레드햇과 데비안의 기본 그룹

</aside>

## ♤ 실무를 위해 꼭 기억하자(Only for me) ♤

<aside>
🧠

</aside>
