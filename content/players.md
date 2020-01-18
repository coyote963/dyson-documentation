## About Players

Endpoints relating to players. Player is the base model that gamemode profiles are based off of. Each player endpoint is uniquely identified by their "platform" and "profile". Platform is what game store they got bman from `0 = steam, 1 = discord, 2 = itch.io 3 = gamejolt`. The colors of each player is stored as a gamejolt color value

### List players

Lists all the players in the database. By default this only lists 10 entries and the first page. Other options you can specify what page you want. This is great for pagination on websites and keeps requests fast. Each API call also returns the total number of pages in the database. 

If you don't provide a pagenumber it will automatically default to the first page.

```endpoint
GET /players/{pagenumber}
```

#### Example request

```curl
$ curl https://bman.gg/players/{pagenumber}
```

```javascript
var request = require('request');

var options = {
    url: 'https://bman.gg/players/{pagenumber}'
};

function callback(error, response, body) {
    if (!error && response.statusCode == 200) {
        console.log(body);
    }
}

request(options, callback);
```

```python
import requests

response = requests.get('https://bman.gg/players/{pagenumber}')
```

#### Example response

```json
{
  "docs" : [
    {
      "_id" : {
        "profile" : "76561197960287930",
        "platform" : "0"
      },
      "ip" : [
        "127.0.0.1"
      ],
      "name" : [
        "gabelogannewell"
      ],
      "color" : "10789796",
      "premium" : "1",
      "hat" : "1"
    }
  ],
  "totalDocs": 2006,
  "limit": 10,
  "totalPages": 201,
  "page": 1,
  "pagingCounter": 1,
  "hasPrevPage": false,
  "hasNextPage": true,
  "prevPage": null,
  "nextPage": 2
}
```

### Search by name

Searches the player database for a player's name. It searches by the substring of every player's name. It is case insensitive and returns all the results that contain the search term

```endpoint
GET players/name/{name}
```

#### Example request

```curl
curl https://bman.gg/players/name/{name}
```


```javascript
var request = require('request');

var options = {
    url: 'https://bman.gg/players/name/{name}'
};

function callback(error, response, body) {
    if (!error && response.statusCode == 200) {
        console.log(body);
    }
}

request(options, callback);
```

```python
import requests

response = requests.get('https://bman.gg/players/name/{name}')
```

#### Example response

```json
[
    {
        "_id": {
            "platform": {store},
            "profile": {steamid}
        },
        "ip": [
            {ip},
            {ip}
        ],
        "name": [
            {name},
            {name}
        ],
        "color": {color},
        "hat": {hat},
        "premium": {premium status}
    },
    {
        "_id": {
            "platform": {store},
            "profile": {steamid}
        },
        "ip": [
            {ip},
            {ip}
        ],
        "name": [
            {name},
            {name}
        ],
        "color": {color},
        "hat": {hat},
        "premium": {premium status}
    }
]
```

### Retrieve a player

Returns a single player.

```endpoint
GET /players/{profileid}/platform/{platform}
```

Retrieve information for a single player. The profile id and the platform in combination uniquely identify a player, so this request will return at most one record. `platform` is a number representing steam, discord, itch.io or gamejolt. `profileid` is their id on that platform.

#### Example request

```curl
curl https://bman.gg/players/76561198303147008/platform/0
```


```python
import requests

response = requests.get('https://bman.gg/players/76561198303147008/platform/0')
```

```javascript
var request = require('request');

var options = {
    url: 'https://bman.gg/players/76561198303147008/platform/0'
};

function callback(error, response, body) {
    if (!error && response.statusCode == 200) {
        console.log(body);
    }
}

request(options, callback);
```

#### Example response

```json
[
    {
        "_id": {
            "platform": "0",
            "profile": "76561198303147008"
        },
        "ip": [
            "127.0.0.1"
        ],
        "name": [
            "coyote and bird"
        ],
        "color": "1783114",
        "hat": "0",
        "premium": "1"
    }
]
```
