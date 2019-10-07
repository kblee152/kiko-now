---
layout: post
title: "Carsharing 데이터 분석 2: Trip의 수, 추세 등"
tags: [tableau, carsharing]
comments: true
---

Table: dump table

| 필드 이름 | 유형 |
|:---|:---|
| id  | INTEGER  |
| created  | TIMESTAMP  |
| updated  | TIMESTAMP  |
| deleted  | TIMESTAMP  |
| status  | INTEGER  |
| pickup_time  | TIMESTAMP  |
| return_time  | TIMESTAMP  |
| options  | INTEGER  |
| purpose  | STRING  |
| car_id  | INTEGER  |
| exemption_id  | STRING  |
| paycard_id  | STRING  |
| pickup_spot_id  | INTEGER  |
| return_spot_id  | INTEGER  |
| user_id  | INTEGER  |
|----

1. 일자별 Trip의 수
2. 스팟별 Trip의 수
3. 시작 Station, 도착 Station 별 개수
4. Trip을 시작하는 특정 날짜 및 시간에 대한 Count
5. 2019년 1월 1일부터 시간대별 추세
6. 요일별 사용자 수 Count

#### 1. 일자별 Trip의 수
```sql
SELECT DATE(pickup_time), COUNT(id) as count
FROM carsharing_data.dump
GROUP BY date
ORDER BY date;
```

#### 2. 스팟별 Trip의 수
```sql
SELECT pickup_spot_id, COUNT(id) as count
FROM carsharing_data.dump
GROUP BY prickup_spot_id
ORDER BY count DESC;
```

### Tableau Visualization

#### Proportion of customers
![정회원/준회원 비율](../images/2019-03-17-carsharing-data-analysis-회원변동.png)

#### Peaks
![PickupTime1](../images/2019-04-16-pickup-time-1.png)
![PickupTime2](../images/2019-04-16-pickup-time-2.png)

#### Peaks Weekdays Or weekends
![PickupTime3](../images/2019-04-16-3-Weekday-or-Weekends.png)