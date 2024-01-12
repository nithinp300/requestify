# requestify

A Python program that reads a json/yml file for request data and sends the request

## Installation

First, clone the repo:

```sh
$ git clone https://github.com/nithinp300/requestify.git
$ cd requestify
```

Then, install the dependencies:

```sh
$ pip install -r requirements.txt
```

## Usage example

### To get help with commandline arguments

```sh
python requestify/requestify.py --help
```

### Using Command-line Arguments

```sh
python requestify/requestify.py -f "some/folder/myrequest.yml"
```

(or)

```sh
python requestify/requestify.py -f "some/folder/myrequest.json"
```

### Colorize Output

```sh
python requestify/requestify.py -f "some/folder/myrequest.yml" -c
```

## IO Redirection

the response is written to stdout and headers/status are written to stderr so that users can take IO redirection to their advantage. This works on windows, linux and mac.

```sh
python requestify/requestify.py -f "some/folder/myrequest.yml" > res.json 2> res_headers.txt
```

both stdout and stderr can be redirected to the same file

```sh
python requestify/requestify.py -f "some/folder/myrequest.yml" > res.txt 2>&1
```

## Sample request file (`myrequest.yml`)

### GET

```yaml
url: https://cdn.animenewsnetwork.com/encyclopedia/api.xml?anime=4658
method: get
params:
  offset: 2
  limit: 100
headers:
  accept: text/xml
  accept-language: en
timeout: 5000
```

#### File Download (`python requestify/requestify.py -f "some/folder/myrequest.yml" > book.pdf`)

```yaml
url: http://do1.dr-chuck.com/pythonlearn/EN_us/pythonlearn.pdf
method: get
```

### POST

```yaml
url: https://jsonplaceholder.typicode.com/todos/
method: POST
headers:
  Authorization: Basic bXl1c2VybmFtZTpteXBhc3N3b3Jk
  content-type: application/json
data:
  title: walk the dog
  completed: false
timeout: 5000
```

### PUT

```yaml
url: https://jsonplaceholder.typicode.com/todos/1
method: PUT
headers:
  content-type: application/json
data:
  title: walk the dog
  completed: true
timeout: 5000
```

### DELETE

```yaml
url: https://jsonplaceholder.typicode.com/todos/1
method: DELETE
```

## Complete request file with all available fields (`myrequest.yml`)

```yaml
method: XXX # (REQUIRED) GET, OPTIONS, HEAD, POST, PUT, PATCH, or DELETE
url: XXX # (REQUIRED) must be prefixed with http:// or https://

params: # url query parameters. have as many as you like
  offset: 0
  limit: 10

data: # data for POST
  name: john
  age: 22
  hobbies:
    - running
    - eating
    - sleeping

# you can also type data in json format instead of yaml
data: |
  {
    "name": "john",
    "age": 22,
    "hobbies": ["running", "eating", "sleeping"]
  }

headers: # have as many as you like
  Content-Type: application/json
  Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c


cookies: # have as many as you like
  mycookie: cookievalue
  myothercookie: othercookievalue

timeout: 3.14 # seconds

allow_redirects: true # true or false

proxies: # have as many as you like
  http: http://10.10.1.10:3128
  https: https://10.10.1.11:1080
  ftp: ftp://10.10.1.10:3128

# EITHER verify server's TLS certificate. true or false
verify: true
# OR path to a CA bundle to use
verify: some/folder/cacert.crt

# EITHER path to single ssl client cert file (*.pem)
cert: some/folder/client.pem
# OR (*.cert), (*.key) pair.
cert:
  - some/folder/client.cert
  - some/folder/client.key

```

## Contributing

We welcome contributions to requestify! These are the many ways you can help:

- Submit patches and features
- Report bugs