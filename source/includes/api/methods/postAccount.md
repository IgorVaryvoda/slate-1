## Update account info

```python
import http.client

conn = http.client.HTTPSConnection("api.sirv.com")

payload = "{\"fetching\":{\"enabled\":false}}"

headers = {
    'content-type': "application/json",
    'authorization': "Bearer BEARER_TOKEN_HERE"
    }

conn.request("POST", "/v2/account", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```shell
curl --request POST \\
  --url https://api.sirv.com/v2/account \\
  --header 'authorization: Bearer BEARER_TOKEN_HERE' \\
  --header 'content-type: application/json' \\
  --data '{"fetching":{"enabled":false}}'
```

```javascript--node
var http = require("https");

var options = {
  "method": "POST",
  "hostname": "api.sirv.com",
  "port": null,
  "path": "/v2/account",
  "headers": {
    "content-type": "application/json",
    "authorization": "Bearer BEARER_TOKEN_HERE"
  }
};

var req = http.request(options, function (res) {
  var chunks = [];

  res.on("data", function (chunk) {
    chunks.push(chunk);
  });

  res.on("end", function () {
    var body = Buffer.concat(chunks);
    console.log(body.toString());
  });
});

req.write("{\"fetching\":{\"enabled\":false}}");
req.end();
```

```javascript
var data = "{\"fetching\":{\"enabled\":false}}";

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.sirv.com/v2/account");
xhr.setRequestHeader("content-type", "application/json");
xhr.setRequestHeader("authorization", "Bearer BEARER_TOKEN_HERE");

xhr.send(data);
```

```java
HttpResponse<String> response = Unirest.post("https://api.sirv.com/v2/account")
  .header("content-type", "application/json")
  .header("authorization", "Bearer BEARER_TOKEN_HERE")
  .body("{\"fetching\":{\"enabled\":false}}")
  .asString();
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.sirv.com/v2/account",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => "{\"fetching\":{\"enabled\":false}}",
  CURLOPT_HTTPHEADER => array(
    "authorization: Bearer BEARER_TOKEN_HERE",
    "content-type: application/json"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

```ruby
require 'uri'
require 'net/http'
require 'openssl'

url = URI("https://api.sirv.com/v2/account")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE

request = Net::HTTP::Post.new(url)
request["content-type"] = 'application/json'
request["authorization"] = 'Bearer BEARER_TOKEN_HERE'
request.body = "{\"fetching\":{\"enabled\":false}}"

response = http.request(request)
puts response.read_body
```

```swift
import Foundation

let headers = [
  "content-type": "application/json",
  "authorization": "Bearer BEARER_TOKEN_HERE"
]

let postData = NSData(data: "{"fetching":{"enabled":false}}".data(using: String.Encoding.utf8)!)

let request = NSMutableURLRequest(url: NSURL(string: "https://api.sirv.com/v2/account")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

```csharp
var client = new RestClient("https://api.sirv.com/v2/account");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/json");
request.AddHeader("authorization", "Bearer BEARER_TOKEN_HERE");
request.AddParameter("application/json", "{\"fetching\":{\"enabled\":false}}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

```go
package main

import (
	"fmt"
	"strings"
	"net/http"
	"io/ioutil"
)

func main() {

	url := "https://api.sirv.com/v2/account"

	payload := strings.NewReader("{\"fetching\":{\"enabled\":false}}")

	req, _ := http.NewRequest("POST", url, payload)

	req.Header.Add("content-type", "application/json")
	req.Header.Add("authorization", "Bearer BEARER_TOKEN_HERE")

	res, _ := http.DefaultClient.Do(req)

	defer res.Body.Close()
	body, _ := ioutil.ReadAll(res.Body)

	fmt.Println(res)
	fmt.Println(string(body))

}
```

Use this method to change the account options. You can enable or disable JS/CSS file minification. You can also enable/disable automatic fetching via HTTP or S3 from a remote location.

### Query string


None


### Body payload


Example:

<div class="center-column"></div>
```json
{
  "fetching": {
    "enabled": false
  }
}
```



JSON Schema:

<div class="center-column"></div>
```json
{
  "type": "object",
  "properties": {
    "minify": {
      "type": "object",
      "properties": {
        "enabled": {
          "description": "Enable or disable automatic minification of JS/CSS files",
          "type": "boolean"
        }
      },
      "additionalProperties": false,
      "patterns": [],
      "required": [
        "enabled"
      ]
    },
    "fetching": {
      "type": "object",
      "properties": {
        "enabled": {
          "examples": [
            false
          ],
          "example": false,
          "type": "boolean"
        },
        "type": {
          "oneOf": [
            {
              "enum": [
                "http",
                "s3"
              ],
              "type": "string"
            }
          ]
        },
        "http": {
          "oneOf": [
            {
              "type": "object",
              "properties": {
                "auth": {
                  "type": "object",
                  "properties": {
                    "enabled": {
                      "type": "boolean"
                    },
                    "username": {
                      "oneOf": [
                        {
                          "type": "string"
                        }
                      ]
                    },
                    "password": {
                      "oneOf": [
                        {
                          "type": "string"
                        }
                      ]
                    }
                  },
                  "additionalProperties": false,
                  "patterns": [],
                  "required": [
                    "enabled"
                  ]
                },
                "url": {
                  "type": "string",
                  "format": "uri"
                }
              },
              "additionalProperties": false,
              "patterns": [],
              "required": [
                "url"
              ]
            }
          ]
        },
        "s3": {
          "oneOf": [
            {
              "type": "object",
              "properties": {
                "endpoint": {
                  "type": "string"
                },
                "accessKeyId": {
                  "type": "string"
                },
                "secretAccessKey": {
                  "type": "string"
                },
                "bucket": {
                  "type": "string"
                },
                "prefix": {
                  "type": "string"
                },
                "forcePathStyle": {
                  "type": "boolean"
                }
              },
              "additionalProperties": false,
              "patterns": [],
              "required": [
                "accessKeyId",
                "secretAccessKey",
                "bucket"
              ]
            }
          ]
        }
      },
      "additionalProperties": false,
      "patterns": [],
      "required": [
        "enabled"
      ]
    },
    "aliases": {
      "type": "object",
      "properties": {},
      "additionalProperties": false,
      "patterns": [
        {
          "rule": {
            "type": "object",
            "properties": {
              "cdn": {
                "type": "boolean"
              },
              "prefix": {
                "type": "string"
              },
              "defaultProfile": {
                "type": "string"
              }
            },
            "additionalProperties": false,
            "patterns": []
          }
        }
      ]
    }
  },
  "additionalProperties": false,
  "patterns": []
}
```


### Response

Example response:

<div class="center-column"></div>
```
< HTTP/1.1 200
< date: Sat, 18 Jul 2020 11:45:50 GMT
< content-length: 0
< connection: close
< x-ratelimit-limit: 50
< x-ratelimit-remaining: 46
< x-ratelimit-reset: 1595075478
< x-ratelimit-type: rest:post:account
< access-control-allow-origin: *
< access-control-expose-headers: *
< cache-control: no-cache
< server: Sirv.API
< strict-transport-security: max-age=31536000

/ no response body: HTTP status 200 means SUCCESS /
```
