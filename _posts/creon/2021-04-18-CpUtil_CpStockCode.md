---
title: "CpUtil.CpStockCode"
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

**설명**: CYBOS에서 사용되는 주식코드 조회 작업을 함.

**모듈위치**: CpUtil.dll

## Method

value = object.**CodeToName(code)**

code에 해당하는 종목명을 반환합니다.
- code: 종목코드
- 반환값: 종목명

value = object. **NameToCode(name)**

code에 해당하는 종목명을 반환합니다.
- code: 종목명
- 반환값: 종목코드

value = object.**CodeToFullCode(code)**

code에 해당하는 FullCode를 반환한다.
- Code: 종목코드,
- 반환값: Full Code

value = object.**FullCodeToName(fullcode)**

fullcode에해당하는종목명을반환한다.
- fullcode: FullCode
- 반환값: 종목명

value = object.**FullCodeToCode(fullcode)**

fullcode에 해당하는 Code를 반환한다.
- fullcode:Full Code
- 반환값: Code

value = object. **CodeToIndex(code)**

code에 해당하는 Index를 반환한다.
- code:종목코드
- 반환값: Index

value = object.**GetCount()**

종목코드수를 반환한다.
- 반환값: 종목코드 개수

value = object.**GetData(type,index)**

해당 인덱스의 종목데이터를 구한다.
- type: 데이터 종류
  - 0 : 종목코드
  - 1 : 종목명
  - 2 : FullCode
- index: : 종목코드 인덱스
- 반환값: 해당 데이터

value = object.**Get****PriceUnit****(****code, basePrice, directionUp****)**

주식/ETF/ELW의 호가 단위를 구한다.
- code(string):종목코드
- basePrice(long):기준가격
- directionUp(bool[default:true]]):상승의 단위인가의 여부
- 반환값(long): 호가 단위
