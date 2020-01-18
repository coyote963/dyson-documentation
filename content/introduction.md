## Dyson City API

Welcome to the Dyson City API! Here you can reference how to retrieve data from the Boring Man databases using HTTP or TCP/UDP. 

### How Dyson.city works? ###

Every time kills, chats, or players join a Boring Man V2 server, their information is stored and updated in a central database. Each packet of data is transfered via the RCON interface provided by the game.

After this information is stored, you can query data from the database using the endpoints documented below. As for now there is no rate limit.