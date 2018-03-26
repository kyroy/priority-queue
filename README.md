# priority-queue

[![Build Status](https://jenkins.kyroy.com/job/github.com-kyroy/job/priority-queue/job/master/badge/icon)](https://jenkins.kyroy.com/job/github.com-kyroy/job/priority-queue/job/master/)
[![Jenkins tests](https://img.shields.io/jenkins/t/https/jenkins.kyroy.com/job/github.com-kyroy/job/priority-queue/job/master.svg)](https://jenkins.kyroy.com/job/github.com-kyroy/job/priority-queue/job/master/)
[![Jenkins coverage](https://img.shields.io/jenkins/c/https/jenkins.kyroy.com/job/github.com-kyroy/job/priority-queue/job/master.svg)](https://jenkins.kyroy.com/job/github.com-kyroy/job/priority-queue/job/master/)

A [priority queue](https://en.wikipedia.org/wiki/Priority_queue) implementation in golang where every element in the queue can be accessed by its index in constant time.
This is achieved by using Golang's [sort](https://golang.org/pkg/sort/) package. 


## Usage

```bash
go get github.com/kyroy/priority-queue
```

```go
import "github.com/kyroy/priority-queue"
````

```go
type Data struct {
	value int
}

func main() {
    queue := pq.NewPriorityQueue()
    
    // Insert
    queue.Insert(Data{value: 7}, 3.5)
    queue.Insert(Data{value: 7}, 5.)
    queue.Insert(Data{value: 123}, 2.5)
    
    fmt.Println("len", queue.Len()) // len 3
    
    // Get
    for i := 0; i < queue.Len(); i++ {
    	d, prio := queue.Get(i)
    	fmt.Println("get", i, d, prio)
    }
    // get 0 {123} 2.5
    // get 1 {7} 3.5
    // get 2 {7} 5
    
    // Pop...
    d := queue.PopLowest().(Data)
    fmt.Println("d", d) // d {123}
    d = queue.PopHighest().(Data)
    fmt.Println("d", d) // d {7}
    
    // Len
    fmt.Println("len", queue.Len()) // len 1
}
```


### WithMinPrioSize

*Note: Equivalend for `WithMaxPrioSize`*

```go
type Data struct {
	value int
}

func main() {
    queue := pq.NewPriorityQueue(pq.WithMinPrioSize(2))
    
    // Insert
    queue.Insert(Data{value: 7}, 3.5)
    queue.Insert(Data{value: 7}, 5.)
    queue.Insert(Data{value: 123}, 2.5)
    
    fmt.Println("len", queue.Len()) // len 2
    
    // Get
    for i := 0; i < queue.Len(); i++ {
    	d, prio := queue.Get(i)
    	fmt.Println("get", i, d, prio)
    }
    // get 0 {123} 2.5
    // get 1 {7} 3.5
    
    // Pop...
    d := queue.PopLowest().(Data)
    fmt.Println("d", d) // d {123}
    d = queue.PopHighest().(Data)
    fmt.Println("d", d) // d {7}
    
    // Len
    fmt.Println("len", queue.Len()) // len 0
}
```
