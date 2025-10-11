AUTOSAR
==
# 1. autosar란?

AUTOSAR(AUTomotive Open System ARchitecture)는 자동차 소프트웨어 개발의 표준화를 위해 만들어진 개방형 아키텍처입니다.

자동차의 전자제어장치(ECU)에 들어가는 소프트웨어를 개발하고 관리하는 방식을 표준화하여, 여러 자동차 제조사와 부품 공급업체가 소프트웨어를 쉽게 공유하고 재사용할 수 있도록 하는 것이 핵심 목표  

기능(소프트웨어)과 제어기(하드웨어)를 완전히 분리해서 개발하고,  

마치 스마트폰에 앱을 설치하듯이, 만들어진 소프트웨어 기능들을 원하는 제어기에 쏙쏙 집어넣는 방식입니다.

## 1-1. autosar도입된 이유

<img width="1056" height="430" alt="image" src="https://github.com/user-attachments/assets/df3c835f-334d-47a8-8cad-5539d72e8183" />

점점 복잡해지고 비효율적으로 변하는 자동차 소프트웨어 개발 환경을 바로잡고,  

소프트웨어의 재사용성을 높여 개발 비용과 시간을 줄이기 위한 표준 규격으로 AUTOSAR가 등장  

## 1-2. 어떻게 중간다리 역할을 하나?

AUTOSAR는 애플리케이션(SWC) → 가상 통신망(RTE) → 표준 서비스(BSW) → 하드웨어 통역사(MCAL) 순서로 역할을 철저히 분담합니다.  

각 계층은 정해진 약속(인터페이스)으로만 대화하기 때문에, 맨 위에 있는 애플리케이션은 하드웨어가 어떻게 생겼는지 전혀 몰라도 되는 것입니다.   

그래서 특정 하드웨어가 바뀌면 그 하드웨어와 직접 대화하는 맨 아래 계층(MCAL)만 교체해주면, 그 위에 있는 모든 소프트웨어는 코드 수정 없이 그대로 재사용할 수 있게 됩니다.  

# 2. autosar의 layer


<img width="1214" height="619" alt="image" src="https://github.com/user-attachments/assets/4ba16b99-6eeb-4d71-99e4-94191b03f1cf" />


<img width="1245" height="660" alt="image" src="https://github.com/user-attachments/assets/a816ede3-99f4-4946-bfb4-a072a34fa815" />

## 2-1. AUTOSAR Application

ECU들에는 component들이 존재하고, 각 component들 안에는 실제 기능을 구현하기 위한 러너블들이 존재. 러너블들은 어떤 트리거 이벤트에 의해 트리거되어 실행됨.  

주기 이벤트 혹은 초기화 이벤트, 데이터 수신 이벤트 등 트리거 조건들을 설정할 수 있음. 또한, 트리거된 러너블들이 실행될 때는 OS Task에 매핑되어 동작함.  

마지막으로, software component들 간의 communication은 ECU내부, 외부 커뮤니케이션인지 고려하지 않고, RTE에게 요청하여 커뮤니케이션이 이루어지게 됨.  
****
구조: ECU > Component > Runnable  
자동차 소프트웨어의 구조는 마치 회사 조직도와 같습니다.  

- ECU: 하나의 '부서'

- 소프트웨어 컴포넌트(SWC): 부서 내의 '팀'

- 러너블(Runnable): 실제 업무를 수행하는 '팀원'

  하나의 ECU(부서) 안에는 여러 개의 SWC(팀)가 존재할 수 있고, 각 SWC(팀)는 특정 임무를 수행하는 여러 러너블(팀원)들로 구성됩니다.
****
실행: Event와 OS Task
'팀원(러너블)'은 아무 때나 일하는 것이 아니라, 명확한 **'업무 지시(Event)'**가 있을 때만 움직입니다.

- 이벤트 (Event) 기반 실행: 러너블을 실행시키는 '업무 지시'에는 다음과 같은 종류가 있습니다.

  - 주기 이벤트 (Timing Event): "10ms마다 한 번씩 보고해!"

  - 초기화 이벤트 (Init Event): "업무 시작할 때 딱 한 번만 실행해!"

  - 데이터 수신 이벤트 (Data Received Event): "다른 팀에서 자료가 도착하면 바로 확인해!"

- OS 태스크 (Task) 매핑: 이렇게 업무 지시를 받은 러너블들은 AUTOSAR OS가 관리하는 **'집중 근무 시간(Task)'**에 배정되어 실행됩니다. OS는 프로젝트 매니저처럼 여러 러너블의 실행 순서와 주기를 관리하여 ECU의 자원을 효율적으로 사용합니다. 하나의 태스크 안에 여러 러너블이 묶여서 함께 실행될 수도 있습니다.
****
통신: RTE의 역할
'팀(SWC)' 간의 소통은 **'사내 메신저/비서(RTE)'**를 통해서만 이루어집니다.

- 위치 투명성 (Location Transparency): A 컴포넌트가 B 컴포넌트에게 데이터를 보낼 때, B가 같은 ECU(내부 통신)에 있는지 다른 ECU(외부 통신)에 있는지 전혀 신경 쓸 필요가 없습니다.

- RTE의 중계: 그냥 "RTE, 이 데이터 좀 B한테 전달해줘"라고 요청만 하면, RTE가 알아서 내부 통신으로 처리할지, CAN이나 이더넷 같은 외부 통신으로 보낼지를 결정하고 실행합니다.

이러한 구조 덕분에 개발자는 하드웨어의 복잡한 구조나 통신 방식은 신경 끄고, 오직 소프트웨어의 기능 로직 개발에만 집중할 수 있게 됩니다.

## 2-2. AUTOSAR RTE
## 2-2-1. RTE의 기본 역할과 특
<img width="933" height="566" alt="image" src="https://github.com/user-attachments/assets/795b0c4b-c0e1-450a-9c8c-30d11a153299" />

ECU 내부, 외부 통신을 담당하는 미들웨어  

- 실행 지시: 어떤 기능을(러너블) 언제 실행할지 결정하고 OS에 지시합니다.  

- 통신 중계: 모든 소프트웨어 부품들 간의 데이터 교환을 도맡아 처리합니다.  

- 보호막 역할: 애플리케이션이 OS나 하드웨어 제어 SW에 직접 접근하는 것을 막아주는 안전장치입니다.
****
  SWC끼리 커뮤니케이션 필요할 때는 SWC가 RTE에게 요청. RTE는 SWC간의 커뮤니케이션(목적: 데이터 교환), SWC와 BSW끼리의 커뮤니케이션(BSW에게 서비스 요청) 제공
****
- AUTOSAR (전체 설계도):

  - Application Layer (앱)

  - RTE (중간 관리자)

  - BSW (기반 소프트웨어)


## 2-2-2. RTE를 이용한 커뮤니케이션: Sender/Receiver, client/Server communication
<img width="313" height="334" alt="image" src="https://github.com/user-attachments/assets/2b264187-d32d-4926-b66d-018ac713ba6f" />

RTE가 외부 통신이 필요한지 판단하는 기준은 데이터 매핑 설정 정보를 기준으로 판단.  
****
Sender/Receiver communication  
- direct(explicit): "지금 값 줘"라고 직접 요청해서 즉시 받는 1:1 통신.    
- buffered(implicit): 최신 값 하나만 자동으로 덮어쓰며 유지되는 방식 (이전 값은 무시됨).     
- queued: 모든 데이터를 순서대로 차곡차곡 쌓아놓고 하나씩 처리하는 방식 (데이터 손실 없음).  
****
Client/Server communication  

클라이언트 (손님): 서버에게 특정 작업을 해달라고 요청합니다.  
서버 (요리사): 요청받은 작업을 수행하고 결과를 돌려줍니다.  

호출 방식:
- 동기 (Synchronous): 요청 후 결과가 올 때까지 기다립니다.
- 비동기 (Asynchronous): 요청만 하고 기다리지 않고 바로 다음 일을 합니다.
****
**문제**: 경합 상태 (Race Condition)  
여러 기능(러너블)이 하나의 공유 변수에 동시 접근 시, 실행 순서에 따라 데이터가 오염되는 문제.  

**해결책**  
Exclusive Area (EA):  
코드 블록 전체를 잠금(Lock)하여, 여러 줄의 연산이 중간에 방해받지 않도록 보장합니다.  

Inter-Runnable Variable (IRV):  
단일 변수에 대한 접근을 RTE가 제공하는 안전한 전용 읽기/쓰기 함수로만 제한합니다.   
****
RTE의 부가적인 기능 Multiple Instantiation: 붕어빵. 하나의 붕어빵틀로 수많은 붕어빵을 계속해서 찍어냄

# 2-2-3. AUTOSAR Interface
Client/Server 포트, Sender/Receiver 포트가 autosar interface에 해당  
user가 직접 인터페이스를 정의해야 하고, 실제로 코드를 구현할 때 코드 내에서 어떤 시점에 커뮤니케이션을 할지도 고려해야 함  

1. AUTOSAR Interface (일반 포트)
목적: 애플리케이션(SWC)끼리 서로 데이터를 주고받거나 기능을 호출하기 위해 사용합니다. 가장 일반적인 소통 방식입니다.

특징:

Port 기반: 통신 대상을 명확히 지정하기 위해 포트(Port)를 사용합니다.

RTE 함수 사용: Rte_Write, Rte_Read, Rte_Call 등 RTE가 제공하는 표준 함수를 통해 통신합니다.

2. Standardized Interface (BSW 내부 API)
목적: RTE가 BSW(OS, 통신 드라이버 등)의 내부 기능을 직접 제어하기 위해 사용합니다. 시스템의 기반을 다루는 내부 규칙입니다.

특징:

직접 함수 호출: 포트가 아닌 Com_SendSignal 같은 표준 C언어 함수(API)를 직접 호출합니다.

애플리케이션 접근 불가: 앱 개발자는 이 인터페이스에 절대 직접 접근할 수 없으며, RTE만 사용할 수 있습니다.

3. Standardized AUTOSAR Interface (서비스 포트)
목적: 애플리케이션(SWC)이 AUTOSAR 표준으로 미리 정해진 BSW의 공용 서비스(진단, 메모리 관리 등)를 사용하기 위해 사용합니다.

특징:

서비스 포트 사용: BSW의 표준 서비스를 호출하기 위한 전용 포트인 '서비스 포트'를 사용합니다.

앱 친화적: 애플리케이션 입장에서는 마치 다른 SWC의 기능을 호출하는 것처럼, 동일하게 Rte_Call 함수를 사용하여 BSW의 고급 기능을 쓸 수 있습니다.

****
  
<img width="728" height="307" alt="image" src="https://github.com/user-attachments/assets/681c39ae-942a-4309-b201-aaf26fd09132" />

****
SWC (소프트웨어 컴포넌트) = 부서장 (Manager)   
BSW (기반 소프트웨어) = 실무 직원 (Employee)   
RTE = 개인 비서 (Assistant)

## 2-3. AUTOSAR BSW
<img width="920" height="511" alt="image" src="https://github.com/user-attachments/assets/58253d61-eb02-4a81-8e4b-1ce6ca5429e5" />

### 2-3-1. Service Layer
진단, 메모리, 워치독, 커뮤니케이션 등의 기능들 제공하는 레이어.  

### 2-3-2. ECU Abstraction Layer
제어기를 추상화하는 레이어. 하드웨어 의존적인 코드와 상위 소프트웨어를 분리시켜 줌. 상위 계층의 소프트웨어가 ECU하드웨어에 의존하지 않도록 만들어줌.  

MCU를 제외한 주변 하드웨어, 칩, 드라이버 등이 이에 해당함.  

### 2-3-3. Microcontroller abstraction layer
상위계층을 마이크로컨트롤러로부터 독립적인 개발환경으로 만들어줌.  

### 2-3-4. Complex Device Drivers
보통 CDD라고 표현하며, 일반적인 어플리케이션 SWC로 처리하기 어려운 복잡한 센서, 엑츄에이터를 제어하기 위해 사용하는 특수한 SWC를 의미.  

BSW위치에 위치함. 

### 2-3-5. Communication모듈
<img width="205" height="470" alt="image" src="https://github.com/user-attachments/assets/56fad7e2-2067-4533-8174-4b6645b97144" />

1. COM (Communication)
역할: 데이터 포장 전문가 📦

설명: 애플리케이션이 보내려는 '엔진 온도=95'와 같은 개별 정보(신호, Signal)들을 받습니다. 그리고 이 정보들을 **PDU(Protocol Data Unit)**라는 표준 규격의 '데이터 상자'에 담고 포장하는 역할을 합니다. 애플리케이션과 가장 가까이서 소통하는 창구입니다.

2. PDU Router (PDUR)
역할: 중앙 교통 관제소 🚦

설명: COM이 포장한 데이터 상자(PDU)를 받아서, 이 상자를 어떤 도로(CAN, 이더넷 등)로 보낼지 결정하고 경로를 지정해 줍니다. 상자 안에 무엇이 들었는지는 신경 쓰지 않고, 오직 '어디로 보낼지'만 담당하는 핵심적인 길잡이입니다.

3. Transport Protocol (TP)
역할: 대형 화물 분할 담당 쪼개기

설명: 한 번에 보내기엔 너무 큰 데이터 상자(PDU)가 들어왔을 때, 이를 전송 가능한 여러 개의 작은 조각으로 나누어 순서대로 보냅니다. 받는 쪽에서는 이 조각들을 다시 원래의 큰 상자로 재조립합니다. 주로 진단 데이터나 소프트웨어 업데이트처럼 용량이 큰 데이터를 보낼 때 필수적입니다.

4. IPDU Multiplexer (IPDUMux) - (선택 사항)
역할: 주소 절약을 위한 트릭 📮

설명: 똑같은 주소(CAN ID)를 사용하지만, 상황에 따라 서로 다른 종류의 데이터 상자를 보내고 싶을 때 사용합니다. 상자 안의 특정 표시를 보고 "아, 이번엔 A 종류의 데이터구나" 하고 구분할 수 있게 해주는 특별 기능입니다.

5. Interface
역할: 특정 하드웨어에 종속되지 않도록 공통된 인터페이스를 상위계층에 제공하여 상위모듈은 하드웨어 종류를 몰라도 통신이 가능하게 만들어주면서  

각 버스특성에 맞는 기능도 제공해주는 모듈.  

하위에 드라이버 API를 호출해주는 역할.  

6. Driver
하드웨어를 직접 제어. 상위 모듈이 통신을 사용할 수 있도록 지원. CAN controller의 레지스터 직접 제어, 초기화, 버퍼 관리, 인터럽트 처리를 위한 IXR구현해야 함.

7. Transceiver
하드웨어 회로의 전기적 신호를 생성, 감지하여 DAC 변환

****
application이 RTE에게 데이터 송신을 요청하는 상황에서 ECU 외부로 송신해야 하는 경우 흐름. 
-
<img width="479" height="570" alt="image" src="https://github.com/user-attachments/assets/e1f1fa85-dbf3-425e-aa86-20bb4f5c6671" />

송신:  
어플리케이션에서 시그널 단위로 송신 요청을 하면 COM모듈은 시그널들을 모아 PDU 버퍼에 저장.  

PDU는 PDU 라우터로 전달되어, 즉시 보내질 수도 있고 설정된 주기에 맞추어 보내질 수도 있음.  

PDU는 각각의 아이디가 있어 구분될 수 있음. PDU라우터는 해당 PDU가 어떤 버스를 통해 송신되어야 하는지 판단해서 해당 버스의 인터페이스 모듈로 전달.  

인터페이스 모듈은 어떤 신호를 사용해 송신할지.  

CAN driver는 메시지 우선순위를 고려하여 가능한 빨리 메시지 전송. 

수신:  
수신처리는 인터럽트 또는 폴링 방식으로. 인터럽트 방식은 수신해야 할 메시지가 있으면 하드웨어가   

상위계층에 알린후 처리. 폴링은 주기적으로 모니터링하면서 수신처리해야할 메시지가 있는지 확인.  

외부 ECU에서 보낸 메시지는 can버스를 통해 전달되고, can컨트롤러가 인터럽트를 발생시켜 can드라이버가 수신된 메시지를 읽음.   

데이터를 전달받은 can 인터페이스는 PDU라우터에게 전달하고, PDU라우터는 해당 메시지가 상위의 COM 모듈로 가야하는지 CAN TP로 가야하는지 판단.    

만약 COM 모듈로 전달되면 COM 모듈은 PDU에서 시그널 추출. 최종적으로 RTE에서 시그널을 읽어감.    

### 2-3-6. Mode Management 모듈

<img width="468" height="503" alt="image" src="https://github.com/user-attachments/assets/85359e7f-f36d-4104-be03-4feac5d19727" />

1. EcuM 모듈
ECU의 전체적인 상태처리. 제어기의 시작과 끝을 관리.
2. ComM 모듈
통신상태 관리.
3. NM 모듈(Network Management)
통신을 위해 버스를 활성화시키거나 셧다운.
4. bus state manager
bus 통신 상태 관리.
5. Basic software mode manager
BSW의 유저가 설정한 규칙 기반으로 BSW의 동작 제어.

### 2-3-7. Watchdog
software가 정상적으로 실행되고 있는지 감시. 일반적으로 모니터링 대상이 정상적으로 동작하면, watch trigger가 주기적으로 발생하여  

시스템이 정상적으로 수행되고 있음을 알림. 이상이 생기면 트리거 발생x. 시스템 리셋 유도하게 됨.   

watchdog driver는 hardware watchdog을 제어. watchdog interface통해 명령을 받음. 

### 2-3-8. Memory Services
autosar를 적용하여 제어기를 개발하다보면 다양한 종류의 메모리를 사용해야 함. 어떤 종류의 메모리든 동일한 방식으로 접근하여 사용할 수 있도록 추상화된 구조 제공하는 역할.  

인터널 메모리인지, 익스터널 메모리인지 위치에 상관없이 동일한 방법으로 접근하여 개발자가 편리하게 코드를 작성할 수 있도록 추상화. 유지 보수성 확대.  

메모리 드라이버는 실제 하드웨어를 제어하기 위한 드라이버. MCU에 따라 다르게 구현됨. 하드웨어 종속적.  

### 2-3-9. 진단 관련 모듈
<img width="285" height="532" alt="image" src="https://github.com/user-attachments/assets/3b0b43f4-75d4-4473-8075-b1c348daf532" />

DCM은 진단 통신 프로토콜 구현해놓은 모듈. 외부 진단 장비와 ECU간의 통신을 처리.  

진단 요청에 대한 수신 및 응답처리, 서비스 ID에 따른 기능 수행, 세션 관리 등을 담당.  

DEM은 error event, 즉 DTC를 관리하는 모듈.   

FIM은 특정 진단 이벤트가 발생했을 때 사용. DEM으로부터 전달받은 event의 상태를 기반으로 기능의 실행 여부에 대한 명령 부여.  

오류가 발생하면 오류 발생 당시 상태를 스냅샷으로 저장. 

### 2-3-10. 하드웨어 관련 모듈
autosar는 IO를 위한 주변장치가 MCU 내부에 존재하든 외부에 존재하든 추상화 제공. 센서나 액츄에이터, 즉 하드웨어 자체의 추상화가 아니라 IO신호에 대한 인터페이스를 제공.  

IO를 제어하기 위해 다양한 하드웨어 드라이버 모듈을 제공. 

### 2-3-10. OS
static operationg system. 태스크나 우선순위, 자원 등이 툴 설정을 기반으로 하여 런타임 도중 태스크를 추가하거나 삭제하지 않음.  

task, event, alarm, interrupt등이 구성요소.

## 2-4. AUTOSAR 개발 툴
- 아키텍쳐를 설계하는 툴
Prevision: 소프트웨어 컴포넌트에 대한 설계, 네트워크 설계, 와이어링 하네스에 대한 설계까지 가능.
Virtual target pro: 가상의 환경에서 ECU 구성 SWC 실행시켜 문제가 없는지 찾아내 시뮬레이션.
다빈치 디벨로퍼: 소프트웨어 컴포넌트의 내부 동작 정의하거나 SWC의 커뮤니케이션에 필요한 인터페이스 정의. ECU SWC를 설계할 때 사용.
다빈치 configurator pro: 주요 역할은 ECU의 기반 소프트웨어(BSW)와 RTE를 설정하고, 그 설정값에 맞는 코드를 자동으로 생성하는 것입니다.
CANoe.AMD: 별도의 툴이 아님. CANoe를 이용해 실시간으로 ECU내부 상태를 모니터링. 
