# Kali & meta

오늘은 칼리 리눅스와 메타스플로잇을 사용해서

칼리나 메타의 경우, 머신의 설치 없이 vmx 파일로 배포가 되고 있다. VM에 임포트 하기만 하면 된다.

<img width="1108" height="816" alt="image" src="https://github.com/user-attachments/assets/21d48b97-dd6d-4689-8b14-b9dcd84d530b" />


칼리의 초기 화면이다. 기본 유저와 패스워드는 모두 kali 이다.

<img width="724" height="514" alt="image" src="https://github.com/user-attachments/assets/11abacf5-3bf3-4ee8-8fe4-f09a854b3676" />


메타의 ifconfig 화면이다. 기본 유저와 패스워드는 모두 msfadmin 이다.

<aside>
💡

칼리 : 해커와 보안 전문가들을 위한 종합 도구 상자, 모의 해킹 전용 OS라고 보면 편하다.

메타스플로잇 : 취약점을 실제로 공격해보는 가장 강력한 해킹 프레임워크, 매우 성능이 좋은 해킹툴이라고 보면 편하다.

</aside>

칼리와 메타는 좋은 목적으로 배포되고 있기는 하지만, 엄연히 해커들도 사용하는 OS이다. 그만큼 툴 또한 다양하다. 먼저, 칼리의 nmap을 알아보자.

<img width="667" height="537" alt="image" src="https://github.com/user-attachments/assets/06f3ba69-e8d9-4f19-a675-14c93c2a9b5f" />


<img width="658" height="525" alt="image" src="https://github.com/user-attachments/assets/cb4cbc72-d75e-4462-b6a5-21798efa5807" />


수 많은 양의 정보가 쏟아지듯 들어온다. 고급스캔 옵션인 -A를 했기 때문에, 타겟의 OS, 프로그램과 그의 버전정보, 취약점과 세부 설정 오류, 네트워크 경로(라우터 기기들)를 보여준다.

Kali 단독은 아니지만, 기본적으로 깔려있는 프로그램인 와이어샤크를 이용하여 패킷 분석을 해보도록 하겠다. Kali는 NIC를 Promiscuous 모드가 가능하고, 이 모드 중에는 모든 신호에 응답한다. 

<aside>
💡

와이어샤크는 만능 툴이 아니다.

와이어샤크의 가장 중요한 점은 NIC에 스치는 패킷만 읽어들일 수 있다는 것이다. 라우터 밖으로 나가는 것은 고사하고 스위치 내부에서 조차도 자유롭게 움직이지 못한다. 그렇기에 실제 호스트 환경에서는 본인 컴퓨터에 닿지 않는 패킷은 로드할 수 없다. 하지만 가상머신의 경우, 여러 설정이나 환경으로 인해, 다른 가상머신의 패킷이 와이어샤크 호스트에 닿게 된다. 이로 인해 가상머신에서는 타 머신의 패킷을 읽을 수 있게 되는 것이다.

</aside>

먼저, 다른 머신 하나를 더 켜준다. 칼리는 와이이샤크용으로 사용해야 하므로, 메타와 함께할 다른 머신을 구동해준다. 나는 우분투로 하겠다.

일단, 칼리의 와이어샤크를 실행하여, 네트워크카드에 닿는 패킷을 기록하도록 설정해주겠다.

<img width="305" height="44" alt="image" src="https://github.com/user-attachments/assets/6b880d57-cafb-48df-936e-7548844aa2f0" />


이러한 명령어로 칼리에서 실행한다.

<img width="995" height="729" alt="image" src="https://github.com/user-attachments/assets/74e039a6-83c2-4d1c-a531-77ad623e079b" />


이러한 창이 뜨는데, 우리는 NIC인 eth0를 확인한다. 

<img width="990" height="726" alt="image" src="https://github.com/user-attachments/assets/9f703892-23ae-4492-a035-07d0f2ee2123" />


이 창이 켜졌으면, 준비가 끝난 것이다.

먼저, CLI 환경의 메타에 우분투로 접속해준다. dvwa는 디렉토리라고 생각하면 편하다. 지정된 사이트에서, 이름이 dvwa인 곳으로 목적지를 정했다고 생각하면 된다.

<img width="1028" height="882" alt="image" src="https://github.com/user-attachments/assets/735e0de3-dbab-4fcb-80c0-75e80f7d1112" />


![image.png](image%208.png)

연결된 웹페이지이다. 유저는 어드민, 패스워드는 password. 초기 유저네임과 패스워드이다.

이제는 다시 칼리의 와이어샤크로 가보자.

<img width="1260" height="888" alt="image" src="https://github.com/user-attachments/assets/6507e9e6-2608-4983-8a03-c191402eff6d" />


<img width="980" height="269" alt="image" src="https://github.com/user-attachments/assets/00688eea-fa8d-4dc3-a80a-2ee1167aa038" />


찰나의 순간에도 많은 패킷이 오고갔다. 지금도 조금씩 올라가고 있는것을 보면, 내가 이 곳에 글을 쓰는 것도 감지가 되고있지 않은가 하는 생각을 한다.

이번에는 직접 신호를 읽어보겠다. 우분투가 메타에 SSH로 접속하고 나사의 변화를 알아보자.

<img width="743" height="496" alt="image" src="https://github.com/user-attachments/assets/5e25bf42-f49b-4e80-9ce2-4e465cd55d24" />


접속을 완료했다. 이제 와이어샤크로 가보자.

<img width="974" height="269" alt="image" src="https://github.com/user-attachments/assets/2fe12e92-932b-4908-8198-8be172a87ce3" />


SSH로 아주 잘 연결이 되어진 모습이다.

오늘도 꽤 재미있었다. 특히 해킹툴을 어떤 방식으로 사용하느냐에 따라 달라진다는 사실이 흥미롭고, 또 더 많은 것들을 해보고 싶어졌다. 나중에 조금 여유가 생기면, 칼리는 더 만져볼 것 같다.
