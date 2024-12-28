# convert

[![Package Version](https://img.shields.io/hexpm/v/convert)](https://hex.pm/packages/convert)
[![Hex Docs](https://img.shields.io/badge/hex-docs-ffaff3)](https://hexdocs.pm/convert/)

**Encode and decode from and to Gleam types effortlessly !**

Define a converter once and encode and decode as much as you want.

## Installation

```sh
gleam add convert
```

## Usage

```gleam
import gleam/io
import gleam/json
import convert
import convert/json as cjson

pub type Person {
  Person(name: String, age: Int)
}

pub fn main() {
  let converter =
    convert.object({
      use name <- convert.field("name", fn(v: Person) { Ok(v.name) }, convert.string())
      use age <- convert.field("age", fn(v: Person) { Ok(v.age) }, convert.int())
      convert.success(Person(name:, age:))
    })

  Person("Anna", 21)
  |> cjson.json_encode(converter)
  |> json.to_string
  |> io.debug
  // '{"name": "Anna", "age": 21}'

  "{\"name\": \"Bob\", \"age\": 36}"
  |> json.decode(cjson.json_decode(converter))
  |> io.debug
  // Ok(Person("Bob", 36))
}
```

Further documentation can be found at <https://hexdocs.pm/convert>.

## Features

- Javascript and Erlang targets
- Converters for all basic types
- Define converters for List, Dict, Result & Option
- Build converters for custom objects and enums

## Potential developments

Feel free to open PRs and issues if you want more features !

## Development

```sh
gleam run   # Run the project
gleam test  # Run the tests
```
