# JSON

JSON stands for **J**ava**S**cript **O**bject **N**otation. It's a lightweight data interchange format that is easy for humans to read and write, and easy for machines to parse and generate. JSON is widely used for transmitting data between a server and a web application, as well as for configuration files and data storage.

## Structure - key-value pairs

JSON data is organized into key-value pairs, similar to objects in JavaScript or dictionaries in Python or [maps in Go](https://github.com/bjssacademy/go-maps). 

Key-value pairs are a fundamental concept in computer science and data structures. They represent associations between two pieces of data: a key and a value. 

The key is how you access the data - it's an identifier.

The value is the data it holds.

## Basic Structure 

The basic structure of JSON consists of two main types:

- Objects 
    - Enclosed in curly braces `{}`, containing key-value pairs separated by commas `,`. Keys must be strings, and values can be strings, numbers, objects, arrays, booleans, or null.
- Arrays 
    - Ordered lists of values enclosed in square brackets `[]`, separated by commas `,`. Values within arrays can also be strings, numbers, objects, arrays, booleans, or null.

## Basic Syntax

Here's an example of JSON that represents a person:

```json
{
  "name": "John Doe",
  "age": 30,
  "isStudent": false,
  "address": {
    "street": "123 Main St",
    "city": "Anytown",
    "zipcode": "12345"
  },
  "hobbies": ["reading", "painting", "hiking"]
}
```


We have five "top-level" keys - `name`, `age`, `isStudent`, `address` and `hobbies`, and each is enclosed in quotes - absolutely vital in JSON!

Each value has a different type:

| Key    | Value | Type |
| -------- | ------- | ------ |
| name  | John Doe    | string |
| age  | 30    | number |
| isStudent  | false    | boolean |
| address  | JSON object    | object |
| hobbies  | JSON array    | array |

`name`, `age` and `isStudent` are all simple data types. Our string is contained in quotes "John Doe", and our number and boolean are not.

`address` holds a *JSON object*. That's right, we're back in the land of trees, just like the file system, or how HTML is structured.

Inside the `address` object, we can see it is also a set of key-value pairs in JSON format, comprising `street`, `city` and `zipcode`, which all have string values.

`hobbies` is an array of strings.

## Array of objects

JSON allows for nested objects and arrays, enabling complex data structures to be represented in a hierarchical manner.

Let's say people had more than one address. We could perhaps create two keys - something like `home_address` and `work_address`:

```json
{
  "name": "John Doe",
  "age": 30,
  "isStudent": false,
  "work_address": {
    "street": "123 Main St",
    "city": "Anytown",
    "zipcode": "12345"
  },
  "home_address": {
    "street": "456 Nowhere St",
    "city": "Anytown",
    "zipcode": "12345"
  },
  "hobbies": ["reading", "painting", "hiking"]
}
```

However, it gets very messy very quickly if we add more addresses. We're better off making the address an array of objects, and calling it `addresses` and adding a new field `type`:

```json
{
  "name": "John Doe",
  "age": 30,
  "isStudent": false,
  "addresses": [
    {
        "type": "work",
        "street": "123 Main St",
        "city": "Anytown",
        "zipcode": "12345"
    },
    {
        "type": "home",
        "street": "456 Nowhere St",
        "city": "Anytown",
        "zipcode": "12345"
    }
  ],
  "hobbies": ["reading", "painting", "hiking"]
}
```
## What's JSON used for?

JSON is commonly used in web development, and some of its applications include:

- **APIs (Application Programming Interfaces)** 
    - Many web services use JSON to send and receive data between the server and client. 
- **Configuration files** 
    - JSON is often used to configure applications or settings due to its simplicity and readability.
- **Data storage** 
    - NoSQL databases like MongoDB store data in JSON-like formats.

### Example

When you fill in a form on a website, perhaps registering for an account, the email/username and password you choose will be sent to the web server using JSON that might look like:

```json
{
    "email":"tedt@hotmail.com",
    "password":"myverysecurepassword"
}
```

And the data sent back might look like:

```json
{
    "id": 17853,
    "roles": []
}
```

## Using JSON

In our code, interacting with JSON in typically involves two main operations: parsing JSON and generating JSON. 

### Parsing JSON
Parsing JSON involves converting a JSON string into a data structure that can be used in your code, such as objects, arrays, dictionaries, or maps, depending on the programming language.

In JavaScript, you can use the `JSON.parse()` method to parse a JSON string into a JavaScript object.

```javascript
const jsonString = '{"name": "John Doe", "age": 30}';
const jsonObject = JSON.parse(jsonString);
console.log(jsonObject.name); // Output: John Doe
console.log(jsonObject.age); // Output: 30
```

In Python, you can use the `json.loads()` function from the json module to parse a JSON string into a Python dictionary.

```python
import json

json_string = '{"name": "John Doe", "age": 30}'
json_object = json.loads(json_string)
print(json_object['name'])  # Output: John Doe
print(json_object['age'])   # Output: 30
```

### Generating JSON
Generating JSON involves converting data structures (such as objects, arrays, dictionaries, or maps) into a JSON string.

In JavaScript, you can use the `JSON.stringify()` method to convert a JavaScript object into a JSON string.

```javascript
const jsonObject = { name: "John Doe", age: 30 };
const jsonString = JSON.stringify(jsonObject);
console.log(jsonString); // Output: {"name":"John Doe","age":30}
```

In Python, you can use the `json.dumps()` function from the json module to convert a Python dictionary into a JSON string.

```python
import json

json_object = {'name': 'John Doe', 'age': 30}
json_string = json.dumps(json_object)
print(json_string)  # Output: {"name": "John Doe", "age": 30}
```

### Deserializing JSON

Deserializing JSON refers to the process of converting a JSON string into an object or data structure that can be used within your code. This process typically involves parsing the JSON string and mapping its key-value pairs to corresponding fields or properties of an object.

Here's an example in C# or converting a string of JSON to an instance of the Person class:

```c#
using Newtonsoft.Json;

string jsonString = "{\"name\": \"John Doe\", \"age\": 30}";
Person person = JsonConvert.DeserializeObject<Person>(jsonString);

class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```

Typically you deserialize JSON when you receive JSON - for instance you write the API endpoint that accepts JSON being sent to it.

### Serializing JSON

Serializing JSON refers to the process of converting an object or data structure into a JSON string. This process typically involves converting the fields or properties of an object into key-value pairs in a JSON object.

Normally you serialize when you want to *send* JSON to an endpoint.

```c#
using Newtonsoft.Json;

Person person = new Person { Name = "John Doe", Age = 30 };
string jsonString = JsonConvert.SerializeObject(person);

class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```