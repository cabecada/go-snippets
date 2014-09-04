### zookeeper

## Dependencies

```bash
$ go get launchpad.net/gozk
```
[Godoc Link](http://go.pkgdoc.org/launchpad.net/gozk/zookeeper)

## Getting Started

```go
package main

import "launchpad.net/gozk"

func main() {
    zk, session, err := gozk.Init("localhost:2181", 5000)
    if err != nil {
        println("Couldn't connect: " + err.String())
        return
    }
    defer zk.Close()

    // Wait for connection.
    event := <-session
    if event.State != gozk.STATE_CONNECTED {
        println("Couldn't connect")
        return
    }

    _, err = zk.Create("/counter", "0", 0, gozk.WorldACL(gozk.PERM_ALL))
    if err != nil {
        println(err.String())
    } else {
        println("Created!")
    }
}
```