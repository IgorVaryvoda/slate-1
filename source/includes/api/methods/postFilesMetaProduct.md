## Set product meta

```python
import http.client

conn = http.client.HTTPSConnection("api.sirv.com")

payload = "{\"id\":\"LLBB77\",\"name\":\"Blue Lake Card\",\"brand\":\"BLUE LAKE LLC\",\"category1\":\"Cards\",\"category2\":\"Lakes\"}"

headers = {
    'content-type': "application/json",
    'authorization': "Bearer BEARER_TOKEN_HERE"
    }

conn.request("POST", "/v2/files/meta/product?filename=%2FREST%20API%20Examples%2Fblue-lake.jpg", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```shell
curl --request POST \\
  --url 'https://api.sirv.com/v2/files/meta/product?filename=%2FREST%20API%20Examples%2Fblue-lake.jpg' \\
  --header 'authorization: Bearer BEARER_TOKEN_HERE' \\
  --header 'content-type: application/json' \\
  --data '{"id":"LLBB77","name":"Blue Lake Card","brand":"BLUE LAKE LLC","category1":"Cards","category2":"Lakes"}'
```

```javascript--node
var http = require("https");

var options = {
  "method": "POST",
  "hostname": "api.sirv.com",
  "port": null,
  "path": "/v2/files/meta/product?filename=%2FREST%20API%20Examples%2Fblue-lake.jpg",
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

req.write("{\"id\":\"LLBB77\",\"name\":\"Blue Lake Card\",\"brand\":\"BLUE LAKE LLC\",\"category1\":\"Cards\",\"category2\":\"Lakes\"}");
req.end();
```

```javascript
var data = "{\"id\":\"LLBB77\",\"name\":\"Blue Lake Card\",\"brand\":\"BLUE LAKE LLC\",\"category1\":\"Cards\",\"category2\":\"Lakes\"}";

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === this.DONE) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "https://api.sirv.com/v2/files/meta/product?filename=%2FREST%20API%20Examples%2Fblue-lake.jpg");
xhr.setRequestHeader("content-type", "application/json");
xhr.setRequestHeader("authorization", "Bearer BEARER_TOKEN_HERE");

xhr.send(data);
```

```java
HttpResponse<String> response = Unirest.post("https://api.sirv.com/v2/files/meta/product?filename=%2FREST%20API%20Examples%2Fblue-lake.jpg")
  .header("content-type", "application/json")
  .header("authorization", "Bearer BEARER_TOKEN_HERE")
  .body("{\"id\":\"LLBB77\",\"name\":\"Blue Lake Card\",\"brand\":\"BLUE LAKE LLC\",\"category1\":\"Cards\",\"category2\":\"Lakes\"}")
  .asString();
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api.sirv.com/v2/files/meta/product?filename=%2FREST%20API%20Examples%2Fblue-lake.jpg",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => "{\"id\":\"LLBB77\",\"name\":\"Blue Lake Card\",\"brand\":\"BLUE LAKE LLC\",\"category1\":\"Cards\",\"category2\":\"Lakes\"}",
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

url = URI("https://api.sirv.com/v2/files/meta/product?filename=%2FREST%20API%20Examples%2Fblue-lake.jpg")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE

request = Net::HTTP::Post.new(url)
request["content-type"] = 'application/json'
request["authorization"] = 'Bearer BEARER_TOKEN_HERE'
request.body = "{\"id\":\"LLBB77\",\"name\":\"Blue Lake Card\",\"brand\":\"BLUE LAKE LLC\",\"category1\":\"Cards\",\"category2\":\"Lakes\"}"

response = http.request(request)
puts response.read_body
```

```swift
import Foundation

let headers = [
  "content-type": "application/json",
  "authorization": "Bearer BEARER_TOKEN_HERE"
]

let postData = NSData(data: "{"id":"LLBB77","name":"Blue Lake Card","brand":"BLUE LAKE LLC","category1":"Cards","category2":"Lakes"}".data(using: String.Encoding.utf8)!)

let request = NSMutableURLRequest(url: NSURL(string: "https://api.sirv.com/v2/files/meta/product?filename=%2FREST%20API%20Examples%2Fblue-lake.jpg")! as URL,
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
var client = new RestClient("https://api.sirv.com/v2/files/meta/product?filename=%2FREST%20API%20Examples%2Fblue-lake.jpg");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/json");
request.AddHeader("authorization", "Bearer BEARER_TOKEN_HERE");
request.AddParameter("application/json", "{\"id\":\"LLBB77\",\"name\":\"Blue Lake Card\",\"brand\":\"BLUE LAKE LLC\",\"category1\":\"Cards\",\"category2\":\"Lakes\"}", ParameterType.RequestBody);
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

	url := "https://api.sirv.com/v2/files/meta/product?filename=%2FREST%20API%20Examples%2Fblue-lake.jpg"

	payload := strings.NewReader("{\"id\":\"LLBB77\",\"name\":\"Blue Lake Card\",\"brand\":\"BLUE LAKE LLC\",\"category1\":\"Cards\",\"category2\":\"Lakes\"}")

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

Use this API method to set product meta fields for an image. This can be used by retailers for organizing images into product groups for an ecommerce store.

### Query string


Parameter | Type | Description | Example
--------- | ---- | ----------- | ------- 
filename | string |  | /REST API Examples/blue-lake.jpg


### Body payload


Example:

<div class="center-column"></div>
```json
{
  "id": "LLBB77",
  "name": "Blue Lake Card",
  "brand": "BLUE LAKE LLC",
  "category1": "Cards",
  "category2": "Lakes"
}
```



JSON Schema:

<div class="center-column"></div>
```json
{
  "type": "object",
  "properties": {
    "id": {
      "examples": [
        "LLBB77"
      ],
      "example": "LLBB77",
      "type": "string",
      "maxLength": 256
    },
    "name": {
      "examples": [
        "Blue Lake Card"
      ],
      "example": "Blue Lake Card",
      "type": "string",
      "maxLength": 256
    },
    "brand": {
      "examples": [
        "BLUE LAKE LLC"
      ],
      "example": "BLUE LAKE LLC",
      "type": "string",
      "maxLength": 256
    },
    "category1": {
      "examples": [
        "Cards"
      ],
      "example": "Cards",
      "type": "string",
      "maxLength": 256
    },
    "category2": {
      "examples": [
        "Lakes"
      ],
      "example": "Lakes",
      "type": "string",
      "maxLength": 256
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
< date: Sat, 18 Jul 2020 11:46:08 GMT
< content-length: 0
< connection: close
< x-ratelimit-limit: 7000
< x-ratelimit-remaining: 6866
< x-ratelimit-reset: 1595075478
< x-ratelimit-type: rest:global
< access-control-allow-origin: *
< access-control-expose-headers: *
< cache-control: no-cache
< server: Sirv.API
< strict-transport-security: max-age=31536000

/ no response body: HTTP status 200 means SUCCESS /
```
