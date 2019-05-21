# Goland live templates
Useful live templates for goland IDE

## Golang
### if err not nil return  
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


### errors.wrap  
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
