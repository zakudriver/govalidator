## govalidator
> struct 验证器

#### 安装

```
go get github.com/Zhan9Yunhua/govalidator
```

#### 使用

```go
package main

import (
	github.com/Zhan9Yunhua/govalidator
	fmt
)

type Person struct {
    Name string     `validator:"required||string=[2|_"`     // 必填。2<=len
    Age  int        `validator:"number=10|20]"`             // 选填。10<Age<=20 / 0
    Sex  int        `validator:"number||in=0,1,2"`          // 选填。值只能是0||1||2     
    Car  []string   `validator:"multi=_|5]||in=LEXUS,BMW"`  // 选填。len>=5且包含LEXUS||BMW
}

func main{
	p := Person{Name: "z", Age: 11, Sex: 1, Car: []string{"AUDI"}}
	
	vali := govalidator.NewValidator()

	errs := vali.Validate(p)
	fmt.Println(errs) 
	// [[Name] should be greater than [2] [Car] is not in [LEXUS,BMW]]
}
```


