# Goland live templates
Useful live templates for goland IDE

## Golang
### if err not nil return  
Checks that err is not nil and writes return statement with default return values, except last - error. It would be wrapped with [errors.Wrap](https://godoc.org/github.com/pkg/errors#Wrap).
`errors.Wrap` can be easily replaced with fmt.Errorf or any other function
Abbreviation: 
```
errr
```
Template text:
```go
if $ERR$ != nil {
 return $RETURN$errors.Wrap($ERR$, "$TEXT$")$END$
}
```
Applicable: statement

| Name     | Expression                                               | Default value | Skip if defined |
|----------|----------------------------------------------------------|---------------|-----------------|
| $ERR$    | `errorVariable()`                                        | "err"         |                 |
| $RETURN$ | `regularExpression(defaultReturnValues, "([^,]*$)", "")` |               |                 |
| $TEXT$   | `errorVariable()`                                        |               |                 |


### errors.Wrap  
Abbreviation: 
```
wrap
```
Template text:
```go
$END$ errors.Wrap($ERR$, "$TEXT$")
```
Applicable: expression, statement

| Name     | Expression                                                     | Default value | Skip if defined |
|----------|----------------------------------------------------------------|---------------|-----------------|
| $ERR$    | `errorVariable()`                                              | "err"         |                 |
| $TEXT$   | `errorVariable()`                                              |               |                 |

### Variadic slice declaration
Creates shortcut for in-place slice declarations. Compiler should inline function call, so this function free to use.
Was created as a replacement for constructions like `[]string{}` -> `ss()`, `[]int{}` -> `is()`, etc. 

Abbreviation:
```
ss
```
Template text:
```go
func $NAME$$END$(slice ...$TYPE$) []$TYPE$ { return slice }
```
Applicable: file

| Name     | Expression                                                     | Default value | Skip if defined |
|----------|----------------------------------------------------------------|---------------|-----------------|
| $TYPE$   |                                                                | "string"      |                 |
| $NAME$   |                                                                | "ss"          |                 |

### Json field names in camelCase
Sometimes we need to declare json fields not in snake_case format (goland used it by default), but in camelCase.

Abbreviation:
```
jsonc
```
Template text:
```go
json:"$FIELD_NAME$"
```
Applicable: tag literal

| Name         | Expression                                                     | Default value | Skip if defined |
|--------------|----------------------------------------------------------------|---------------|-----------------|
| $FIELD_NAME$ | camelCase(fieldName())                                         |               |                 |

### Sort
Generate sort interface for your type. When go core team would add generics you may delete this.

Abbreviation:
```
sort
```
Template text:
```go
type $SLICE$ []$TYPE$
func ($REC$ $SLICE$) Len() int           { return len($REC$) }
func ($REC$ $SLICE$) Swap(i, j int)      { $REC$[i], $REC$[j] = $REC$[j], $REC$[i] }
func ($REC$ $SLICE$) Less(i, j int) bool {
    panic("implement me")$END$
}
```
Applicable: file

| Name     | Expression                                                     | Default value | Skip if defined |
|----------|----------------------------------------------------------------|---------------|-----------------|
| $TYPE$   | complete()                                                     | "Some"        |                 |
| $SLICE$  |                                                                | "SomeSlice"   |                 |
| $REC$    |                                                                | "ss"          |                 |
