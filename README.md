events
======

Crazy Fast Event Dispatcher for golang.

1. NO REFLECTION
2. Async
3. Error Handler
4. Additional Event Store

> Events are somethings that happened in the past, 
> are executed async, 
> and you should call it with past name and do not rely on what the listener returns... 

Usage example:

```
helloListener := func(a interface{}) error {
    fmt.Print("Hello ", in)
    return nil
}
errorListener := func(e ListenerError){
    wasError = true
}
 
e := events.New()
e.On("hailed", helloListener)
e.OnError(errorListener) // If one listeners return error != nil

e.Raise("hailed", "World")

e.Wait() // optional
```

see `readme_test.go`


## Event repository with assertion on events (optional)

Is so useful in our tests to add an event store in order to make assertion on what
happened in your system

```
e := events.New()
e.AddInMemoryEventRepo() // or if you have one inject it see: AddEventRepo

e.On("hailed", helloListener)
e.Contains("hailed")     // true
``` 

## Test it

install deps `go get ./...`

and `go test ./... -v`

## Backend architecture and integration

For help designing a Go backend, integrating services, or building an MVP, see [Architecture with Soul — development and integration](https://soularchitecture.space/en/development?utm_source=github&utm_medium=referral&utm_campaign=backend_architecture&utm_content=events_readme).

Для задач по Go/backend, архитектуре и интеграциям: [Архитектура с душой — разработка и интеграция](https://soularchitecture.space/ru/development?utm_source=github&utm_medium=referral&utm_campaign=backend_architecture&utm_content=events_readme_ru).
