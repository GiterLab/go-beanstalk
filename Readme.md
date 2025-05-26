# Beanstalk

Go client for beanstalkd with auth.

## Install

    go get github.com/Giterlab/go-beanstalk

## Use

Produce jobs:

    c, err := beanstalk.Dial("tcp", "127.0.0.1:11300")
    id, err := c.Put([]byte("hello"), 1, 0, 120*time.Second)

Consume jobs:

    c, err := beanstalk.Dial("tcp", "127.0.0.1:11300")
    id, body, err := c.Reserve(5 * time.Second)

With auth:

    c, err := beanstalk.Dial("tcp", "127.0.0.1:11300")
    // Authenticate with the server (if needed)
    err = c.Auth("your_password")
    if err != nil {
        fmt.Println("Error authenticating:", err)
        return
    }

    c, err := beanstalk.DialWithAuth("tcp", "127.0.0.1:11300", "your_password")
    if err != nil {
        fmt.Println("Error connecting with auth:", err)
        return
    }
