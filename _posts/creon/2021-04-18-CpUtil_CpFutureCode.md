---
title: "CpUtil.CpFutureCode"
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
**설명**: CYBOS에서 사용되는 선물코드 조회작업을 함.

**모듈위치**: CpUtil.dll

## Method

Value = object.**CodeToName(code)**

Code에 해당하는 선물 종목명을 반환한다
- code: 선물코드
- 반환값: 선물종목명

value = object.**GetCount()**

선물코드수를 반환한다
- 반환값: 선물코드 개수

value = object.**GetData(type,index)**

해당인덱스의 선물종목코드 데이터를 구한다

- **type:** **데이터****종류**
	- 0 : 종목코드
	- 1: 종목명
- index : 코드 인덱스
- 반환값: 해당 데이터