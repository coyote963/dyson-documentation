## Dyson City API

Welcome to the Dyson City API! Here you can reference how to retrieve data from the Boring Man databases using HTTP or TCP/UDP. This API was designed with `www.bman.gg` in mind, so the endpoints are the minimal endpoints necessary to build the functioning page. However, I am open to suggestions to new endpoints.

### How does Dyson.city work? ###

Every time kills, chats, or players join a Boring Man V2 server, their information is stored and updated in a central database. Each packet of data is transfered via the RCON interface provided by the game.

After this information is stored, you can query data from the database using the endpoints documented below. As for now there is no rate limit.

Rating system is implemented with Microsoft's Trueskill rating system, that uses Bayesian inference to dynamically adjust player's ratings. If you would like to know more please read Microsoft's documentation on how their rating system works.