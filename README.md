#Nasim Bot Platform
Are you a JS Developer? By this platform, you can develop [Nasim](https://nasim.elenoon.ir/) bots easily.
##Requirements
You should have installed [node](https://nodejs.org) and [npm](https://www.npmjs.com) on your system.
##Create a bot like a boss!
###Get a bot token from Nasim BotFather.
You can find Nasim BotFather by this id: <b>@bot-father</b>
###Prepare your environment
```bash
$ mkdir mybot
$ cd mybot
$ npm init
```
### Install the platform
```bash
$ npm install nasim-bot
```
### Require it
Create an index.js file and inside it:
```javascript
const Platform = require("nasim-bot");
```
### Nasim bot platform is Object-Oriented!
Enjoy the provided classes. Here you are:
```javascript
const NasimBot = Platform.NasimBot;
const TextMessage = Platform.TextMessage;
const FileMessage = Platform.FileMessage;
const File = Platform.File;
const BotStatus = Platform.BotStatus;
const User = Platform.User;
const Conversation = Platform.Conversation;
```
### Instantiate your bot
```javascript
let bot = new NasimBot("Your Token");
```
Now your index.js should look something like this:
```javascript
const Platform = require("nasim-bot");

const NasimBot = Platform.NasimBot;
const TextMessage = Platform.TextMessage;
const FileMessage = Platform.FileMessage;
const File = Platform.File;
const BotStatus = Platform.BotStatus;
const User = Platform.User;
const Conversation = Platform.Conversation;

let bot = new NasimBot("Your Token");
```
### Next
Now your code environment is ready. You can ```hear``` for an individual message. Make ```conversation```s and talk to your users, and so on and so forth...  
Discover more and more from [samples](#samples).
## Samples
### Hears sample
You can hear for a message with a particular content and respond to it.  
The ```hears``` method takes two arguments:
* A string array of expected texts in receiving messages to match. (Or alternatively a [Sensitive](#sensitive) object)
* A callback function in type of ```(message, responder) => {}``` that takes two arguments:
    * **message**: The matched received [Message][#message] object.
    * **responder**: See [Responder](#responder).
```js
"use strict";

const Platform = require("nasim-bot");
const NasimBot = Platform.NasimBot;
const TextMessage = Platform.TextMessage;

let bot = new NasimBot("Your Token");

bot.hears(['whats your name', 'name', 'name?'], (message, responser) => {
    responser.reply("My name is samplebot!");
});
```
### Conversation sample
Not all activities are limited to just ```hear```ing for a message and respond to it; As sometimes there is a need to make a __statefull__ conversation. Using this platform, you can make conversations with users as follows.  
1. Create a [Conversation](#conversation) object.  
2. Determine what makes the conversation to trigger and get started.  
3. Determine what states the conversation would take, and the behavior of each state.  
4. Set the created conversation to your ```bot```.
```js
"use strict";

const Platform = require("nasim-bot");
const NasimBot = Platform.NasimBot;
const TextMessage = Platform.TextMessage;
const BotStatus = Platform.BotStatus;
const User = Platform.User;
const Conversation = Platform.Conversation;

let bot = new NasimBot("Your Token");

let conv = new Conversation();

let tracer = conv.startsWith(["lets talk"]);
tracer.then((message, session, responser) => {
    //STATE 0
    //The first state definitely matches with the "starts with" sensitive. In this case: "lets talk"
    responser.reply("OK. Whats your name?");
    //Go to the next state
    session.next();
}).then((message, session, responser) => {
    //STATE 1
    if (message.text.length < 7) {
        responser.reply("Nice name. I like " + message.text);
        //Ok. go to the next state...
        session.next();
    } else {
        responser.reply("What a long name! Give me a shorter name! :|");
        // Don't call session.next() to remain in the current state.
    }
});

bot.setConversation(conv);
```
### Send sample
```js
"use strict";

const Platform = require("nasim-bot");
const NasimBot = Platform.NasimBot;
const TextMessage = Platform.TextMessage;
const User = Platform.User;
const Conversation = Platform.Conversation;

let bot = new NasimBot("Your Token");
let msg = new TextMessage("Hi, I'm connected :)", new User(123 /*user id*/, "321" /*user access hash*/));
bot.send(msg);
```
## API classes and models
### Sensitive
### Message
### Responder
### Conversation
