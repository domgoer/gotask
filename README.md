# gotask

[![Build Status](https://travis-ci.org/domgoer/gotask.svg?branch=master)](https://travis-ci.org/domgoer/gotask)
[![codecov](https://codecov.io/gh/domgoer/gotask/branch/master/graph/badge.svg)](https://codecov.io/gh/domgoer/gotask)

### 轮询任务

``` go
package main

import (
    "time"
    
    "github.com/domgoer/gotask"
)

func main()  {
     tk,_ := gotask.NewTask(time.Second*20,func() {
            // do ... 
     })
     gotask.AddToTaskList(tk)
}
```

#### 注意

当task的轮询速度快于执行速度时，需要设置合理的结束时间，来防止goroutine的泄露。

### 动态修改轮询任务的执行时间

``` go
package main

import (
    "time"
    
    "github.com/domgoer/gotask"
)

func main()  {
     tk,_ := gotask.NewTask(time.Second*20,func() {
            // do ... 
     })
     gotask.AddToTaskList(tk)
     
     // 修改执行时间，立即生效
     tk.SetInterval(time.Second*30)
}
```

### 定时任务

``` go
package main

import (
    "github.com/domgoer/gotask"
)

func main()  {
     tkDay,_ := gotask.NewDailyTask("12:20:00",func() {
            // do ... 
     })
     tkMonth,_ := gotask.NewMonthlyTask("20 12:20:00",func() {
             // do ... 
      })
     tkYear,_ := gotask.NewYearlyTask("03-01 12:20:00",func(){})
     gotask.AddToTaskList(tkDay)
     gotask.AddToTaskList(tkMonth)
     gotask.AddToTaskList(tkYear)
}
```

> 多任务

``` go
package main

import (
    "github.com/domgoer/gotask"
)

func main()  {
     tkDays,_ := gotask.NewDailyTasks([]string{"12:20:00","10:10:10"},func() {
            // do ... 
     })
     tkMonths,_ := gotask.NewMonthlyTasks([]string{"20 12:20:00","21 10:10:10"},func() {
             // do ... 
      })
     gotask.AddToTaskList(tkDays...)
     gotask.AddToTaskList(tkMonths...)
}
```

### 暂停

``` go
package main

import (
    "github.com/domgoer/gotask"
)

func main()  {
     gotask.Pause("task.ID()")
}
```

### 恢复

``` go
package main

import (
    "github.com/domgoer/gotask"
)

func main()  {
     gotask.Resume("task.ID()")
}
```

### 移除

``` go
package main

import (
    "github.com/domgoer/gotask"
)

func main()  {
     gotask.Remove("task.ID()")
}
```

