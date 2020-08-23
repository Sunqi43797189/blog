---
title: golang时间计算
date: 2020-04-17 15:10:53
tags:
  - Golang
Categories:
  - Golang

---

### 获取当前时间是本周第几天，本年第几天

### 时间戳转时间对象

### 时分秒前后

### 年月日前后

### 获取特定日期

<!--more-->

- 获取当前时间是本周第几天，本年第几天
  
  ```go
  time.Now().Weekday()
  time.Now().YearDay()
  ```

- 时间戳转时间对象
  
  ```go
  time.Unix(1591234567, 0) // 秒，纳秒
  ```

- 时分秒前后,  2m两分钟后 -2m两分钟前 2h两小时后 -2h两小时前 2s两秒后 -2s两秒前
  
  ```go
  m, _ := time.ParseDuration("2m")
  time.Now().Add(m)
  ```

- 年月日前后
  
  ```go
  time.Now().AddDate(0, 0, -7) // 年月日 正数后，负数前
  ```

- 获取本周周一
  
  Time.Weekday 类型可以做运算，强制转int类型，得到偏差数
  
  默认是 Sunday 开始到 Saturday 算 0,1,2,3,4,5,6
  
  ```go
  func GetMondayOfWeek() (weekMonday string) {
      now := time.Now()
      offset := int(time.Monday - now.Weekday())
      if offset > 0 {
          offset = -6
      }
      weekStartDate := time.Date(now.Year(), now.Month(), now.Day(), 0, 0, 0, 0, time.Local).AddDate(0, 0, offset)
      weekMonday = weekStartDate.Format("2006-01-02")
      return
  }
  ```

- 获取上周周一
  
  ```go
  func GetLastWeekMondayDate() (weekMonday string) {
      thisWeekMonday := GetMondayOfWeek()
      TimeMonday, _ := time.Parse("2006-01-02", thisWeekMonday)
      lastWeekMonday := TimeMonday.AddDate(0, 0, -7)
      weekMonday = lastWeekMonday.Format("2006-01-02")
      return
  }
  ```

- 获取每个月第一天和最后一天
  
  ```go
  func getFirstDayOfMonth()  {
      now := time.Now()
      location := now.Location()
      year, month, _ := now.Date()
      firstOfMonth := time.Date(year, month, 1, 0, 0, 0, 0, location)
      lastOfMonth := firstOfMonth.AddDate(0, 1, -1)
      fmt.Println(firstOfMonth, lastOfMonth)
  }
  ```

- 获取分钟的开始
  
  ```go
  func getStartOfMinute()  {
      now := time.Now()
      fmt.Println(now)
      second := now.Second()
      duration, _ := time.ParseDuration(strconv.Itoa(second * -1) + "s")
      newTime := time.Date(now.Year(), now.Month(), now.Day(), now.Hour(), now.Minute(), 0, 0, time.Local)
      fmt.Println(newTime)
      fmt.Println(time.Now().Add(duration))
  }
  ```

- 计算两个日期之间相差天数
  
  ```go
  func getDayBetweenTwoDate()  {
      d1 := "2019-05-08"
      d2 := "2020-05-04"
      time1, _ := time.Parse("2006-01-02", d1)
      time2, _ := time.Parse("2006-01-02", d2)
      sub := time2.Sub(time1)
      day := sub.Hours() / 24
      fmt.Println(day)
  }
  ```
