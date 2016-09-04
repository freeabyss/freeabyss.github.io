---
title: QuartZ Cron表达式详解
date: 2016-05-29 00:29:57
tags: [Java, QuartZ, Cron, note]
categories: Java
---

## Cron表达式
> 格式：{seconds} {minutes} {hours} {day of month} {month} {day of week} [year]  
> year是可选的

| 字段名| 允许的值| 允许的字符| 
| :--: | :----:| :------| 
| 秒| 0-59 |  , - * / |
| 分| 0-59  | , - * / |
| 小时| 0-23 | , - * / |
| 日| 1-32 | , - * / ? L W C |
| 月| 1-12 or JAN-DEC |, - * / |
| 周| 1-7 or SUN-SAT | , - * / ? L #|
| 年| empty,1970-2099 | , - * / |

> day of month : 可以用数字1-31中的任一一个值，但要注意一些特别的月份。   
> day of week : 可以用1-7数字表示，1代表周日，或者用字符: SUN,MON,TUE,WED,THU,FRI,SAT。  
> month: 可以用1-12，或者字符: JAN, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC。 

## 字符解释
> \* :匹配该域的任意值，如\* 用在分所在的域，表示每分钟都会触发事件。     
> ?  :该字符仅用在`day of month`与`day of week`两个域中，并且两个域的?互斥，当其中一个被指定值后，另外一个为避免冲突需要将值设为?。  
> \- :匹配一个特定范围值，例如，10-12，表示10、11、12的时候触发事件。  
> ,  :匹配多个值，例如，10,12,13，表示10、12、13的时候触发事件。    
> /  :左边表示开始触发时间，右边是每隔固定时间触发一次事件，如`senconds`的值为'5/15' 表示 5 秒、20 秒、35 秒、50 秒的时候都触发一次事件。   
> L  :表示最后的意思。   
>   
> * 在`day of month`表示每月最后一天；
> * 在`day of week`表示周日；
> * 如果前面加上数字，表示本月最后一天，例如'6L'表示每月最后一个周五；
> * 还可以指定从最后一天到开始时间，例如，'L-2'表示每月的第2天到最后一天。
> 
> W  :表示工作日，例如，值为'15W'，表示在最近的工作日触发，如果15日是周六那么将在周五触发，如果是周日将在周一触发，如果是周一到周五则当天触发。 
>    ** *'L'可以与'W'结合使用，'LW'表示当月最后一个工作日* **    
> \#  :用来表示每个月的第几个星期几，例如，'6#3'表示某个月的第3个星期五。  

## 示例
| 表达式| 意思|
|:--- | :----|
| 0 0 12 * * ?  | Fire at 12pm (noon) every day |
| 0 15 10 ? * * | Fire at 10:15am every day |
| 0 15 10 * * ? | Fire at 10:15am every day |
| 0 15 10 * * ? *   | Fire at 10:15am every day |
| 0 15 10 * * ? 2005    | Fire at 10:15am every day during the year 2005 |
| 0 * 14 * * ?  | Fire every minute starting at 2pm and ending at 2:59pm, every day |
| 0 0/5 14 * * ?    | Fire every 5 minutes starting at 2pm and ending at 2:55pm, every day |
| 0 0/5 14,18 * * ? | Fire every 5 minutes starting at 2pm and ending at 2:55pm, AND fire every 5 minutes starting at 6pm and ending at 6:55pm, every day  |
| 0 0-5 14 * * ?    | Fire every minute starting at 2pm and ending at 2:05pm, every day |
| 0 10,44 14 ? 3 WED    | Fire at 2:10pm and at 2:44pm every Wednesday in the month of March. |
| 0 15 10 ? * MON-FRI   | Fire at 10:15am every Monday, Tuesday, Wednesday, Thursday and Friday  |
| 0 15 10 15 * ?    | Fire at 10:15am on the 15th day of every month |
| 0 15 10 L * ? | Fire at 10:15am on the last day of every month |
| 0 15 10 L-2 * ?   | Fire at 10:15am on the 2nd-to-last last day of every month |
| 0 15 10 ? * 6L    | Fire at 10:15am on the last Friday of every month  |
| 0 15 10 ? * 6L    | Fire at 10:15am on the last Friday of every month  |
| 0 15 10 ? * 6L 2002-2005  | Fire at 10:15am on every last friday of every month during the years 2002, 2003, 2004 and 2005 |
| 0 15 10 ? * 6#3   | Fire at 10:15am on the third Friday of every month |
| 0 0 12 1/5 * ?    | Fire at 12pm (noon) every 5 days every month, starting on the first day of the month. |
| 0 11 11 11 11 ?   | Fire every November 11th at 11:11am. |

## 参考资料
> [官方说明](http://quartz-scheduler.org/documentation/quartz-2.x/tutorials/crontrigger)
