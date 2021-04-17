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
<style>
H2{color:ForestGreen !important;}
</style>
**설명**: CYBOS의 각종 상태를 확인할 수 있음.

**모듈위치**: CpUtil.dll

## Property

value = object.**IsConnect**

(읽기전용) CYBOS의 통신 연결상태를 반환합니다

* 반환값: 0- 연결끊김, 1- 연결정상

value = object.**ServerType**

(읽기전용) 연결된 서버 종류를 반환합니다

* 반환값: 0- 연결끊김, 1- cybosplus 서버, 2- HTS 보통서버(cybosplus 서버제외)

value = object.**LimitRequestRem****a****inTime**

(읽기전용) 요청개수를 재계산하기까지 남은시간을 반환합니다. 즉 리턴한 시간동안 남은 요청개수보다 더 요청하면 요청제한이 됩니다.

* 반환값: 요청개수를 재계산하기까지 남은시간(단위:milisecond)

## Method

value = object.**GetLimitRemainCount(limitType)**

limitType에 대한 제한을 하기까지 남은 요청개수를 반환합니다.

* limitType: 요청에 대한 제한타입

  * LT_TRADE_REQUEST    = 0, 주문 / 계좌 관련 RQ 요청

  * LT_NONTRADE_REQUEST = 1, 시세관련 RQ 요청

  * LT_SUBSCRIBE        = 2, 시세관련 SB

* 반환값: 제한을 하기 전까지의 남은 요청개수

  

value = object.<span style= "color:Red !important;">**PlusDisconnect()**</span>

Plus 종료. 단 종료 API 호출 하더라도 사용하시는 응용프로그램을 종료하지 않으면 PLUS 연결 서비스가 유지됩니다.

## Event

Object.**OnDisConnect**

U-CYBOS의 통신연결 상태가 끊긴 경우에 이벤트가 발생합니다.

이 이벤트를 받은후에는 더 이상 데이터통신이 불가능합니다.

가능한 프로그램을 정리하고 안전하게 종료하도록 프로그램을 작성해야 합니다.
