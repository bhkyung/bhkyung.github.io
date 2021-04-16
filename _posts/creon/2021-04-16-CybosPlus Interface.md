---
title:  "CybosPlus Interface"
search: true
categories:
  - creon
toc: true
toc_label: "목차"
sidebar:
  title: "Creon-Plus"
  nav: sidebar-creon
---
<style>
H3{color:Blue !important;}
</style>
### Method
<table>
  <thead>
    <tr>
      <th></th>
      <th>RQ/RP</th>
      <th>SB/PB</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Data Input</td>
      <td colspan="2">object.SetInputValue (type, value)
type에 해당하는 입력데이터를 Value 값으로 지정한다.
type : 입력데이터 종류
value : 새로 지정할 값</td>
    </tr>
    <tr>
      <td>통신요청 (하단 각각 비교 설명 참조)</td>
      <td>object.Request()
ret = object.BlockRequest ()
ret = object.BlockRequest2 (short option)
3가지 중에 선택 1</td>
      <td>object.Subscribe()
object.SubscribeLatest()
2가지 중에 선택 1</td>
    </tr>
    <tr>
      <td>Data Get</td>
      <td colspan="2">value = object.GetHeaderValue ( type )
type에 해당하는 헤더데이터를 반환한다.
type : 데이터 종류
반환값 : 데이터 종류에 해당하는 값
value = object.GetDataValue ( type, index )
type : 데이터 종류
index : 데이터 인덱스
반환값 : 데이터 종류의 index번째 데이터</td>
    </tr>
  </tbody>
</table>

|                                                              | **RQ/RP**                                                    | **SB/PB**                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data  Input**                                              | object.**SetInputValue** (type, value)<br/>  type에 해당하는 입력데이터를 Value 값으로 지정한다.<br/>  type : 입력데이터 종류<br/>  value : 새로 지정할 값 |                                                              |
| **통신요청 (하단 각각 비교 설명 참조)** | object.**Request**()<br/>ret = object.**BlockRequest** ()<br/>ret = object.**BlockRequest2** (short  option)<br/>3가지 중에 선택 1 | object.**Subscribe**()<br/>object.**SubscribeLatest**()<br/>2가지 중에 선택 1 |
| **Data  Get**                                                | value = object.**GetHeaderValue** ( type )<br/>   type에 해당하는 헤더데이터를 반환한다.<br/>  type : 데이터 종류 <br/>반환값 : 데이터 종류에 해당하는 값 <br/>value = object.**GetDataValue** ( type, index )<br/>  type : 데이터 종류<br/> index : 데이터 인덱스<br/> 반환값 : 데이터 종류의 index번째 데이터 |  

|    <!-- -->          |        <!-- -->                     |
|----------------------|-------------------------------------|
| object.**GetDibStatus** | DIB 통신상태 (읽기전용)<br/>  반환값 :<br/>  -1 - 오류<br/> 0 - 정상<br/> 1 - 수신대기.<br/>  오류(-1) , 정상(0) 상태에서는 데이타 요청 가능.<br/> 수신대기(1) Request를 요청하고 아직 Received 이벤트를 받지 않은 상태의 오브젝트로 다시  Request/BlockRequest/BlockRequest2를 호출한 경우에 발생 |
| object.**GetDibMsg1**     | DIB 통신결과 메시지 문자열 (읽기전용)<br/>  반환값 : 결과 메시지 문자열 |
| object.**GetDibMsg2**     | **사용안함**                                                 |

### Property

|    <!-- -->          |        <!-- -->                     |
|----------------------|-------------------------------------|
| object.**Continue** | 연속 데이터 유무를 나타내는 프로퍼티. (읽기전용)<br/>  반환값 :<br/> 1 - 연속 데이터 있음.<br/> 0 - 연속 데이터 없음. |
| object.**Header**   | Header 컬렉션 루트 객체를 반환한다.<br/>  Header 컬렉션에는 Header 정보의 종류와 이름이 들어있다.(읽기전용)<br/>  반환값 : Header 컬렉션 객체. |
| object.**Data**     | Data 컬렉션 루트 객체를 반환한다.<br/>  Data 컬렉션에는 Data 정보의 종류와 이름이 들어있다.(읽기전용)<br/>  반환값 : Data 컬렉션 객체. | 

### Event
object.**Received**

데이터를 수신했을 때 발생하는 이벤트 

### BlockRequest/Blockrequest****2****/Request****의****리턴값

|                  | **BlockRequest/BlockRequest2**                               | **Request** |
| ---------------- | ------------------------------------------------------------ | ----------- |
| 시세오브젝트     | 리턴값<br/>0: 정상 요청<br/>1: 통신요청 실패<br/>3: 그외의 내부 오류            | 리턴값 없음  |
| 주문관련오브젝트 | 리턴값<br/>0: 정상 요청<br/>1: 통신요청 실패<br/>2: <span style= "color:Blue !important;"> 주문 확인창에서 취소</span><br/>3: 그외의 내부 오류<br/>4: 주문 요청 제한 개수 초과 | 좌동        |

 

### 요청제한

사용자의 고의 또는 실수(무한루프등...)로부터 서버 및 다른 사용자들을 보호하기 위하여 시세요청(RQ)과 실시간요청(SB)에 대해 제한을 두고 있습니다.

|                  | **RQ**  **제한**                                             | **SB**  **제한**                       |
| ---------------- | ------------------------------------------------------------ | -------------------------------------- |
| 시세 오브젝트     | 15초에 최대 60건으로 제한<br/>초과 요청 시 첫 요청으로부터 15초가 지날 때까지 내부적으로 기다림 | 최대 400건의 요청으로 제한<br/>초과 요청 시 오류 |
| 주문 관련 오브젝트 | 15초에 최대 20건으로 제한<br/>초과 요청 시 첫 요청으로부터 15초가 지날 때까지 요청 함수(Request, BlockRequest, BlockRequest2)에서 4를 반환 | 제한없음                               |

위의 제한사항은 당사방침에 따라 변경될 수 있습니다.

CpCybos의 LimitRequestRemainTime과 GetLimitRemainCount로 타임아웃까지 남은 시간과 남아 있는 요청 개수를 얻을 수 있습니다.

 

### BlockRequest와 BlockRequest2 비교

예를 들어 설명하겠습니다. 다음과 같은 예가 있습니다.
(a) BlockRequest하는 도중에 다른이벤트(Received,마우스클릭 등) 처리 안에서

다른 (b)BlockRequest가 있다고 가정할 경우

|      | **BlockRequest**                                 | **BlockRequest2**                                            |
| ---- | ------------------------------------------------ | ------------------------------------------------------------ |
| 설명 | (b)의  BlockRequest가 우선 처리                   | option 인자에 따라 기능이 다름<br/> - option이 0 :  BlockRequest와 같은 기능<br/> - option이 1:  요청한 순서대로 (a)의 BlockRequest2가 먼저 수행됩니다. |
| 특징 | 이벤트에서 요청할 RQ를 우선적으로 처리할 경우 유리함 | 순차적으로 RQ를 요청할 경우 유리함 통상적인경우 BlockRequest2 사용을 추천함 |

 

### Subscribe와 SubscribeLatest 비교

시세 변동의 이벤트는 내부에서는 배열로 처리하고 있습니다.

|        | **Subscribe**                                                | **SubscribeLatest**                                          |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 설명   | 배열에 쌓인 시세 변동 이벤트를 순차적으로 모두 발생되도록 요청       | 배열에 쌓인 시세 변동의 이벤트중에서 가장 최근의 이벤트만 발생되도록 요청 |
| 사용 예 | <히스토리성 데이타><br/> HTS의 TR7024 호가 체결 리스트 화면처럼 시세변동 데이타를 빠짐없어 모두 처리해야 하는 경우에 사용합니다. | <스냅샷성 데이타><br/> HTS의 TR7021 현재가 화면처럼 보는 시점에 가장 최근 데이타만 수신되도록 합니다.  따라서 Subscribe보다는 처리할 이벤트는 줄어 들어서 처리속도는 줄어 들어 유용하게 사용 |
