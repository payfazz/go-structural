# go-structural

[![Go Reference](https://pkg.go.dev/badge/github.com/payfazz/go-structural.svg)](https://pkg.go.dev/github.com/payfazz/go-structural)

Utility for structural typing in go.

Normaly Go use both nominal typing and structural for it type system, but structural typing only work with `interface`, with `struct` you can only achieve nominal typing.

Nominal typing is where you care about the name of the type. for example, function `takeA` will fail to compile because it need a type *named* `A`
```go
type A struct {
  X int
  Y string
}

type B struct {
  X int
  Y string
}

func takeA(a A) {}

func main() {
  var b B
  takeA(b) // compile-error
}
```

Structural typing is where you care about structure/behavior of the type. for example, function `takeA` will still compile because it need anything that *structured/behaved* like `A`
```go
type A interface {
  X() int
  Y() string
}

type B interface {
  X() int
  Y() string
}

func takeA(a A) {}

func main() {
  var b B
  takeA(b)
}
```

## Assign

`Assign` behave like [Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) in javascript.

It will assign every field that is exported and have same name/type.

It is useful for `DTO`.
