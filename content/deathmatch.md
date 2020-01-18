## About Deathmatch

These are all endpoints related to the gamemode: Deathmatch. By default the database stores match information, player rating profiles, player kills, chat messages etc. All player profiles are backed by a player profile, however not every player has a deathmatch profile.

### List deathmatch profiles

Deathmatch profiles are statistics related to the players deathmatch history. This route allows you to list the deathmatch profiles, retrieve 10 records per api call. Specify the pagenumber in the url and if there is no pagenumber provided it will return the first page by default. Note that in the example response only a single record is listed for brevity.

```endpoint
GET /dmprofiles/{pagenumber}
```

#### Example request

```curl
$ curl https://bman.gg/dmprofiles/{pagenumber}
```

```javascript
var request = require('request');

var options = {
    url: 'https://bman.gg/dmprofiles/{pagenumber}'
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

response = requests.get('https://bman.gg/dmprofiles/{pagenumber}')
```

#### Example response

```json
{
    "docs": [
        {
            "_id": "5dcf84a5f97ad754e3b9a044",
            "player": {
                "platform": "0",
                "profile": "76561198803977655"
            },
            "mu": "27.07298087932027",
            "sigma": "0.7966123143415406",
            "kills": "115",
            "deaths": "103",
            "last_updated": "Wed Jan 15 2020 18:48:47 GMT-0500 (Eastern Standard Time)"
        },
    ],
    "totalDocs": 986,
    "limit": 10,
    "totalPages": 99,
    "page": null,
    "pagingCounter": null,
    "hasPrevPage": false,
    "hasNextPage": false,
    "prevPage": null,
    "nextPage": null
}
```

### Display the full profile

This basically combines all the data on a deathmatch profile and player profile. Provide a `profileID` and a `storeID` (steam, discord, itch.io, gamejolt) and it will return a deathmatch profile with all the information displayed in full.

```endpoint
GET dmprofiles/full/{profileID}/platform/{storeID}
```

#### Example request

```curl
curl https://bman.gg/dmprofiles/full/{profileID}/platform/{storeID}
```


```javascript
var request = require('request');

var options = {
    url: 'https://bman.gg/dmprofiles/full/{profileID}/platform/{storeID}'
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

response = requests.get('https://bman.gg/dmprofiles/full/{profileID}/platform/{storeID}')
```

#### Example response

```json
[
    {
        "_id": "5dd03bb5e1d2bd59172151c2",
        "player": {
            "name": [
                "White Fox",
                "Bunny Boi"
            ],
            "_id": {
                "platform": "0",
                "profile": "76561198140027269"
            },
            "color": "255",
            "hat": "27",
            "premium": "1"
        },
        "mu": "24.09227820175617",
        "sigma": "3.295183723276668",
        "kills": "0",
        "deaths": "0",
        "last_updated": "Sun Nov 17 2019 16:00:43 GMT-0500 (Eastern Standard Time)"
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
