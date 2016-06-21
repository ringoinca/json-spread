Json-Spread
===========

## Description

A simple javascript library that helps first flatten a json structured object and creates duplicate objects off of each nested array elements.

Great for converting multi leveled json data to single level json that can be used to create csv,tsv,excel or other row column structured data.

## Installation
```bash
npm install json-spread
```

## Usage

```javascript
var jsonSpread = require('json-spread');
var output = jsonSpread({
  "a": [
    {
      "index": 1
    },
    {
      "index": 2
    },
    {
      "index": 3
    }
  ]
})
/*
output = [
  {
    "a.index": 1
  },
  {
    "a.index": 2
  },
  {
    "a.index": 3
  }
]
*/
```

## Examples

nested array
```javascript
//input
{
  "a": [
    1,
    2,
    3
  ],
  "b": {
    "a": [
      1,
      2,
      3
    ]
  }
}
//output
[
  {
    "a":1
  },
  {
    "a":2
  },
  {
    "a":3
  },
  {
    "b.a":1
  },
  {
    "b.a":2
  },
  {
    "b.a":3
  }
]
```

nested arrays within nested objects
```javascript
//input
{
  "a": {
    "b": {
      "c": {
        "d": {
          "e" : {
            "array": [
              1,
              2,
              3
            ]
          }
        }
      }
    }
  }
}
//output
[
  {
    "a.b.c.d.e.array": 1
  },
  {
    "a.b.c.d.e.array": 2
  },
  {
    "a.b.c.d.e.array": 3
  }
]
```

real life example
```javascript
//input
[
  {
    "user_id" : 1,
    "email": "1@domain.com",
    "hobbies": [
      {
        "type": "sport",
        "name": "soccer",
        "dates": [
          "May 3rd",
          "May 4th",
          "May 5th"
        ]
      },
      {
        "type": "sport",
        "name": "basketball",
        "dates": [
          "June 3rd",
          "July 4th"
        ]
      }
    ]
  },
  {
    "user_id" : 2,
    "email": "2@domain.com"
  },
  {
    "user_id" : 3,
    "email": "3@domain.com",
    "hobbies": []
  }
]
//output
[{
	"user_id": 1,
	"email": "1@domain.com",
	"hobbies.type": "sport",
	"hobbies.name": "soccer",
	"hobbies.dates": "May 3rd"
}, {
	"user_id": 1,
	"email": "1@domain.com",
	"hobbies.type": "sport",
	"hobbies.name": "soccer",
	"hobbies.dates": "May 4th"
}, {
	"user_id": 1,
	"email": "1@domain.com",
	"hobbies.type": "sport",
	"hobbies.name": "soccer",
	"hobbies.dates": "May 5th"
}, {
	"user_id": 1,
	"email": "1@domain.com",
	"hobbies.type": "sport",
	"hobbies.name": "basketball",
	"hobbies.dates": "June 3rd"
}, {
	"user_id": 1,
	"email": "1@domain.com",
	"hobbies.type": "sport",
	"hobbies.name": "basketball",
	"hobbies.dates": "July 4th"
}, {
	"user_id": 2,
	"email": "2@domain.com"
}, {
	"user_id": 3,
	"email": "3@domain.com",
	"hobbies": null
}]
```

## Options

you can define the value for empty arrays in options.  
default is ``null``

```javascript
var jsonSpread = require('json-spread');
var data = { "a": [] };
var options = {
  emptyValue: null //default is null
}
var output = jsonSpread(data,options);
//output
{
  "a" : null
}
```

## Contributing

fork it, then do an ``npm install``. everything should be in there  
I use babel to compile es6 to vanilla javascript.   

write code in ``/src`` folder then
```bash
npm run build
```
this compiles to the build folder

I use mocha and chai to test. 
```bash
npm test
```
write tests in ``/test`` folder. tests depends on compiled assets from build folder

don't touch ``/dist`` folder


## Dependencies
this library current depends on [flat](https://www.npmjs.com/package/flat) and [lodash](https://www.npmjs.com/package/lodash)

## License
MIT License