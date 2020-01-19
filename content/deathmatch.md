## Deathmatch Profiles

Deathmatch profiles contain information relating to a player's activity in Spasman's Deathmatch server. These profiles use the same Trueskill rating system that is used in TDM but simply applied to 1v1's. 

### List deathmatch profiles

Deathmatch profiles are statistics related to the players deathmatch history. This route allows you to list the deathmatch profiles, retrieve 10 records per api call. Specify the pagenumber in the url and if there is no pagenumber provided it will return the first page by default. Note that in the example response only a single record is listed for brevity.

```endpoint
GET /dmprofiles/{pagenumber}
```

#### Example request

```curl
$ curl https://api.bman.gg/dmprofiles/{pagenumber}
```

```javascript
var request = require('request');

var options = {
    url: 'https://api.bman.gg/dmprofiles/{pagenumber}'
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

response = requests.get('https://api.bman.gg/dmprofiles/{pagenumber}')
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
### List of players ranked

This route is for returning a list of players ranked based on their Elo rating. It automatically performs the adjustment for sigma ratings. Pass in the optional page to get the corresponding page. Omitting it will return the first page.

```endpoint
GET dmprofiles/rankings
```

#### Example request

```curl
curl https://api.bman.gg/dmprofiles/full/76561198140027269/platform/0
```

```javascript
var request = require('request');

var options = {
    url: 'https://api.bman.gg/dmprofiles/full/76561198140027269/platform/0'
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

response = requests.get('https://api.bman.gg/dmprofiles/full/76561198140027269/platform/0')
```

#### Example response

```json
{
    "docs": [
        {
            "mu": 30.57994960821335,
            "sigma": 0.9425143812467252,
            "result": 27.752406464473175,
            "name": "Moon"
        },
        {
            "mu": 30.19622481800646,
            "sigma": 0.8166518500203079,
            "result": 27.746269267945536,
            "name": "Nova"
        },
        ...
    ],
    "totalDocs": 381,
    "limit": 10,
    "page": 1,
    "totalPages": 39,
    "pagingCounter": 1,
    "hasPrevPage": false,
    "hasNextPage": true,
    "prevPage": null,
    "nextPage": 2
}
```

### Get the full profile

This basically combines all the data on a deathmatch profile and player profile. Provide a `profileID` and a `storeID` (steam, discord, itch.io, gamejolt) and it will return a deathmatch profile with all the information displayed in full.

```endpoint
GET dmprofiles/full/{profileID}/platform/{storeID}
```

#### Example request

```curl
curl https://api.bman.gg/dmprofiles/full/76561198140027269/platform/0
```


```javascript
var request = require('request');

var options = {
    url: 'https://api.bman.gg/dmprofiles/full/76561198140027269/platform/0'
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

response = requests.get('https://api.bman.gg/dmprofiles/full/76561198140027269/platform/0')
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

### Get a single player

Gets the deathmatch profile of a single user. This doesn't combine the information from the player information. The reason to use this over the more detailed full profile is that it is two times faster. Use this endpoint when information on the player isn't completely essential. 

```endpoint
GET dmprofiles/{profileID}/platform/{storeID}
```


#### Example request

```curl
curl https://api.bman.gg/dmprofiles/76561198140027269/platform/0
```


```python
import requests

response = requests.get('https://api.bman.gg/dmprofiles/76561198140027269/platform/0')
```

```javascript
var request = require('request');

var options = {
    url: 'https://api.bman.gg/players/dmprofiles/76561198140027269/platform/0'
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
        "_id": "5dd03bb5e1d2bd59172151c2",
        "player": {
            "platform": "0",
            "profile": "76561198140027269"
        },
        "mu": "24.09227820175617",
        "sigma": "3.295183723276668",
        "kills": "0",
        "deaths": "0",
        "last_updated": "Sun Nov 17 2019 16:00:43 GMT-0500 (Eastern Standard Time)"
    }
]
```

## Deathmatch Kills

These routes allow for the querying of information pertaining to kills. Kill data is useful for understanding the context of each elimination, this includes weapon used, death coordinates, and kill coordinates. Kills also uniquely reference a match which allows users to bundle kills into matches.

### List deathmatch kills

This will list deathmatch kills sorted in ascending time. As usual, you can optionally submit a page number and omitting it will simply return the first page. 

```endpoint
GET dmkills/{page}
```


#### Example request

```curl
curl https://api.bman.gg/dmkills
```


```python
import requests

response = requests.get('https://api.bman.gg/dmkills')
```

```javascript
var request = require('request');

var options = {
    url: 'https://api.bman.gg/players/dmkills'
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
{
    "docs": [
        {
            "killer_rating": {
                "mu": 27.678012029874072,
                "sigma": 0.7906125269412195,
                "mu_delta": 0.09591250758511904,
                "sigma_delta": -0.0003333979958908273
            },
            "victim_rating": {
                "mu": 27.76942863425856,
                "sigma": 0.7955871372882849,
                "mu_delta": -0.09713812389775,
                "sigma_delta": -0.0004520302848265434
            },
            "_id": "5e2399608ab5eb05970bd3cb",
            "killer": {
                "platform": "0",
                "profile": "76561198238477762"
            },
            "victim": {
                "platform": "0",
                "profile": "76561198386200919"
            },
            "weapon": "20",
            "killer_location": "5782.67,2399.97",
            "victim_location": "5200.52,2424.99",
            "date_created": "2020-01-18T23:33:50.575Z",
            "match": "5e2398018ab5eb05970bd3c5"
        },
        ...
    ],
    "totalDocs": 54351,
    "limit": 10,
    "totalPages": 5436,
    "page": null,
    "pagingCounter": null,
    "hasPrevPage": false,
    "hasNextPage": false,
    "prevPage": null,
    "nextPage": null
```

### List of deathmatch kills populated

With this API endpoint you can display the full player information. It will fill in all the information from the player information from the Players database. Please use this sparingly as it is a rather slow operation. Page number is optional. There is a massive amount of information sent back...

```endpoint
GET dmkills/full/{page}
```

#### Example request 
```curl https://api.bman.gg/dmkills/1
```


#### Example request

```curl
curl https://api.bman.gg/dmkills/full/1
```


```python
import requests

response = requests.get('https://api.bman.gg/dmkills/full/1')
```

```javascript
var request = require('request');

var options = {
    url: 'https://api.bman.gg/dmkills/full/1'
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
{
    "docs": [
        {
            "killer_rating": {
                "mu": 27.678012029874072,
                "sigma": 0.7906125269412195,
                "mu_delta": 0.09591250758511904,
                "sigma_delta": -0.0003333979958908273
            },
            "victim_rating": {
                "mu": 27.76942863425856,
                "sigma": 0.7955871372882849,
                "mu_delta": -0.09713812389775,
                "sigma_delta": -0.0004520302848265434
            },
            "_id": "5e2399608ab5eb05970bd3cb",
            "killer": [
                {
                    "_id": {
                        "platform": "0",
                        "profile": "76561198238477762"
                    },
                    "name": [
                        "Taterazay"
                    ],
                    "color": "0",
                    "hat": "19",
                    "premium": "1"
                },
                {
                    "_id": {
                        "platform": "0",
                        "profile": "76561198386200919"
                    },
                    "name": [
                        "chengkinhoken"
                    ],
                    "color": "16777215",
                    "hat": "0",
                    "premium": "0"
                }
            ],
            "victim": [
                {
                    "_id": {
                        "platform": "0",
                        "profile": "76561198238477762"
                    },
                    "name": [
                        "Taterazay"
                    ],
                    "color": "0",
                    "hat": "19",
                    "premium": "1"
                },
                {
                    "_id": {
                        "platform": "0",
                        "profile": "76561198386200919"
                    },
                    "name": [
                        "chengkinhoken"
                    ],
                    "color": "16777215",
                    "hat": "0",
                    "premium": "0"
                }
            ],
            "weapon": "20",
            "killer_location": "5782.67,2399.97",
            "victim_location": "5200.52,2424.99",
            "date_created": "2020-01-18T23:33:50.575Z",
            "match": {
                "_id": "5e2398018ab5eb05970bd3c5",
                "map_name": "Boring Lake",
                "date_created": "2020-01-18T23:33:50.534Z",
                "date_ended": "2020-01-18T23:53:31.899Z"
            }
        },
        ...
    ],
    "totalDocs": 54351,
    "limit": 10,
    "totalPages": 5436,
    "page": 1,
    "pagingCounter": 1,
    "hasPrevPage": false,
    "hasNextPage": true,
    "prevPage": null,
    "nextPage": 2
}
```

### Get all the kills from a match

Sometimes you want to see a list of every kill that occured during a deathmatch game. This is the endpoint to do that. Pass in the unique ID corresponding to every match.

```endpoint
GET https://api.bman.gg/dmkills/findMatch
```


#### Example request

```curl
curl https://api.bman.gg/dmkills/match/5e2398018ab5eb05970bd3c5
```


```python
import requests

response = requests.get('https://api.bman.gg/dmkills/match/5e2398018ab5eb05970bd3c5')
```

```javascript
var request = require('request');

var options = {
    url: 'https://api.bman.gg/players/dmkills/match/5e2398018ab5eb05970bd3c5'
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
        "killer_rating": {
            "mu": 27.678012029874072,
            "sigma": 0.7906125269412195,
            "mu_delta": 0.09591250758511904,
            "sigma_delta": -0.0003333979958908273
        },
        "victim_rating": {
            "mu": 27.76942863425856,
            "sigma": 0.7955871372882849,
            "mu_delta": -0.09713812389775,
            "sigma_delta": -0.0004520302848265434
        },
        "_id": "5e2399608ab5eb05970bd3cb",
        "killer": {
            "platform": "0",
            "profile": "76561198238477762"
        },
        "victim": {
            "platform": "0",
            "profile": "76561198386200919"
        },
        "weapon": "20",
        "killer_location": "5782.67,2399.97",
        "victim_location": "5200.52,2424.99",
        "date_created": "2020-01-18T23:33:50.575Z",
        "match": "5e2398018ab5eb05970bd3c5"
    },
    ...
]
```

### Get all the kills from a certain player

This endpoint is for retrieving the list of all kills gotten by a certain player. Provide the `profileID` and `storeID` to ensure that you get the kills for the correct player. `page` is optional.

```endpoint
GET https://api.bman.gg/dmkills/{profileID}/platform/{platformID}/{page}
```

#### Example request

```curl
curl https://api.bman.gg/dmkills/76561198386200919/platform/0
```


```python
import requests

response = requests.get('https://api.bman.gg/dmkills/76561198386200919/platform/0')
```

```javascript
var request = require('request');

var options = {
    url: 'https://api.bman.gg/dmkills/76561198386200919/platform/0'
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
        "killer_rating": {
            "mu": 27.99689278551442,
            "sigma": 0.7919372021967669,
            "mu_delta": 0.08861771931542961,
            "sigma_delta": -0.00020557683284050388
        },
        "victim_rating": {
            "mu": 27.45321244953377,
            "sigma": 0.7880848710982954,
            "mu_delta": -0.08774767858041699,
            "sigma_delta": -0.00011647419008775639
        },
        "_id": "5e239a418ab5eb05970bd3d6",
        "killer": {
            "platform": "0",
            "profile": "76561198386200919"
        },
        "victim": {
            "platform": "0",
            "profile": "76561198238477762"
        },
        "weapon": "10",
        "killer_location": "4781.96,2345.38",
        "victim_location": "5162.49,2462.20",
        "date_created": "2020-01-18T23:33:50.575Z",
        "match": "5e2398018ab5eb05970bd3c5"
    },
    ...
]
```