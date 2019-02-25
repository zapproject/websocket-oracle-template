## MARKET SIGNAL ORACLE

- Purpose : to provide a subscription service based on Zap oracle platform to manage subscriptions and distribute information through authenticated websocket connections.
### WORK FLOW
*ORACLE*
- Oracle has an endpoint with curve set for a subscription service (not to be queried)
- Oracle creates authenticated websocket server
- Oracle implement method `getData` to get data from database or other source and emit data to authenticated connections
- Oracle run server to start listenting to connection, verify user and emitting data to connected users

*USER*
- User approve -> bond -> subscribe to Oracle's endpoint
- User connect to server websocket with params:
    + {
    +  signature: {{sign endpoint's name with user's address}},
    + endpoint: {{endpoint name}},
    + address: {{user's address}}
    +  }
- After successful authenticated, user will be able to connect with websocket until the block remaining subscriptions is 0
- User listen to channel `signalData` from Oracle and receive data


### SETUP
- ``` yarn ```
##### Run Server:
- Create `priv_config.ts` based on `config.ts` template with oracle's information
- In `src/server.ts` modify method `getData` to get custom data of your own. This data will be broadcasted to users
- ``` yarn server```

##### User Connecting to server:
- In `src/user.ts` modify signature, address and endpoint
- ```yarn user```
