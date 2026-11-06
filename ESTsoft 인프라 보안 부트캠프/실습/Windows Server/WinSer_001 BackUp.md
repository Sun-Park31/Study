# WinSer BackUp

오늘은 윈도우 서버를 백업해볼 것이다!

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/adf22aea-9986-44d2-9f98-47551903dc71" />


먼저 윈도우 서버를 켜준다!

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/089a6ef6-52c0-4d54-bbf0-b8b9668d39d3" />


가장 먼저, 백업 기능을 활성화 하기 위해 관리도구의 서버 관리자로 들어간다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/ab55a6f9-0a87-4546-9e63-8d2812e3dfa0" />


<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/9e47b42f-4ca0-4f75-8b99-28398c94ea62" />


이 곳의 윈서버 백업 기능을 설치하면 된다.

설치가 완료되었으면 머신을 종료하고, 하드디스크를 하나 추가한다. 백업본은 보통 리스크를 최소화 하기 위해서 다른 디스크에 저장한다.

<img width="759" height="734" alt="image" src="https://github.com/user-attachments/assets/726fc5a9-cb7b-4690-9f89-4f066fd74728" />


Add를 눌러 하드를 1개 추가하였다. 이제 다시 머신을 파워온 하여 서버관리자의 저장소-디스크 관리로 들어간다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/a958c274-5c87-43bc-a760-f11908b3e9ef" />


디폴트값으로 넘긴다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/92b9f105-65ae-4d25-abae-5ed8dcbaf235" />


디스크 0은 원래 설정되어있던 하드이고, 디스크 1은 우리가 방금 새로 만든 하드이다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/4f094bf2-2e77-4225-9186-ca18875f2885" />


먼저 오프라인인 디스크를 온라인으로 바꿔주고,

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/81bf2f7a-740a-4cad-9940-1af772322161" />


새 단순 볼륨으로 설정해준다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/4e8d9353-9803-46f3-9b57-ce41d5ca2153" />


<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/2d8668ab-ea27-4bae-a854-2f5f31bd29ae" />


이러한 설정값으로 지정해주면 된다. (볼륨 레이블은 백업을 위한 디스크이므로 BAK로 지정해줬다.)

이렇게 디스크 설정은 완료했다. 이제 본격적으로 윈도우 서버의 백업을 진행해보자. 먼저, 관리도구의 윈도우서버 백업을 찾아 들어간다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/f2615140-0766-4a90-8b0b-bad39048a353" />


<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/29882a77-b125-4e35-8faa-f1f90a0bf235" />


백업에는 3가지의 종류가 있다. 전부를 백업하는 풀백업, 증가값만 백업하는 증분백업, 차이를 백업하는 차등백업.

오늘은 풀백업과 증분백업을 해볼것이다.

윈서버의 백업 기본값은 풀백업이다. 우측의 한 번 백업을 누르면 진행할 수 있다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/2de23805-83b2-4810-a780-dd437925e052" />


<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/598b2b65-9889-40b5-b7d1-dd5d534d3962" />


대부분을 디폴트값으로 지정한다. 백업 구성은 본래의 하드이고, 백업 대상은 새로 만든 하드임을 유의하며 설정하자.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/505eccc7-ea28-46e8-a2de-0dd01b498aa4" />

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/a8cc0d3a-d633-4da7-bfd6-c80d06ed1649" />

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/8c151073-ba09-4b7b-a7fe-e79c417b40b4" />


백업이 예쁘게 잘 되었다. 이번에는 복구를 해보겠다. 이를 위해서 임의의 폴더를 하나 삭제한다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/9761b5f6-2b3a-4208-9fec-017653cbbe4a" />


커먼 파일즈를 날렸다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/46f5a9af-3a24-4941-afd1-b8ea16edfca5" />


복구를 시도해보자.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/04d59de7-a951-4956-8b8b-7455a9d9df03" />


복구할 항목을 선택하였다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/29e2474f-a2e2-450b-b0d3-2bea0c8ea803" />


<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/38a9cb0b-608c-4d31-8a91-e60f3a27d2d1" />


복구 완료.

이번에는 증분 백업을 해보도록 하자. 증분백업은 풀백업분이 먼저 있어야 한다. 풀백업을 먼저 하고, 증분백업을 실행하도록 하자.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/258218bb-332b-4a82-b23d-896ed4dcac89" />


동작의 성능 설정 구성으로 간다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/b4bbd9bc-9e70-4e26-91ff-9fa0c341891a" />


로컬 C를 증분 백업으로 바꿔준다. 그리고 한 번 백업을 아까와 같이 실행한다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/3fde48a9-267c-45f9-837d-82d5da21cb5f" />


자, 아까의 백업분에 데이타를 추가해야한다. 바탕화면에 적당히 만들어준다. 그리곤, 다시 한 번 백업을 진행한다. 진행 방식은 똑같다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/13174bb8-54b7-4f38-86ed-8980ba26730b" />


아까의 크기와는 확연히 다른 용량의 데이터만 백업되었다. 바탕화면에 txt 파일만 2개를 추가했기 때문에, 용량이 절대적으로 작다.

마지막으로 스케쥴러로 백업 일정을 예약해보겠다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/358f9728-ee27-4271-9b99-3097aa99e45b" />


백업일정을 눌러주면 된다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/88b5aebf-3fe1-4960-95a5-8e76e8de2182" />


디스크 추가를 해야 한다. 그래야 백업 대상 설정이 가능하다.

이 과정을 거치면 된다.

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/5c4514f3-23bd-431f-b268-a46a97c2a679" />

<img width="804" height="714" alt="image" src="https://github.com/user-attachments/assets/b8895092-fea3-4f8c-b97e-cd4417175eca" />


이 화면이 뜨면 성공이다.

오늘은 윈도우서버 백업을 해봤다. 나중에 컴퓨터를 한 번 싹 밀고 난 뒤에, 스케쥴을 걸어놓고 새벽에 구동되게 셋팅한다면, 조금 더 효율적인 컴퓨터 사용이 되지 않을까 싶다.
