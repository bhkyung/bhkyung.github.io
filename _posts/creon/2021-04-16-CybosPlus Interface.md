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
## Method ##

|                                                              | **RQ/RP**                                                    | **SB/PB**                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data  Input**                                              | object.**SetInputValue**( type, value)  type에해당하는입력데이터를 Value 값으로지정한다.  type : 입력데이터종류 value : 새로지정할값 |                                                              |
| **통신****요청****(****하단****각각****비교****설명****참조****)** | object.**Request**()ret = object.**BlockRequest** ()ret = object.**BlockRequest2** (short  option)3가지중에선택1 | object.**Subscribe**()object.**SubscribeLatest**()2가지중에선택1 |
| **Data  Get**                                                | value = object.**GetHeaderValue** ( type )   type에해당하는헤더데이터를반환한다.  type : 데이터종류 반환값 : 데이터종류에해당하는값 value = object.**GetDataValue** ( type, index )  type : 데이터종류 index : 데이터인덱스 반환값 : 데이터종류의 index 번째데이터 |                                                              |

 

| object.  **GetDibStatus** | DIB 통신상태 (읽기전용)  반환값 :  -1 - 오류 0 - 정상 1 - 수신대기.  오류(-1) , 정상(0) 상태에서는데이타요청가능. 수신대기(1) Request를요청하고아직 Received 이벤트를받지않은상태의오브젝트로다시 Request/BlockRequest/BlockRequest2를호출한경우에발생 |
| ------------------------- | ------------------------------------------------------------ |
| object.**GetDibMsg1**     | DIB 통신결과메시지문자열(읽기전용)  반환값 : 결과메시지문자열 |
| object.**GetDibMsg2**     | **사용안함**                                                 |

 

![img](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAPCAYAAAA71pVKAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAACgSURBVDhPY/wPBAxkAiYoTRYYOM0Yfv7w4zrDvuu9DO/fXwPyOIH4O4OgoBaDk2YxgwCHJlgNDGDYfOz6VKDG+1AeCHCCDQKJowMMzc/fXweS34GYkyHZaS+cDRFHBVj8DFEMA8lOx6AskDgqwKIZphGieO4+ZygbYSAMYGiWFAQFCkQxskaIOCrA0GylmQ0OXWRnCgoqgsXRwchLngwMAG4tNxDXYvVAAAAAAElFTkSuQmCC)**Property**  

| object.**Continue** | 연속데이터유무를나타내는프로퍼티. (읽기전용)  반환값 : 1 - 연속데이터있음. 0 - 연속데이터없음. |
| ------------------- | ------------------------------------------------------------ |
| object.**Header**   | Header 컬렉션루트객체를반환한다.  Header 컬렉션에는 Header 정보의종류와이름이들어있다.(읽기전용)  반환값 : Header 컬렉션객체. |
| object.**Data**     | Data 컬렉션루트객체를반환한다.  Data 컬렉션에는 Data 정보의종류와이름이들어있다.(읽기전용)  반환값 : Data 컬렉션객체. |

 

![img](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAPCAYAAAA71pVKAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAACgSURBVDhPY/wPBAxkAiYoTRYYOM0Yfv7w4zrDvuu9DO/fXwPyOIH4O4OgoBaDk2YxgwCHJlgNDGDYfOz6VKDG+1AeCHCCDQKJowMMzc/fXweS34GYkyHZaS+cDRFHBVj8DFEMA8lOx6AskDgqwKIZphGieO4+ZygbYSAMYGiWFAQFCkQxskaIOCrA0GylmQ0OXWRnCgoqgsXRwchLngwMAG4tNxDXYvVAAAAAAElFTkSuQmCC)**Event**

object**.Received**
데이터를수신했을때발생하는이벤트

 

![img](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAPCAYAAAA71pVKAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAACgSURBVDhPY/wPBAxkAiYoTRYYOM0Yfv7w4zrDvuu9DO/fXwPyOIH4O4OgoBaDk2YxgwCHJlgNDGDYfOz6VKDG+1AeCHCCDQKJowMMzc/fXweS34GYkyHZaS+cDRFHBVj8DFEMA8lOx6AskDgqwKIZphGieO4+ZygbYSAMYGiWFAQFCkQxskaIOCrA0GylmQ0OXWRnCgoqgsXRwchLngwMAG4tNxDXYvVAAAAAAElFTkSuQmCC)**BlockRequest/Blockrequest****2****/Request****의****리턴값**

|                  | **BlockRequest/BlockRequest2**                               | **Request** |
| ---------------- | ------------------------------------------------------------ | ----------- |
| 시세오브젝트     | 리턴값0: 정상요청1: 통신요청실패3: 그외의내부오류            | 리턴값없음  |
| 주문관련오브젝트 | 리턴값0: 정상요청1: 통신요청실패2: 주문확인창에서취소3: 그외의내부오류4: 주문요청제한개수초과 | 좌동        |

 

![img](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAPCAYAAAA71pVKAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAACgSURBVDhPY/wPBAxkAiYoTRYYOM0Yfv7w4zrDvuu9DO/fXwPyOIH4O4OgoBaDk2YxgwCHJlgNDGDYfOz6VKDG+1AeCHCCDQKJowMMzc/fXweS34GYkyHZaS+cDRFHBVj8DFEMA8lOx6AskDgqwKIZphGieO4+ZygbYSAMYGiWFAQFCkQxskaIOCrA0GylmQ0OXWRnCgoqgsXRwchLngwMAG4tNxDXYvVAAAAAAElFTkSuQmCC)**요청제한**

사용자의고의또는실수(무한루프등...)로부터서버및다른사용자들을보호하기위하여시세요청(RQ)과실시간요청(SB)에대해제한을두고있습니다.

|                  | **RQ**  **제한**                                             | **SB**  **제한**                       |
| ---------------- | ------------------------------------------------------------ | -------------------------------------- |
| 시세오브젝트     | 15초에최대 60건으로제한초과요청시첫요청으로부터15초가지날때까지내부적으로기다림 | 최대 400건의요청으로제한초과요청시오류 |
| 주문관련오브젝트 | 15초에최대 20건으로제한초과요청시첫요청으로부터15초가지날때까지요청함수(Request, BlockRequest, BlockRequest2)에서4를반환 | 제한없음                               |

위의제한사항은당사방침에따라변경될수있습니다.

CpCybos의 LimitRequestRemainTime과 GetLimitRemainCount로타임아웃까지남은시간과남아있는요청개수를얻을수있습니다.

 

![img](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAPCAYAAAA71pVKAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAACgSURBVDhPY/wPBAxkAiYoTRYYOM0Yfv7w4zrDvuu9DO/fXwPyOIH4O4OgoBaDk2YxgwCHJlgNDGDYfOz6VKDG+1AeCHCCDQKJowMMzc/fXweS34GYkyHZaS+cDRFHBVj8DFEMA8lOx6AskDgqwKIZphGieO4+ZygbYSAMYGiWFAQFCkQxskaIOCrA0GylmQ0OXWRnCgoqgsXRwchLngwMAG4tNxDXYvVAAAAAAElFTkSuQmCC)  **BlockRequest****와****Bl****ockRequest2****비교**

예를들어설명하겠습니다. 다음과같은예가있습니다.
(a) BlockRequest 하는도중에다른이벤트(Received,마우스클릭등) 처리안에서

다른 (b)BlockRequest가있다고가정할경우

|      | **BlockRequest**                                 | **BlockRequest2**                                            |
| ---- | ------------------------------------------------ | ------------------------------------------------------------ |
| 설명 | (b)의  BlockRequest가우선 처리                   | option 인자에따라기능이다름 - option이 0 :  BlockRequest와같은기능 - option이 1:  요청한순서대로  (a)의 BlockRequest2가먼저수행됩니다. |
| 특징 | 이벤트에서요청할  RQ를우선적으로처리할경우유리함 | 순차적으로 RQ를요청할경우유리함 통상적인경우  BlockRequest2 사용을추천함 |

 

![img](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAPCAYAAAA71pVKAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAACgSURBVDhPY/wPBAxkAiYoTRYYOM0Yfv7w4zrDvuu9DO/fXwPyOIH4O4OgoBaDk2YxgwCHJlgNDGDYfOz6VKDG+1AeCHCCDQKJowMMzc/fXweS34GYkyHZaS+cDRFHBVj8DFEMA8lOx6AskDgqwKIZphGieO4+ZygbYSAMYGiWFAQFCkQxskaIOCrA0GylmQ0OXWRnCgoqgsXRwchLngwMAG4tNxDXYvVAAAAAAElFTkSuQmCC)  **Subscribe****와****SubscribeL****atest****비교**

시세변동의이벤트는내부에서는배열로처리하고있습니다.

|        | **Subscribe**                                                | **SubscribeLatest**                                          |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 설명   | 배열에쌓인시세변동이벤트를순차적으로모두발생되도록요청       | 배열에쌓인시세변동의이벤트중에서가장최근의이벤트만발생되도록요청 |
| 사용예 | <히스토리성데이타> HTS의TR7024 호가체결리스트화면처럼시세변동데이타를빠짐없어모두처리해야하는경우에사용합니다. | <스냅샷성데이타 > HTS의TR7021현재가화면처럼보는시점에가장최근데이타만수신되도록합니다.  따라서 Subscribe보다는처리할이벤트는줄어들어서처리속도는줄어들어유용하게사용 |
