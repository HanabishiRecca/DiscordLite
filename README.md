# Discord Slim
### V2 IS UNDER DEVELOPMENT!  
Contains breaking changes and incompatible with V1.  
Dev version is unstable and can have bugs!  
API is unfinished and may be changed with further updates.  

### V2 main features
- Typed actions API instead of manual requests.  
- Typed events API instead of manual packet handling.  
- Actions is now independent from the client.  

### Support & suggestions server
https://discord.gg/drsXkP8R4h  

## Before you start
### **Node.js** 12+ is required!
Make sure you have some understaning of **[Discord API](https://discordapp.com/developers/docs)**.  

## Installation
### Note: NPM version may be out-of-date and not contain latest repo commits.
```
npm i discord-slim@dev
```
## Usage example

```js
const
    Discord = require('discord-slim'),
    Actions = Discord.Actions,
    Events = Discord.Helpers.Events,
    Intents = Discord.Helpers.Intents,
    client = new Discord.Client(),
    authorization = new Discord.Authorization('token'),
    requestOptions = { authorization };

client.on('connect', () => console.log('Connection established.'));
client.on('disconnect', (code) => console.error(`Disconnect. (${code})`));
client.on('warn', console.warn);
client.on('error', console.error);
client.on('fatal', (e) => { console.error(e); process.exit(1); });

client.events.on(Events.MESSAGE_CREATE, (message) => {
    if(message.author.id == client.user.id) return;
    if(message.content.toLowerCase().indexOf('hello bot') < 0) return;
    Actions.Message.Create(message.channel_id, {
        content: `Hi, <@${message.author.id}>!`,
        message_reference: {
            channel_id: message.channel_id,
            message_id: message.id,
        },
    }, requestOptions);
});

client.Connect(authorization, Intents.GUILDS | Intents.GUILD_MESSAGES);
```

## Build from source
Install `typescript` package from `npm` and run `tsc`.  
