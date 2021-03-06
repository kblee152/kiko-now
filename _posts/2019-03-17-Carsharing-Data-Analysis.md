---
layout: post
title: "Carsharing 데이터 분석: MAU, DAU"
tags: [data-analysis]
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

1. MAU(Monthly Active User)
2. DAU(Daily Active User)

#### 1. MAU(Monthly Active User)
```sql
SELECT COUNT(DISTINCT user_id)
FROM `carsharing_data.dump`
WHERE pickup_time >= '2019-02-01' and pickup_time <= '2019-02-28';
```

#### 2. DAU(Daily Active User)
```sql
SELECT COUNT(DISTINCT user_id)
FROM `carsharing_data.dump`
WHERE pickup_time = '2019-02-01';
```


#### Tableau Visualization

##### Proportion of customers
![정회원/준회원 비율](../images/2019-03-17-carsharing-data-analysis-회원변동.png)

##### Peaks
![PickupTime1](../images/2019-04-16-pickup-time-1.png)
![PickupTime2](../images/2019-04-16-pickup-time-2.png)

##### Peaks Weekdays Or weekends
![PickupTime3](../images/2019-04-16-3-Weekday-or-Weekends.png)