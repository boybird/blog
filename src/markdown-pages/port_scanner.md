---
title: "port scanner writing in golang"
date: "2019-10-26"
---


```go
package main

import (
	"flag"
	"fmt"
	"net"
	"sync"
	"time"
)

func main() {
	hostname := flag.String("hostname", "baidu.com", "hostname to test")
	startPort := flag.Int("start-port", 80, "the port which the scanning starts")
	endPort := flag.Int("end-port", 100, "the port which to scanning ends")
	timeout := flag.Duration("timeout", time.Millisecond*200, "timeout")
	flag.Parse()

	fmt.Printf("hostname: %s; start-port: %d; end-port: %d;\n", *hostname, *startPort, *endPort)

	ports := []int{}
	wg := &sync.WaitGroup{}

	for port := *startPort; port < *endPort; port++ {
		wg.Add(1)
		go func(p int) {
			opened := isOpen(*hostname, p, *timeout)
			if opened {
				ports = append(ports, p)
			}
			wg.Done()
		}(port)
	}
	wg.Wait()
	fmt.Printf("opened ports: %v\n", ports)
}

func isOpen(host string, port int, timeout time.Duration) bool {
	time.Sleep(time.Millisecond * 1)
	conn, err := net.DialTimeout("tcp", fmt.Sprintf("%s:%d", host, port), timeout)
	if err == nil {
		_ = conn.Close()
		return true
	}
	return false
}
```


```sh
go run main.go -hostname=www.nanniwan.com -end-port=9000  (
```
