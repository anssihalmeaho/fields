# fields
**fields** is [FunL](https://github.com/anssihalmeaho/funl) module for having easier access to certain kind of maps.
If map keys are strings and there are nested maps then it's sometimes easier to access field
by giving whole path separated with dots (like structures or records in some languages).

fields is implemented in FunL programming language: https://github.com/anssihalmeaho/funl

## Get started
Prerequisite is to have [FunL interpreter](https://github.com/anssihalmeaho/funl) compiled.
Clone fields from Github:

```
    git clone https://github.com/anssihalmeaho/fields.git
```

Put **fields.fnl** to some directory which can be found under **FUNLPATH** or in working directory.

See more information: https://github.com/anssihalmeaho/funl/wiki/Importing-modules

## Services

### getv
Returns value from map for given path of keys (dot -format string).

```
    call(fields.getv <map> <dot-format-string>) -> <value>
```

If any of keys is not found Runtime Error is generated.

### getlv
Similar to **getv** but returns list (pair) of:

1. true/false (bool), true if keypath was found, false if not found
2. value (if it was found, false if not found)

```
    call(fields.getlv <map> <dot-format-string>) -> list(<bool:is-found> <value>)
```

## Example
Here is example of usage:

```
ns main

import fields

main = proc()
	m = map(
		'person' map(
			'info' map(
				'age' 50
				'name' map(
					'firstname' 'Hank'
					'lastname'  'Hill'
				)
			)
		)
	)

	list(
		call(fields.getv m 'person.info.age')
		call(fields.getlv m 'person.info.age')
	)
end

endns
```

Output is:

```
list(50, list(true, 50))
```

