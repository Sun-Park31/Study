# Cisco Packet Tracer_01



오늘은 처음으로! 패킷 트레이서를 사용해봤다!

## 1. 장치 셋팅하고 케이블 연결하기

<img width="815" height="664" alt="Image" src="https://github.com/user-attachments/assets/c3df2fda-5c26-40f9-9f89-47415bd342a0" />

>> 먼저 아래쪽 아이콘을 이용하여 스위치와 노드, 서버를 셋팅했다.

<img width="815" height="664" alt="Image" src="https://github.com/user-attachments/assets/782b3a67-33b3-45a5-8d71-b95152c6e051" />

>> 케이블을 연결하여 신호가 제대로 오가는 것까지 확인하였다.

>> 자동 케이블을 이용하면 각각의 상황에 맞게 알아서 셋팅해준다.

## 2. 노드와 서버에 IP주소 부여하기

<img width="639" height="569" alt="Image" src="https://github.com/user-attachments/assets/bc9f335e-ed50-4362-add9-764410461d2d" />

>> 노드 중 하나인 컴퓨터를 클릭하여 상세화면으로 들어갔다.

<img width="639" height="569" alt="Image" src="https://github.com/user-attachments/assets/821f8155-e28f-45a9-bf86-3cca56b3aedb" />

>> Desktop의 IP Configuation에 들어간 화면이다.

<img width="639" height="569" alt="Image" src="https://github.com/user-attachments/assets/d0f0b0f4-b9e9-4b48-bb59-ccdb96a638f6" />

>> IP Address에 C클래스 주소를 부여하였다. IP 주소만 작성하면 프로그램에서 서브넷 마스크는 자동으로 설정해준다.

>> 서버도 똑같이 반복하면 된다, 하지만 IP주소는 중복될 수 없으니 192.168.100.30으로 넣어줬다.

## 3. `arp -a` 와 `ping`으로 통신상태 확인하기

- `arp -a` : arp 캐시테이블에 저장된 모든 IP 주소와 MAC 주소의 매핑목록 호출
- `ping` : 특정 ip나 도메인을 가진 네트워크 장치와 통신여부 확인, TTL 확인

<img width="639" height="569" alt="Image" src="https://github.com/user-attachments/assets/bc9f335e-ed50-4362-add9-764410461d2d" />

>> 아까와 같이 노드의 창을 연다. Command Prompt를 실행한다.

<img width="639" height="569" alt="Image" src="https://github.com/user-attachments/assets/45b6647b-6be7-48f2-8d71-15c83e537014" />

>> 이러한 화면이 뜨는데, 먼저 `arp -a`를 사용해보면

<img width="639" height="569" alt="Image" src="https://github.com/user-attachments/assets/5551e02e-de09-4dbb-8c0b-6de94f22b20d" />

>> 아무것도 뜨지 않는다. arp에 관한 어떤 작업도 하지 않았기 때문이다.

<img width="639" height="569" alt="Image" src="https://github.com/user-attachments/assets/369efbca-b2bc-465c-9638-e21959b2ae93" />

>> 다음으로 `ping` 명령어를 이용해 서버에 붙여주었던 `192.168.100.30`에게 직접 ping을 보냈다. 정상적으로 작동하여 Reply가 뜬 모습이다.

<img width="639" height="569" alt="Image" src="https://github.com/user-attachments/assets/3ea4a84a-d37a-4538-8afc-5b99777e94e4" />

>>이후에 다시 `arp -a`를 입력하면, 서버의 ip 주소인 `192.168.100.30`과 MAC 주소인 `0600.2f78.6878`이 뜬다. 신호 교환이 원활하게 이뤄지고 있다는 의미이다.

## 4. Router 설치하기

<img width="815" height="664" alt="Image" src="https://github.com/user-attachments/assets/bcccf94d-5b5d-4bf5-a031-89c71e544294" />

>> 라우터를 위치시키고 이들도 자동 케이블로 연결하였다.

>> 라우터와 스위치 사이에는 게이트웨이가 위치해있다.

>> 라우터와 스위치 사이는 패스트이더넷포트로 이어지고, 라우터 사이는 시리얼포트로 이어진다.

## 5. Router 설정하기

<img width="639" height="569" alt="Image" src="https://github.com/user-attachments/assets/1be02a8d-3946-46a1-9905-546b7b75d681" />

>> 노드와 서버처럼, 중간에 있는 라우터를 클릭하여 CLI로 들어간다.

<img width="639" height="569" alt="Image" src="https://github.com/user-attachments/assets/b999125c-1269-416b-a211-57241281153f" />

>> 라우터를 설정하는 방식이다.

<aside>
👀

**1. 초기 부팅 및 모드 진입**

- **`Continue with configuration dialog? [yes/no]: n`**
    - 라우터가 초기화 상태일 때 마법사 형태의 자동 설정 과정을 진행할지 묻는 창입니다. 숙련자들은 보통 수동 설정을 선호하므로 **`n(no)`*을 입력하고 넘어갑니다.
- **`Router>en`** (enable)
    - 사용자 모드(`>`)에서 라우터의 모든 설정을 확인하고 변경할 수 있는 **관리자(Privileged EXEC) 모드(`#`)**로 전환하는 명령어입니다.
- **`Router#conf t`** (configure terminal)
    - 라우터의 설정을 직접 변경할 수 있는 **전역 설정(Global Configuration) 모드**로 진입합니다. 프롬프트가 `Router(config)#`로 변경됩니다.

**2. 인터페이스 선택 및 IP 주소 설정**

- **`Router(config)#int fa0/0`** (interface fastethernet 0/0)
    - 설정하고자 하는 물리적 랜포트인 **FastEthernet 0/0 인터페이스 설정 모드**로 들어갑니다. 프롬프트가 `Router(config-if)#`로 바뀝니다.
- **`Router(config-if)#ip addr 192.168.100.1 255.255.255.0`**
    - 해당 포트에 IP 주소(`192.168.100.1`)와 서브넷 마스크(`255.255.255.0`, C클래스)를 할당합니다. 이 주소는 이 포트에 연결될 로컬 네트워크 기기들의 **기본 게이트웨이(Default Gateway)** 주소가 됩니다.
- **`Router(config-if)#no shut`** (no shutdown)
    - 시스코 라우터의 모든 포트는 보안을 위해 기본적으로 비활성화(Shutdown)되어 있습니다. 이 포트를 **강제로 켜서 활성화**하는 명령어입니다.

**3. 인터페이스 활성화 로그 (결과 화면)**

`no shut` 명령어를 입력하면 라우터가 포트 상태를 감지하고 다음과 같은 시스템 메시지(로그)를 출력합니다.

- **`%LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up`**
    - 물리 계층(1계층)에서 케이블이 제대로 연결되어 하드웨어적으로 포트가 켜졌음을 의미합니다.
- **`%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0, changed state to up`**
    - 데이터 링크 계층(2계층) 프로토콜이 정상적으로 동작하여, 이제 실제로 패킷을 주고받을 수 있는 통신 준비 상태가 완료되었음을 의미합니다.

from. 챗지피티

---

정리하자면, 라우터의 0/0번 랜포트에 192.168.100.1이라는 주소를 준 뒤, 전원 버튼을 켜서 인터넷 신호가 통하게 만든 것이다.

</aside>

<img width="815" height="664" alt="Image" src="https://github.com/user-attachments/assets/89918967-1b6d-44cb-a16a-23239fe1ac8a" />

>>최종적으로 라우터까지 모두 연결이 완료된 모습이다.

<aside>
📔

오늘은 L1 부터 L3까지의 네트워크 장비를 셋팅해봤다. MAC주소로 움직이는 스위치는 따로 설정을 변경하지 않아도 구동이 가능했지만, 라우터의 경우에는 ip주소가 필요했기에 별도의 설정이 필요했다. 예상했던대로 흥미롭고 또 재미있었다. 다음 실습도 기대가 된다.

</aside>
