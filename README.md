# exl
Excel binding to struct written in Go.(Only supports Go1.18+)

[![CircleCI](https://circleci.com/gh/go-the-way/exl/tree/main.svg?style=shield)](https://circleci.com/gh/go-the-way/exl/tree/main)
[![codecov](https://codecov.io/gh/go-the-way/exl/branch/main/graph/badge.svg?token=8MAR3J959H)](https://codecov.io/gh/go-the-way/exl)
[![Go Report Card](https://goreportcard.com/badge/github.com/go-the-way/exl)](https://goreportcard.com/report/github.com/go-the-way/exl)

## usage

### Read Excel

```go
package main

import (
	"fmt"
	"github.com/go-the-way/exl"
)

type ReadExcelModel struct {
	ID   int    `excel:"ID"`
	Name string `excel:"Name"`
}

func (*ReadExcelModel) ReadMetadata() *exl.ReadMetadata {
	return &exl.ReadMetadata{DataStartRowIndex: 1}
}

func main() {
	if models, err := exl.Read("/to/path.xlsx", new(ReadExcelModel)); err != nil {
		fmt.Println("read excel err:" + err.Error())
	} else {
		fmt.Printf("read excel num: %d\n", len(models))
	}
}
```

### Write Excel

```go
package main

import (
	"fmt"
	"github.com/go-the-way/exl"
)

type WriteExcelModel struct {
	ID   int    `excel:"ID"`
	Name string `excel:"Name"`
}

func (*WriteExcelModel) WriteMetadata() *exl.WriteMetadata {
	return &exl.WriteMetadata{}
}

func main() {
	if err := exl.Write("/to/path.xlsx", []*WriteExcelModel{{100, "apple"}, {200, "pear"}}); err != nil {
		fmt.Println("write excel err:" + err.Error())
	} else {
		fmt.Println("write excel done")
	}
}
```