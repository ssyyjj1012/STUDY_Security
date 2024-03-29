# MOV와 LEA 명령어 비교
## MOV
좌변에 우변(혹은 상수)의 값을 입력하는 것이고, lea는 좌변(레지스터만 가능)에 우변의 주소값을 입력하는 것이다.
<br></br>
먼저, mov 명령어에 대하여 설명하겠다.
<br></br>
> mov eax, dword ptr ss:[ebp-4];

위는 eax는 ebp-4 메모리 주소에 존재하는 값을 dword ptr에 의해 4byte 값을 읽어 입력되는 것을 의미한다.
<br></br>

#### mov : 값을 입력하는 것으로, mov eax,12345(상수) 문장은 성립 가능하다
> mov dword ptr ss:[esp-4], 12345;

> mov dword ptr ds:[0x00560033], 12345;
     
** 좌변에는 레지스터 뿐만 아니라 지역 변수나 전역 변수도 모두 올 수 있다.

## LEA
이번에는 lea 명령어에 대하여 설명하겠다.
<br></br>
>lea eax, dword ptr ss:[ebp-4]

이런 식으로 lea의 좌변은 레지스터만 올 수 있으며, EAX에는 EBP-4가 들어갈 것이다.
<br></br>
위의 명령어를 mov를 사용해도 같은 효과를 낼 수가 있는데, 이를 고치면 주소값을 입력하는 데 2줄의 명령어가 만들어진다.
<br></br>
> mov eax, ebp

> sub eax, 4

<br></br>
lea 명령의 탄생배경이 위와 같이 두 줄 연산의 번거로움을 없애고자 하는 데 있는 것이라고 한다.

**[esp-8]** 처럼 주소값을 의미하는 내에서 [ ] 안에서만 저런 표현은 가능하다.

lea의 우변은 주소값을 가져야 하므로 절대 상수는 올 수 없다.

- 성립 불가 : lea eax, 12345
- 성립 가능 : lea eax, dword ptr ds:[0x00567800] (전역변수) 

**　이 경우 메모리 주소인 0x00567800이 eax에 입력된다.
