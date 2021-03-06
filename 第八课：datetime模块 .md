# 16. datetime模块

Created: Aug 7, 2020 5:29 PM

# datetime模块

datetime 是 Python 中处理日期的标准模块，它提供了 4 种对日期和时间进行处理的类：**datetime**、**date**、**time** 和 **timedelta**。

## 2. date类

```python
class datetime(date):
    def __init__(self, year, month, day, hour, minute, second, microsecond, tzinfo)
        pass
    def now(cls, tz=None):
        pass
    def timestamp(self):
        pass
    def fromtimestamp(cls, t, tz=None):
        pass
    def date(self):
        pass
    def time(self):
        pass
    def year(self):
        pass
    def month(self):
        pass
    def day(self):
        pass
    def hour(self):
        pass
    def minute(self):
        pass
    def second(self):
        pass
    def isoweekday(self):
        pass
    def strftime(self, fmt):
        pass
    def combine(cls, date, time, tzinfo=True):
        pass
```

- `datetime.now(tz=None)` 获取当前的日期时间，输出顺序为：年、月、日、时、分、秒、微秒。
- `datetime.timestamp()` 获取以 1970年1月1日为起点记录的秒数。
- `datetime.fromtimestamp(tz=None)` 使用 unixtimestamp 创建一个 datetime。

```python
import datetime

dt = datetime.datetime(year=2020, month=6, day=25, hour=11, minute=23, second=59)
print(dt)  # 2020-06-25 11:23:59
print(dt.timestamp())  # 1593055439.0

dt = datetime.datetime.fromtimestamp(1593055439.0)
print(dt)  # 2020-06-25 11:23:59
print(type(dt)) # <class 'datetime.datetime'>

dt = datetime.datetime.now()
print(dt)  # 2020-06-25 11:11:03.877853
print(type(dt))  # <class 'datetime.datetime'>
```

【例子】如何创建一个 datetime 对象？

```python
import datetime

dt = datetime.datetime(year=2020, month=6, day=25, hour=11, minute=23, second=59)
print(dt)  # 2020-06-25 11:23:59
print(dt.timestamp())  # 1593055439.0

dt = datetime.datetime.fromtimestamp(1593055439.0)
print(dt)  # 2020-06-25 11:23:59
print(type(dt)) # <class 'datetime.datetime'>

dt = datetime.datetime.now()
print(dt)  # 2020-06-25 11:11:03.877853
print(type(dt))  # <class 'datetime.datetime'>
```

`datetime.strftime(fmt)` 格式化 `datetime` 对象。

[Untitled](https://www.notion.so/991adfa81f0249619e29484db831c485)

【例子】如何将 datetime 对象转换为任何格式的日期？

```python
import datetime
dt = datetime.datetime(year=2020, month=6, day=25, hour=11, minute=51, second=49)
s = dt.strftime("'%Y/%m/%d %H:%M:%S")
print(s) # '2020/06/25 11:51:49
s = dt.strftime('%d %B, %Y, %A')
print(s) # 25 June, 2020, Thursday
```

【练习】如何将给定日期转换为 "mmm-dd, YYYY" 的格式？

```python
# 输入
d1 = datetime.date('2010-09-28')
# 输出
'Sep-28,2010'
```

【参考答案】

```python
import datetime
d1 = datetime.date(2010, 9, 28)
print(d1.strftime('%b-%d,%Y'))
# Sep-28,2010
```

- `datetime.date()` Return the date part.
- `datetime.time()` Return the time part, with tzinfo None.
- `datetime.year` 年
- `datetime.month` 月
- `datetime.day` 日
- `datetime.hour` 小时
- `datetime.minute` 分钟
- `datetime.second` 秒
- `datetime.isoweekday` 星期几
- `date.today()` 获取当前日期信息。

【例子】datetime 对象包含很多与日期时间相关的实用功能。

```python
import datetime
dt = datetime.datetime(year=2020, month=6, day=25, hour=11, minute=51, second=49)
print(dt.date()) # 2020-06-25
print(type(dt.date())) # <class 'datetime.date'>
print(dt.time()) # 11:51:49
print(type(dt.time())) # <class 'datetime.time'>
print(dt.year) # 2020
print(dt.month) # 6
print(dt.day) # 25
print(dt.hour) # 11
print(dt.minute) # 51
print(dt.second) # 49
print(dt.isoweekday()) # 4
```

### parser 模块

在处理含有字符串日期的数据集或表格时，我们需要一种自动解析字符串的方法，无论它是什么格式的，都可以将其转化为 datetime 对象。这时，就要使用到 dateutil 中的 parser 模块。

- `parser.parse(timestr, parserinfo=None, **kwargs)`

【例子】如何在 python 中将字符串解析为 datetime对象？

```python
from dateutil import parser

s = '2020-06-25'
dt = parser.parse(s)
print(dt)  # 2020-06-25 00:00:00
print(type(dt))  # <class 'datetime.datetime'>

s = 'March 31, 2010, 10:51pm'
dt = parser.parse(s)
print(dt)  # 2010-03-31 22:51:00
print(type(dt))  # <class 'datetime.datetime'>
```

【练习】如何将字符串日期解析为 datetime 对象？

```python
# 输入
s1 = "2010 Jan 1"
s2 = '31-1-2000'
s3 = 'October10, 1996, 10:40pm'
# 输出
2010-01-01 00:00:00
2000-01-31 00:00:00
2019-10-10 22:40:00
```

【参考答案】

```python
from dateutil import parser
s1 = "2010 Jan 1"
s2 = '31-1-2000'
s3 = 'October10, 1996, 10:40pm'
dt1 = parser.parse(s1)
dt2 = parser.parse(s2)
dt3 = parser.parse(s3)
print(dt1) # 2010-01-01 00:00:00
print(dt2) # 2000-01-31 00:00:00
print(dt3) # 1996-10-10 22:40:00
```

【练习】计算以下列表中连续的天数。

```python
# 输入
['Oct, 2, 1869', 'Oct, 10, 1869', 'Oct, 15, 1869', 'Oct, 20, 1869','Oct, 23, 1869']
# 输出
[8, 5, 5, 3]
```

【参考答案】

```python
import numpy as np
from dateutil import parser

dateString = ['Oct, 2, 1869', 'Oct, 10, 1869', 'Oct, 15, 1869', 'Oct, 20, 1869', 'Oct, 23, 1869']
dates = [parser.parse(i) for i in dateString]
td = np.diff(dates)
print(td)
# [datetime.timedelta(days=8) datetime.timedelta(days=5)
#  datetime.timedelta(days=5) datetime.timedelta(days=3)]
d = [i.days for i in td]
print(d)  # [8, 5, 5, 3]
```

## **2. date类**

```python
class date:
    def __init__(self, year, month, day):
        pass
    def today(cls):
        pass
```

- `date.today()` 获取当前日期信息。

【例子】如何在 Python 中获取当前日期和时间？

```python
import datetime

d = datetime.date(2020, 6, 25)
print(d)  # 2020-06-25
print(type(d))  # <class 'datetime.date'>

d = datetime.date.today()
print(d)  # 2020-06-25
print(type(d))  # <class 'datetime.date'>
```

【练习】如何统计两个日期之间有多少个星期六？

```python
# 输入
d1 = datetime.date(1869, 1, 2)
d2 = datetime.date(1869, 10, 2)

# 输出
40
```

【参考答案】

```python
import datetime

d1 = datetime.date(1869, 1, 2)
d2 = datetime.date(1869, 10, 2)
dt = (d2 - d1).days
print(dt)
print(d1.isoweekday())  # 6
print(dt // 7 + 1)  # 40
```

## **3. time类**

```python
class time:
    def __init__(self, hour, minute, second, microsecond, tzinfo):
        pass
```

【例子】如何使用 datetime.time() 类？

```python
import datetime

t = datetime.time(12, 9, 23, 12980)
print(t)  # 12:09:23.012980
print(type(t))  # <class 'datetime.time'>
```

注意：

- 1秒 = 1000 毫秒（milliseconds）
- 1毫秒 = 1000 微妙（microseconds）

【练习】如何将给定日期转换为当天开始的时间？

```python
# 输入
import datetime
date = datetime.date(2019, 10, 2)
# 输出
2019-10-02 00:00:00
```

【参考答案】

```python
import datetime
date = datetime.date(2019, 10, 2)
dt = datetime.datetime(date.year, date.month, date.day)
print(dt) # 2019-10-02 00:00:00
dt = datetime.datetime.combine(date, datetime.time.min)
print(dt) # 2019-10-02 00:00:00
```

## 4. timedelta类

`timedelta` 表示具体时间实例中的一段时间。你可以把它们简单想象成**两个日期或时间之间的间隔**。

它常常被用来从 `datetime` 对象中添加或移除一段特定的时间。

```python
class timedelta(SupportsAbs[timedelta]):
    def __init__(self, days, seconds, microseconds, milliseconds, minutes, hours, weeks,):
        pass
    def days(self):
        pass
    def total_seconds(self):
        pass
```

【例子】如何使用 datetime.timedelta() 类？

```python
import datetime

td = datetime.timedelta(days=30)
print(td)  # 30 days, 0:00:00
print(type(td))  # <class 'datetime.timedelta'>
print(datetime.date.today())  # 2020-07-01
print(datetime.date.today() + td)  # 2020-07-31

dt1 = datetime.datetime(2020, 1, 31, 10, 10, 0)
dt2 = datetime.datetime(2019, 1, 31, 10, 10, 0)
td = dt1 - dt2
print(td)  # 365 days, 0:00:00
print(type(td))  # <class 'datetime.timedelta'>

td1 = datetime.timedelta(days=30)  # 30 days
td2 = datetime.timedelta(weeks=1)  # 1 week
td = td1 - td2
print(td)  # 23 days, 0:00:00
print(type(td))  # <class 'datetime.timedelta'>
```

如果将两个 datetime 对象相减，就会得到表示该时间间隔的 timedelta 对象。

同样地，将两个时间间隔相减，可以得到另一个 timedelta 对象。

【练习】 

1. 距离你出生那天过去多少天了？ 

```python
import datetime

birthday=datetime.date(1997,3,27)
date=datetime.date.today()

td=(date-birthday).days
print(td) #8534
```

2. 距离你今年的下一个生日还有多少天？ 

```python
import datetime

birthday=datetime.date(2021,3,27)
date=datetime.date.today()

td=(birthday-date).days
print(td)#232
```

3. 将距离你今年的下一个生日的天数转换为秒数。

```python
print((birthday-date).total_seconds())#20044800.0
```

【参考答案】

```python
from dateutil import parser
import datetime

bDay = 'Oct 2, 1969'
dt1 = parser.parse(bDay).date()
dt2 = datetime.date.today()
dt3 = datetime.date(dt2.year, dt1.month, dt1.day)
print(dt1)  # 1969-10-02
print(dt2)  # 2020-07-01
print(dt3)  # 2020-10-02

td = dt2 - dt1
print(td.days)  # 18535
td = dt3 - dt2
print(td.days)  # 93
print(td.days * 24 * 60 * 60)  # 8035200
print(td.total_seconds())  # 8035200.0
```

## **练习题**：

1、假设你获取了用户输入的日期和时间如`2020-1-21 9:01:30`，以及一个时区信息如`UTC+5:00`，均是`str`，请编写一个函数将其转换为timestamp：

题目说明:

```python
"""
Input file
example1: dt_str='2020-6-1 08:10:30', tz_str='UTC+7:00'
example2: dt_str='2020-5-31 16:10:30', tz_str='UTC-09:00'
Output file
result1: 1590973830.0
result2: 1590973830.0
"""
import datetime
import re
from datetime import  timezone,timedelta
def to_timestamp(dt_str, tz_str):
    dt1=datetime.datetime.strptime(dt_str, '%Y-%m-%d %H:%M:%S')
    hours = int(tz_str[3:tz_str.index(':')])
    tz = timezone(timedelta(hours=hours))

    dt = dt1.replace(tzinfo=tz)
    return dt.timestamp()

dt_str = input("请输入日期和时间（格式：1990-1-1 00:00:00）：")
tz_str = input("请输入时区信息（格式：UTC+7:00）：")
print(to_timestamp(dt_str,tz_str))

#请输入日期和时间（格式：1990-1-1 00:00:00）：2020-6-1 08:10:30
#请输入时区信息（格式：UTC+7:00）：UTC+7:00
#1590973830.0

```

2、编写Python程序以选择指定年份的所有星期日。

题目说明:

```python
"""
   
Input file
   2020
   
Output file
   2020-01-05                         
   2020-01-12              
   2020-01-19                
   2020-01-26               
   2020-02-02     
   -----
   2020-12-06               
   2020-12-13                
   2020-12-20                
   2020-12-27 
"""

import datetime
from datetime import timedelta
from dateutil import parser

def all_sundays(year):
    day = '-01-01'
    dt=year+day
    dt1 = parser.parse(dt).date()
    cha=7-dt1.isoweekday()
    offset=datetime.timedelta(days=cha)
    dt2 = dt1+offset
    i=0
    for i in range(365//7):
        dt3=(dt2+ datetime.timedelta(days = 7*i)).strftime("%Y-%m-%d")
        i=i+1
        print(dt3)
        
year=input('请输入年份：')
all_sundays(year)
```