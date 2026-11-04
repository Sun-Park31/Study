# Rocky of Linux with VMware

어제는 데비안 계열의 우분투를 사용하여 네트워크를 셋팅해봤다면, 오늘은 레드햇 계열의 로키를 사용하여

 

## Rocky 설치하기

<img width="428" height="430" alt="Image" src="https://github.com/user-attachments/assets/75e8d0ac-8236-4c5a-9660-da6eaba5643b" />

VMware의 머신을 만든다. Rocky가 서비스 버전에 없으므로, 로키와 비슷한 CentOS를 선택한다. Rocky와 CentOS는 같은 레드햇 계열이다.

<img width="863" height="583" alt="Image" src="https://github.com/user-attachments/assets/9b19e91f-dc6d-43c5-8835-773d8d6e6070" />

필요한 세팅을 모두 마치고, ISO 이미지 파일도 DVD에 알맞게 꽂힌 모습이다. (메모리는 인스톨 속도 향상을 위해 잠시 올려두었다. 추후 내릴 예정이다.)

<img width="644" height="594" alt="Image" src="https://github.com/user-attachments/assets/0d1a6560-af5e-4de2-941a-601eb770c762" />

파워 온을 하면 이러한 창이 나오는데, 아주 잠시 CLI만 지원된다. 위쪽의 Install Rocky ~ 를 선택해준다.

POST 화면이 뜨고, 시간이 지나면 GUI로 바뀐다.

<img width="1274" height="860" alt="Image" src="https://github.com/user-attachments/assets/c2ef2110-0651-4935-80fb-234f7cbac010" />

이러한 창이 떴으면, 성공이다.

<img width="1274" height="860" alt="Image" src="https://github.com/user-attachments/assets/ca5ad164-e150-4462-93cf-bb3ef4aab194" />

초기 설정 탭이다. 모든 부분을 원하는 방식으로 설정하면 된다. 3곳 정도만 짚고 넘어가겠다.

<img width="1440" height="868" alt="Image" src="https://github.com/user-attachments/assets/0b945cf0-f122-4107-80a5-991cecd17be2" />

가장 먼저, SOFTWARE SELECTIOM이다. 위와 같이 설정해준다.

<img width="1440" height="868" alt="image" src="https://github.com/user-attachments/assets/3d7fbdd5-ae8e-49ee-adc0-a4bd1222518a" />


다음으로 IP와 FQDN을 설정해준다.

<img width="1440" height="868" alt="image" src="https://github.com/user-attachments/assets/e6f07545-4377-4b89-b536-186e31bbe247" />

<img width="1440" height="868" alt="image" src="https://github.com/user-attachments/assets/279b5aa7-41a8-4985-bce6-ecf858bbc22c" />

루트 계정의 비밀번호와, 새로 생성하는 사용자 계정의 비밀번호를 설정해준다.

<img width="1440" height="868" alt="image" src="https://github.com/user-attachments/assets/c0af906c-5e94-43e5-8260-209314a32241" />

설치까지 하면!

<img width="1440" height="868" alt="image" src="https://github.com/user-attachments/assets/3f7655da-a765-4f21-b084-e55e4be75f47" />

끝난다.

<img width="1440" height="868" alt="image" src="https://github.com/user-attachments/assets/a47db13e-1b10-4ba8-ae00-c526549b6ca8" />

라이선스 화면이다. 체크하고 넘어가면 된다.

<img width="1440" height="868" alt="image" src="https://github.com/user-attachments/assets/ef60b384-2719-4e5f-9762-96b6f23a6e87" />

여기까지 왔으면, 완벽하게 성공한 것이다.

<aside>
💡

설치 과정에서 자꾸만 프리즈 되는 상황이 발생했다. 어떠한 상황에서도 계속해서 문제가 발생하는 것으로 봐서는 OS 문제는 아닌 것 같았다. 윈도우 서버의 Hyper-V를 사용하는 상황에서도 호스트와 가상머신인 게스트의 충돌이 발생했던 것으로 봐서는 가상화 관련 문제가 있지 않을까 판단하였다.

BIOS 설정에서 가상화 목록을 껐다 켜서 레지스터를 초기화 해줬고, 마침내 멀쩡하게 구동이 가능해졌다. 이 곳에는 두 문단의 기록만 남았지만, 로키를 설치한 오전 11시 경 부터 현재시간 오후 11시 52분까지 약 12시간 가량을 컴퓨터와 싸웠고, 마침내 승리했다. 아무래도 내가 시스템 관련 지식이 부족했기에, 트러블슈팅에 소모되는 시간이 많이 걸렸던 것 같아. 그래도 하나 배웠다. 가상화에 문제가 있는 것 같으면 바이오스 세팅으로 호스트 설정을 초기화 해주는 것이 해법이 될 수도 있다.

</aside>

## 자, 이제부터는 서버 서비스를 시작해야 한다.

서버를 구축하려면, 모든 세팅은 루트의 권한으로 실행되어야 한다, 하지만 루트 계정 자체로 작업을 하게 되면, 세션 하이재킹과 같은 해킹의 상황에 최고 권한자가 그대로 털려서 최악의 상황을 야기할 수 있다. 그러므로 모든 세팅은, 사용자의 레벨에서 루트의 권한으로 설정하는 것이 정석이다.

<img width="720" height="637" alt="image" src="https://github.com/user-attachments/assets/2f764bc1-0cc8-4951-9ab2-cb92f9956626" />

우분투와 같이 sudo를 활용하여 작업을 진행하려고 하였는데, 안된다. 설명상 sudoers 파일에 bunny가 없다는 소리이다. 그렇다. 우분투는 계정이 생성되면서 sudo가 가능한 그룹으로 자동 배정되었었는데, 로키는 그렇지 않다. 그래서 bunny를 sudoers 그룹에 넣어줘야 한다.

<img width="720" height="637" alt="image" src="https://github.com/user-attachments/assets/50ee24d7-cb50-4ac5-8d27-ae82e069e5f7" />

<img width="720" height="637" alt="image" src="https://github.com/user-attachments/assets/a849aaa1-628d-4d96-b0ca-8e312e57be04" />

/etc/sudoers 파일에 bunny의 권한을 부여해준 것이다. 어떠한 상황에도 bunny는 sudo를 쓸 수 있게 된다.

<img width="411" height="97" alt="image" src="https://github.com/user-attachments/assets/951c7849-a8b4-4ec8-9975-20217f3a14bc" />

sudoers 내용 변경 후, bunny가 sudo를 사용하는 모습이다.

 

## 방화벽 설치해서 설정하기

오늘의 주된 목적 중 하나, 바로 방화벽을 설치하는 것이다.

<img width="720" height="637" alt="image" src="https://github.com/user-attachments/assets/1d1cfd74-5fa8-49e9-8be5-96d455f3b81c" />

설치되어 있는지 확인하는 방법은 간단하다. 해당 프로그램명을 그대로 입력해보면 된다. firewall-config를 사용해야 하는데, 지금 없다고 한다. 그렇다면 인스톨해야 한다.

<img width="720" height="637" alt="image" src="https://github.com/user-attachments/assets/153d963e-d279-4b7a-94ae-5a3d6c9bc967" />

<aside>
💡

yum은 관련 패키지 몽땅 설치(우분투의 apt),

-y 설정은 설치 명령의 is this ok? 질문에 미리 yes라고 답하는 설정

</aside>

<img width="579" height="512" alt="image" src="https://github.com/user-attachments/assets/2e1c45b4-718d-4bcd-b9af-bb07a0c2ebfd" />

설치가 완료되었다! 

<img width="720" height="637" alt="image" src="https://github.com/user-attachments/assets/0a6a8c82-83cd-4586-a6ff-9ebf5ae5044d" />

설치 전에 하나 확인했어야 하는 부분이 있다. /etc/resolf.conf의 DNS 설정이다. 이 것이 제대로 되어있어야 인스톨이 온전히 진행된다. 지금도 게이트웨이 주소로 잘 설정이 되어있지만, 하나에서 두 개 정도 더 추가해 주는 것이 좋다. 넘어가자.

자, 이제 설치된 파이어워를 열어보자

<img width="720" height="637" alt="image" src="https://github.com/user-attachments/assets/8f3e11c6-26d8-4d12-ba24-590df844ce38" />

<img width="893" height="871" alt="image" src="https://github.com/user-attachments/assets/68ce5d3c-c42b-44de-b2c4-dd707f829405" />

방화벽 프로그램을 실행한 모습이다. 오늘은 SSH를 사용할 것이다.

<img width="720" height="634" alt="image" src="https://github.com/user-attachments/assets/c6babf74-e9e1-4ada-a5e6-b4d79da00b79" />

ssh를 실행하였다. d를 붙여 데몬으로 실행하여 백그라운드에 대기시켰다. (서버만 d가 필요하다. 클라이언트는 딱 쓸 때만 필요한거라 굳이 백그라운드 실행이 아니어도 된다.)

<img width="720" height="634" alt="image" src="https://github.com/user-attachments/assets/230fff26-1899-424c-8cee-71b8989ffbe7" />

넷스탯으로 제대로 실행되었는지 확인한다.

<aside>
💡

-nltp는 서버 점검에 가장 많이 쓰이는 옵션

-n : 이름 말고 IP로(속도 향상)

-l : LISTEN 소켓 필터링(연결 대기)

-t : tcp 프로토콜인 녀석들만(u 쓰면 udp)

-p : PID도 함께

</aside>

이제는 ssh를 통해 다른 클라이언트의 접속을 시도해 볼 차례이다. 먼저, ssh를 서비스하는 다른 클라이언트를 찾아야 한다. 편하게 이전에 사용했던 우분투를 그대로 사용하도록 하자.

<img width="893" height="725" alt="image" src="https://github.com/user-attachments/assets/82549103-0bfc-4b7e-8aaa-071d274c46ab" />

우분투에는 ssh가 이미 설치되어있다. 바로 사용하면 된다.

<img width="893" height="725" alt="image" src="https://github.com/user-attachments/assets/54f49c4d-ace6-4ec7-9313-df7356cd4b71" />

로키 가상머신의 ip주소는 192.168.100.135이다. 이를 가지고 클라이언트는 로키 서버에 접속한다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/5f425004-b61c-4a0f-bd43-78c9798a7e7d" />

ssh bunny@192.168.100.135 명령어로 로키 서버 접속에 완료했다. 각각에 맞는 패스워드를 입력하면, 완벽하게 연결에 성공한다.

이제 서버에 원하는 프로그램을 설치해보자.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/017b7f48-d05b-4e41-bcd5-ae27d472ba4a" />

무섭다. 서버는 그저 sshd 하나 구동한 것 뿐이고, IP주소만 알려졌을 뿐인데, 클라이언트에서 접속하여 순식간에 nmap 설치를 완료했다. 이게 만약 바이러스였다면? 충분히 있을 수 있는 일이라고 생각한다. 이렇기에 관제가 중요한 것이다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/327c05f6-4a9a-4fe0-aeda-ffe518b308fa" />

상당히 무서운 일이다. 아무런 거침 없이 클라이언트는 서버의 중요 정보를 빼냈다. 단 한 줄의 명령어로. 심지어 접속과 cat 명령어를 한 번에 처리해서 접속 시간도 상당히 짧았다. 해킹은 이렇게 시작되었던게 아닐까?

하지만 서버도 아무것도 할 수 없는 것은 아니다. 일단 침입 탐지는 쉽게 가능하다.

<img width="720" height="634" alt="image" src="https://github.com/user-attachments/assets/b8982795-35c9-45c1-a16e-fe5cb605af9c" />

w 명령 하나만으로 외부에서 서버에 접속한 접속자를 알 수 있다.

<img width="720" height="634" alt="image" src="https://github.com/user-attachments/assets/f647a2a9-d3c6-4d21-9bfb-96fcc5cc88b8" />

자, 이제 다시 클라이언트에서 서버로 접속해보자.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/6a78ed08-9830-4194-9b38-2e460f6b71ec" />

<img width="720" height="634" alt="image" src="https://github.com/user-attachments/assets/44074d34-cd2b-45b5-994a-1e80d43331bf" />

유저 네임은 bunny이나 본인이 아닌 다른 IP주소로부터 온 접속이 존재하는 것이다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/8c9e32f4-198d-4f8e-bef2-2212399f2abc" />

클라이언트의 tty 터널 1번을 사용중이고, 그 내용이 서버에도 고스란이 적혀있다.

그렇다면, 이 양심 없는 클라이언트의 연결을 서버에서 끊어버릴 방법이 없을까? 당연히 존재한다.

<img width="720" height="634" alt="image" src="https://github.com/user-attachments/assets/620f7adb-cc47-4b63-a26c-f2f9098ef62b" />

<aside>
💡

-e : every, -f : full >> 전부 상세히

</aside>

<img width="720" height="634" alt="image" src="https://github.com/user-attachments/assets/e17dd368-506c-43af-b966-303afdbeffe4" />

ps 명령으로 침입한 클라이언트의 프로세스를 찾았다.

PID는 42636, PPID는 42632이다. 이 부분을 알고 있으면, kill 명령어로 프로세스를 다운시킬 수 있다.

<img width="720" height="634" alt="image" src="https://github.com/user-attachments/assets/bf9352cd-7536-44a2-8b86-b5378a3f5011" />

이런 식으로 사용한다.

<img width="720" height="634" alt="image" src="https://github.com/user-attachments/assets/751bd0c9-9635-4c7e-a154-a630b54e01e0" />

명령어 진행 후 ps 재조회 했을 때, 침입 프로세스가 사라진 모습이다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/a9508691-a164-4320-8370-81511458b002" />

클라이언트로 들어가봐도 시원하게 까인 모습이다.

오늘은 레드햇 계열의 로키 운영체제에 방화벽 설정을 하고 또 SSH를 통해 클라이언트에서 서버로  직접 접속해보는 경험을 했다. 해킹은 절대 이렇게 쉬운 방향으로 흘러가지 않을 것이라는걸 알지만, 그래도 마치 내가 해커가 된 것 마냥 신나고, 또 재미있었다. 문제를 하나하나 해결하는 것에 희열도 있고, 너무 즐거웠다.
