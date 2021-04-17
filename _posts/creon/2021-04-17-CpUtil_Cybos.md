---
title: "CpUtil.CpCybos"
search: true
categories:
  - creon
toc: true
toc_label: "목차"
sidebar:
  title: "Creon-Plus"
  nav: sidebar-creon
---

**설명**: CYBOS의각종상태를확인할수있음.

**모듈위치**: CpUtil.dll

**Property**

value = object.**IsConnect**

(읽기전용) CYBOS의통신연결상태를반환합니다

- 반환값: 0- 연결끊김, 1- 연결정상

value = object.**ServerType**

(읽기전용) 연결된서버종류를반환합니다

- 반환값: 0- 연결끊김, 1- cybosplus 서버, 2- HTS 보통서버(cybosplus 서버제외)

value = object.**LimitRequestRem****a****inTime**

(읽기전용) 요청개수를재계산하기까지남은시간을반환합니다. 즉리턴한시간동안남은요청개수보다더요청하면요청제한이됩니다.

- 반환값: 요청개수를재계산하기까지남은시간(단위:milisecond)

**Method**

value = object.**GetLimitRemainCount(limitType)**

limitType에대한제한을하기까지남은요청개수를반환합니다.

- limitType: 요쳥에 대한 제한타입

LT_TRADE_REQUEST    = 0, 주문 / 계좌 관련 RQ 요청

LT_NONTRADE_REQUEST = 1, 시세관련 RQ 요청

LT_SUBSCRIBE        = 2, 시세관련 SB

- 반환값: 제한을하기전까지의남은요청개수

  

value = object.**PlusDisconnect()**

Plus 종료. 단 종료 API 호출 하더라도 사용하시는 응용프로그램을 종료하지않으면 PLUS 연결 서비스가 유지됩니다.

**Event**

Object.**OnDisConnect**

U-CYBOS의통신연결상태가끊긴경우에이벤트가발생합니다.

이이벤트를받은후에는더이상데이터통신이불가능합니다.

가능한프로그램을정리하고 안전하게종료하도록프로그램을작성해야합니다.