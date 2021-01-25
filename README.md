# Golang code templates
Useful live templates and code completion for Goland IDE.

Install `settings.zip`: https://www.jetbrains.com/help/go/sharing-live-templates.html#import

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
Applicable in Go: statement

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
Applicable in Go: expression, statement

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
Applicable in Go: file

| Name     | Expression                                                     | Default value | Skip if defined |
|----------|----------------------------------------------------------------|---------------|-----------------|
| $TYPE$   |                                                                | "string"      |                 |
| $NAME$   |                                                                | "ss"          |                 |

### Json field names in camelCase
Sometimes we need to declare json fields not in snake_case format (goland used it by default), but in camelCase.
This pattern also can be applied to any other tags, like `sql`, `pg`, `csv`.

Abbreviation:
```
jsonc
```
Template text:
```go
json:"$FIELD_NAME$"
```
Applicable in Go: tag literal

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
Applicable in Go: file

| Name     | Expression                                                     | Default value | Skip if defined |
|----------|----------------------------------------------------------------|---------------|-----------------|
| $TYPE$   | complete()                                                     | "Some"        |                 |
| $SLICE$  |                                                                | "SomeSlice"   |                 |
| $REC$    |                                                                | "ss"          |                 |

### In
Checks that value is in slice of some type. In easy way.

Abbreviation:
```
in
```

Template text:
```go
func isIn$Type$Slice(v $type$, values ...$type$) bool {
	for i := range values {
		if values[i] == v {
			return true
		}
	}
	return false
}
```

Applicable in Go: file

| Name     | Expression                                                     | Default value | Skip if defined |
|----------|----------------------------------------------------------------|---------------|-----------------|
| $type$   |                                                                | "string"      |                 |
| $Type$   |                                                                | "String"      |                 |

### Safe getter 
Generates getter for struct field in protoc-gen-go style. 
Why do you need it? 
It allows access to nested fields without worrying about nil pointers.

```go
type Value struct {
    Field1 *Struct1
}
type Struct1 struct {
    Field2 *Struct2
}
type Struct2 struct {
    UsefulString *string
}

var value *Value
var _ = value.SafeField1().SafeField2().SafeUsefulString()

func (v *Value) SafeField1() *Struct1 {
	if v == nil {
		return nil
	}
	return v.Field1
}
func (s *Struct1) SafeField2() *Struct2 {
	if s == nil {
		return nil
	}
	return s.Field2
}
func (s *Struct2) SafeUsefulString() *string {
	if s == nil {
		return nil
	}
	return s.UsefulString
}
```

Abbreviation:
```
getter
```

Template text:
```go
func ($RECEIVER$ *$TYPE_1$) Safe$NAME$() $TYPE_2$ {
	if $RECEIVER$ == nil {
		return $RESULT$$END$
	}
	return $RECEIVER$.$NAME$
}
```
