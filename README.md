# Goland live templates
Useful live templates for goland IDE

## Golang
### if err not nil return  
Checks that err is not nil and writes return statement with default return values, except last - error. It would be wrapped with (errors.Wrap)[https://godoc.org/github.com/pkg/errors#Wrap]
errors.Wrap can be easily replaced with fmt.Errorf or any other function
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

| Name     | Expression                                                     | Default value | Skip if defined |
|----------|----------------------------------------------------------------|---------------|-----------------|
| $ERR$    | `errorVariable()`                                              | "err"         |                 |
| $RETURN$ | `regularExpression(defaultReturnValues, "(^[^,]*\|,.*)$", "")` |               |                 |
| $TEXT$   | `errorVariable()`                                              |               |                 |


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
