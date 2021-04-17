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

**설명**: CYBOS에서사용되는주식코드조회작업을함.

**모듈위치**: CpUtil.dll

**Method**

value = object.**CodeToName(code)**

code에해당하는종목명을반환합니다

- code: 종목코드
- 반환값: 종목명

value = object. **NameToCode(name)**

code에해당하는종목명을반환합니다

- code: 종목명
- 반환값: 종목코드

value = object.**CodeToFullCode(code)**

code에해당하는 FullCode를반환한다.

- Code: 종목코드,
- 반환값: Full Code

value = object.**FullCodeToName(fullcode)**

fullcode에해당하는종목명을반환한다

- fullcode: FullCode
- 반환값: 종목명

value = object.**FullCodeToCode(fullcode)**

fullcode에해당하는 Code를반환한다

- fullcode:Full Code
- 반환값: Code

value = object. **CodeToIndex(code)**

code에해당하는 Index를반환한다

- code:종목코드
- 반환값: Index

value = object.**GetCount()**

종목코드수를반환한다

- 반환값: 종목코드개수

value = object.**GetData(type,index)**

해당인덱스의종목데이터를구한다

- type: 데이터종류

0 - 종목코드

1 - 종목명

2 - FullCode

- index: : 종목코드인덱스
- 반환값: 해당데이터

value = object.**Get****PriceUnit****(****code, basePrice, directionUp****)**

주식/ETF/ELW의호가단위를구한다.

- code(string):종목코드

- basePrice(long):기준가격
- directionUp(bool[default:true]]):상승의단위인가의여부
- 반환값(long): 호가단위