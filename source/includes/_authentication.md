# Authentication

```shell
    curl -H "Content-Type: application/json" \
     -u YOUR_EMAIL:YOUR_TOKEN  \
    https://prod.practitest.com/api/v2/projects.json
# IS THE SAME AS:
    curl -H "Content-Type: application/json" \
    https://prod.practitest.com/api/v2/projects.json?developer_email=YOUR_EMAIL&api_token=YOUR_TOKEN
```


```csharp
TOKEN = "YOUR_TOKEN";
DEVELOPER_EMAIL = "YOUR_EMAIL";
String encoded =System.Convert.ToBase64String(System.Text.Encoding.GetEncoding("ISO-8859-1").GetBytes(username + ":" + password));
httpWebRequest.Headers.Add("Authorization", "Basic " + encoded);
```

```ruby
require 'net/http'
require 'net/https'
require 'uri'
require 'json'

URL   = "https://prod.practitest.com"
TOKEN = "xxx"
DEVELOPER_EMAIL= "my@mail.address"

uri = URI.parse("#{URL}/api/v2/projects.json")
http = Net::HTTP.new(uri.host, uri.port)
http.use_ssl = true
req = Net::HTTP::Get.new(uri.path)
req.basic_auth DEVELOPER_EMAIL, TOKEN
res = http.request(req)
puts res.body
```


```python
import httplib
import requests
from requests.auth import AuthBase
res = requests.get('https://prod.practitest.com/api/v2/projects.json', auth=('user@pt.com', 'dd2d9ddee2e9cd4861b1f0353375de1b4444d49'))
print res.status_code
print res.text
```

> This command: https://prod.practitest.com/api/v2/projects.json?api_token=xx&developer_email=admin%40pt.com&page[number]=1&page[size]=2", returns JSON structured like below:


```json
{
  "data": [
    {
      "id": "4581",
      "type": "projects",
      "attributes": {
        "name": "Sanity check (Rails 4)",
        "created-at": "2016-07-28T13:34:51Z",
        "automation-support": false,
        "enable-delete-issues": false,
        "time-management-support": false
      }
    },
    {
      "id": "4578",
      "type": "projects",
      "attributes": {
        "name": "Sanity Check (screen captures)",
        "created-at": "2016-06-20T11:32:52Z",
        "automation-support": false,
        "enable-delete-issues": true,
        "time-management-support": false
      }
    }
  ],
  "links": {
    "self": "https://prod.practitest.com/api/v2/projects.json?api_token=afb913899fc295e809255fbdb4fbc1fb37296250&developer_email=admin%40pt.com&page%5Bnumber%5D=1&page%5Bsize%5D=2",
    "next": "https://prod.practitest.com/api/v2/projects.json?api_token=afb913899fc295e809255fbdb4fbc1fb37296250&developer_email=admin%40pt.com&page%5Bnumber%5D=2&page%5Bsize%5D=2",
    "last": "https://prod.practitest.com/api/v2/projects.json?api_token=afb913899fc295e809255fbdb4fbc1fb37296250&developer_email=admin%40pt.com&page%5Bnumber%5D=3&page%5Bsize%5D=2"
  },
  "meta": {
    "current-page": 1,
    "next-page": 2,
    "prev-page": null,
    "total-pages": 3,
    "total-count": 5
  }
}
```


> Make sure to replace `YOUR_TOKEN` with your API token and `YOUR_EMAIL` with your email address.

PractiTest uses API tokens for authentication. You can create a new API token by going to the Account Settings - "API Tokens". Please visit this <a href="https://www.practitest.com/help/account/account-api-tokens/" target="_blank">API tokens</a> for more information.

API expects the API-token and developer email to be included in all API requests to the server.
They can be **either** in the header as basic authentication, **OR** as parameters in the query string (which is usually more convinient with browser's debugging)


<aside class="notice">
You must replace <code>YOUR_EMAIL</code> with your email address and <code>YOUR_TOKEN</code> with your custom API token.
See below why we'd like you to use your real developer email address.
</aside>

<aside class="success">
**Developer email** is not authenticated by the API. You can put there any email you want. But if you have errors, or bad syntax, the only way that we get back to you, would be if you put your valid email address. This way we can help you (almost) immediately if we see something wrong.
</aside>
