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
H2{color:Blue !important;}
</style>
## Method

|                                                              | **RQ/RP**                                                    | **SB/PB**                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data  Input**                                              | object.**SetInputValue** (type, value)<br/>  type에 해당하는 입력데이터를 Value 값으로 지정한다.<br/>  type : 입력데이터 종류<br/>  value : 새로 지정할 값 |                                                              |
| **통신****요청****(****하단****각각****비교****설명****참조****)** | object.**Request**()<br/>ret = object.**BlockRequest** ()<br/>ret = object.**BlockRequest2** (short  option)<br/>3가지중에선택1 | object.**Subscribe**()<br/>object.**SubscribeLatest**()<br/>2가지중에선택1 |
| **Data  Get**                                                | value = object.**GetHeaderValue** ( type )<br/>   type에해당하는헤더데이터를반환한다.<br/>  type : 데이터종류 <br/>반환값 : 데이터종류에해당하는값 <br/>value = object.**GetDataValue** ( type, index )<br/>  type : 데이터종류<br/> index : 데이터인덱스<br/> 반환값 : 데이터종류의 index 번째데이터 |                                                              |

 

| object.  **GetDibStatus** | DIB 통신상태 (읽기전용)<br/>  반환값 :<br/>  -1 - 오류<br/> 0 - 정상<br/> 1 - 수신대기.<br/>  오류(-1) , 정상(0) 상태에서는데이타요청가능.<br/> 수신대기(1) Request를 요청하고 아직 Received 이벤트를 받지 않은 상태의 오브젝트로 다시 Request/BlockRequest/BlockRequest2를 호출한 경우에 발생 |
| ------------------------- | ------------------------------------------------------------ |
| object.**GetDibMsg1**     | DIB 통신결과메시지문자열(읽기전용)<br/>  반환값 : 결과메시지문자열 |
| object.**GetDibMsg2**     | **사용안함**                                                 |

 

## Property

| object.**Continue** | 연속데이터유무를나타내는프로퍼티. (읽기전용)<br/>  반환값 : 1 - 연속데이터있음. 0 - 연속데이터없음. |
| ------------------- | ------------------------------------------------------------ |
| object.**Header**   | Header 컬렉션루트객체를반환한다.<br/>  Header 컬렉션에는 Header 정보의종류와이름이들어있다.(읽기전용)<br/>  반환값 : Header 컬렉션객체. |
| object.**Data**     | Data 컬렉션루트객체를반환한다.<br/>  Data 컬렉션에는 Data 정보의종류와이름이들어있다.(읽기전용)<br/>  반환값 : Data 컬렉션객체. |

 

## Event

object**.Received**
데이터를수신했을때발생하는이벤트

 

## BlockRequest/Blockrequest****2****/Request****의****리턴값

|                  | **BlockRequest/BlockRequest2**                               | **Request** |
| ---------------- | ------------------------------------------------------------ | ----------- |
| 시세오브젝트     | 리턴값<br/>0: 정상요청<br/>1: 통신요청실패<br/>3: 그외의내부오류            | 리턴값없음  |
| 주문관련오브젝트 | 리턴값<br/>0: 정상요청<br/>1: 통신요청실패<br/>2: <span style= "color:Blue !important;"> 주문확인창에서취소</span><br/>3: 그외의내부오류<br/>4: 주문요청제한개수초과 | 좌동        |

 

## 요청제한

사용자의고의또는실수(무한루프등...)로부터서버및다른사용자들을보호하기위하여시세요청(RQ)과실시간요청(SB)에대해제한을두고있습니다.

|                  | **RQ**  **제한**                                             | **SB**  **제한**                       |
| ---------------- | ------------------------------------------------------------ | -------------------------------------- |
| 시세오브젝트     | 15초에최대 60건으로제한<br/>초과요청시첫요청으로부터15초가지날때까지내부적으로기다림 | 최대 400건의요청으로제한<br/>초과요청시오류 |
| 주문관련오브젝트 | 15초에최대 20건으로제한<br/>초과요청 시 첫 요청으로 부터 15초가 지날 때까지요청함수(Request, BlockRequest, BlockRequest2)에서 4를반환 | 제한없음                               |

위의 제한사항은 당사방침에 따라 변경될 수 있습니다.

CpCybos의 LimitRequestRemainTime과 GetLimitRemainCount로 타임아웃까지 남은 시간과 남아 있는 요청 개수를 얻을 수있 습니다.

 

## BlockRequest와 BlockRequest2 비교

예를들어설명하겠습니다. 다음과같은예가있습니다.
(a) BlockRequest 하는도중에다른이벤트(Received,마우스클릭등) 처리안에서

다른 (b)BlockRequest가있다고가정할경우

|      | **BlockRequest**                                 | **BlockRequest2**                                            |
| ---- | ------------------------------------------------ | ------------------------------------------------------------ |
| 설명 | (b)의  BlockRequest가우선 처리                   | option 인자에따라기능이다름<br/> - option이 0 :  BlockRequest와같은기능<br/> - option이 1:  요청한 순서대로 (a)의 BlockRequest2가 먼저 수행됩니다. |
| 특징 | 이벤트에서 요청할 RQ를 우선적으로 처리할 경우 유리함 | 순차적으로 RQ를 요청할 경우 유리함 통상적인경우 BlockRequest2 사용을 추천함 |

 

## Subscribe와 SubscribeLatest 비교

시세변동의이벤트는내부에서는배열로처리하고있습니다.

|        | **Subscribe**                                                | **SubscribeLatest**                                          |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 설명   | 배열에 쌓인 시세 변동 이벤트를 순차적으로 모두 발생되도록 요청       | 배열에쌓인시세변동의이벤트중에서가장최근의이벤트만발생되도록요청 |
| 사용예 | <히스토리성데이타><br/> HTS의 TR7024 호가 체결 리스트 화면처럼 시세변동 데이타를 빠짐없어 모두 처리해야 하는 경우에 사용합니다. | <스냅샷성데이타><br/> HTS의 TR7021 현재가 화면처럼 보는 시점에 가장 최근 데이타만 수신되도록 합니다.  따라서 Subscribe보다는 처리할 이벤트는 줄어 들어서 처리속도는 줄어 들어 유용하게 사용 |
