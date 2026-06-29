# satysfi-test - Unit Testing Framework for SATySFi

This library provides an elm-test-inspired unit testing framework for [SATySFi](https://satysfi.org/).

## Features

- Elm-test inspired API for writing test expectations
- Support for custom equality functions with explicitComparators  
- Failure messages included in test reports
- Typed equality helpers: `equal-int`, `equal-string`, `equal-bool`

## Basic Usage

```satysfi
@require: test/expect
@import: ../src/test

open Test

describe `My tests` [
  it `adds numbers correctly` (fun () -> (
    expect 3 + 4 |> equal-int 7
  ));
  
  it `fails with message` (fun () -> (
    expect "actual" |> equal-string "expected"
  ))
] |> run
```

## API

See `src/expect.satyg` for complete documentation.

## Examples

### Integer Equality

```satysfi
it `adds numbers correctly` (fun () -> (
  expect 3 + 4 |> equal-int 7
))
```

### String Comparison with Custom Format

```satysfi  
let format-person p = `Person(name=`# ^ p.name ^ `, age=`# ^ arabic p.age ^ `)`
expect actual |> equal-by (==) format-show expected
```

### Multiple Assertions on Same Subject

```satysfi  
it `list properties` (fun () -> (
  expect [1;2;3]
    |> all [ fun l -> length l |> equal-int 3
             ; fun l -> List.hd l |> equal-int 1 ]
))
```
