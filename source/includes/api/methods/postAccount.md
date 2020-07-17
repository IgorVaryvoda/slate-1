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
curl --request POST \
  --url https://api.sirv.com/v2/account \
  --header 'authorization: Bearer BEARER_TOKEN_HERE' \
  --header 'content-type: application/json' \
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

Use this method to change the account options. You can enable or disable JS/CSS file minification. You can also enable/disable automatic fetching via HTTP or S3 from a remote location.

### Query string


None


### Body payload


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
< date: Fri, 17 Jul 2020 16:23:37 GMT
< content-length: 0
< connection: close
< x-ratelimit-limit: 50
< x-ratelimit-remaining: 42
< x-ratelimit-reset: 1595003234
< x-ratelimit-type: rest:post:account
< access-control-allow-origin: *
< access-control-expose-headers: *
< cache-control: no-cache
< server: Sirv.API
< strict-transport-security: max-age=31536000


```