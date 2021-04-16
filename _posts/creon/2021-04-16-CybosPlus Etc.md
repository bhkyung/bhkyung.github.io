**-** **CYBOS Code****규칙**

| 분류     | 내용                 | CYBOS의비교화면                     |
| -------- | -------------------- | ----------------------------------- |
| 주식     | A + 6자리(A003540)   | tr7021,7024  등등의주식화면         |
| ETN      | Q + 6자리(Q500001)   | 7021, 7024 등의 주식 화면           |
| 업종     | U + 3자리  (U001)    | tr7036,7035,7041,7042  등의업종화면 |
| Elw      | J + 6자리  (J506633) | tr7714,8971  등의 elw화면           |
| 선물옵션 | CYBOS와동일함        |                                     |

 

**-** **C****ybosPlus DataType**

CybosPlus는COM( Component Object  Model)을기반으로만들어진모듈입니다.  

따라서자동화데이터(Automation Data)형인  VARIANT 데이터형을취합니다.

| 도움말설명  Type | VarinatType | 설명              |
| ---------------- | ----------- | ----------------- |
| string           | VT_BSTR     | BSTR스트링        |
| char             | VT_I1       | 1바이트문자       |
| byte             | VT_UI1      | 1바이트양의문자   |
| short            | VT_I2       | 2바이트정수       |
| int              | VT_INT      | 4바이트정수       |
| long             | VT_I4       | 4바이트정수       |
| longlong         | VT_I8       | 8바이트정수       |
| float            | VT_R4       | 4바이트실수       |
| double           | VT_R8       | 8바이트실수       |
| decimal          | VT_DECIAML  | Decimal(16바이트) |
| ushort           | VT_UI2      | 2바이트양의정수   |
| uint             | VT_UINT     | 4바이트양의정수   |
| ulong            | VT_UI4      | 4바이트양의정수   |
| ulonglong        | VT_UI8      | 8바이트양의정수   |

주의) C#에서는  int는 4바이트정수이지만 long은  8바이트의정수입니다.