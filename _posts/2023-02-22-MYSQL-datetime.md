---
layout: single
title: "MYSQL DATETIME함수 정리"
categories: Database
tag: [MYSQL, SQL]
toc: true
author_profile: false
sidebar:
    nav: "docs"
---

*** MYSQL에서의 날짜와 시간은 'YYYY-MM-DD HH:MM:SS'형식으로 저장되며, 문자열이 해당 형식으로 저장되어 있을 경우 아래 데이터 함수를 사용할 수 있음 (데이터 타입 자동 변환)**



## 표기 방식 지정(DATE_FORMAT())

```mysql
-- DATE_FORMAT(컬럼명, 형식)
SELECT DATE_FORMAT(column_name_, "%Y-%m-%d") FROM table_name_
```

| 형식 | 내용                                         |
| ---- | -------------------------------------------- |
| %Y   | 연도 숫자 (4자리)                            |
| %y   | 연도 숫자 (2자리)                            |
| %M   | 월 이름 (January~December)                   |
| %m   | 월 숫자 (00~12)                              |
| %D   | 영문 접미사가 있는 날자 (1st, 2nd, 3rd, ...) |
| %d   | 날짜 숫자                                    |
| %j   | 일(001~366)                                  |
| %H   | 시간 (00~23)                                 |
| %h   | 시간 (01~12)                                 |
| %i   | 분 (00~59)                                   |
| %S   | 초 (00~59), (=%s)                            |
| %f   | 마이크로초                                   |

[MySQL DATE_FORMAT형식 확인](https://dev.mysql.com/doc/refman/5.7/en/date-and-time-functions.html#function_date-format)



## 기타 날짜 및 시간 함수

### 1. 지정 값 반환

| 함수                                | 설명                        |
| ----------------------------------- | --------------------------- |
| DATE(*expr*)                        | 년, 월, 일 반환             |
| YEAR(*date*)                        | 연도 반환                   |
| MONTH(*date*)                       | 월 반환                     |
| MONTHNAME(*date*)                   | 달의 이름 반환              |
| DAY(*date*)<br />DAYOFMONTH(*date*) | 해당 월의 일 반환           |
| DAYOFYEAR(*date*)                   | 연도의 날짜 반환 (1~366)    |
| DAYOFWEEK(*date*)                   | 요일 인덱스 반환            |
| DAYNAME(*date*)                     | 요일 이름 반환              |
| WEEKDAY(*date*)                     | 요일 인덱스 반환            |
| TIME(*expr*)                        | 시, 분, 초, 마이크로초 반환 |
| HOUR(*time*)                        | 시간 반환                   |
| MINUTE(*time*)                      | 분 반환                     |
| SECOND(*time*)                      | 초 반환(0~59)               |
| MICROSECOND(*time*)                 | 마이크로초 반환             |



### 2. 시간 계산

| 함수                                                         | 설명                        |
| ------------------------------------------------------------ | --------------------------- |
| ADDDATE(*data*, INTERVAL *expr unit*)<br />DATE_ADD(*data*, INTERVAL *expr unit*) | 날짜에서 시간 값(간격) 추가 |
| DATE_SUB(*data*, INTERVAL *expr unit*)                       | 날짜에서 시간 값(간격) 빼기 |
| DATEDIFF(*expr1, expr2*)                                     | 두 날짜 차이 계산           |
| ADDTIME(*expr1, expr2*)                                      | 날짜에서 시간 추가          |
| SUBTIME(*expr1, expr2*)                                      | 두 시간 차이 계산 (문자열)  |
| TIMEDIFF(*expr1, expr2*)                                     | 두 시간 차이 계산           |

```sql
SELECT ADDDATE('2022-02-21', INTERVAL 1 DAY); -- 2022-02-22
SELECT DATE_ADD('2022-02-21', INTERVAL 1 MONTH); -- 2022-03-21
SELECT DATE_SUB('2022-02-21', INTERVAL 1 YEAR); -- 2021-02-21
SELECT DATEDIFF('2022-02-21', '2022-02-10'); -- 11
SELECT ADDTIME('09:30:45', '00:15:30'); -- 09:46:15
SELECT SUBTIME('23:00:00', '01:00:00'); -- 22:00:00
SELECT TIMEDIFF('12:00:00', '08:30:00'); -- 03:30:00
```



### 3. 형식 변환

| 함수                             | 설명                                       |
| -------------------------------- | ------------------------------------------ |
| CUNVERT_TZ(*dt, from_tz, to_tz*) | 한 표준 시간대에서 다른 표준 시간대로 변환 |
| SEC_TO_TIME(*seconds*)           | 초를 'hh:mm:ss' 형식으로 변환              |
| STR_TO_DATE(*str, format*)       | 문자열을 날짜로 변환                       |

```sql
SELECT CONVERT_TZ('2004-01-01 12:00:00','GMT','MET');
-- '2004-01-01 13:00:00'
SELECT CONVERT_TZ('2023-02-21 10:00:00', 'UTC', 'Asia/Seoul');
-- '2023-02-21 19:00:00'
SELECT SEC_TO_TIME(86400); -- '24:00:00'
SELECT STR_TO_DATE('2023-02-21', '%Y-%m-%d'); -- '2023-02-21'
```



### 4. 기타

| 함수      | 설명      |
| --------- | --------- |
| CURDATE() | 현재 날짜 |
| CURTIME() | 현재 시간 |

