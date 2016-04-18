# FaceBot
FaceBot is a Facebook Messenger Bot

# Example
```javascript
import { Router } from 'express';
import http from 'http';
import express from 'express';
import FaceBot from 'facebot';

let app = express();
let api = Router();

let bot = new FaceBot({
    token: '%FACEBOOK_PAGE_ACCESS_TOKEN%',
    verify: '%FACEBOOK_WEBHOOK_TOKEN%'
});

bot.on('message', (payload, reply) => {
    let text = payload.message.text

    reply('text', text, (err) => {
      if (err) throw err
    })
});

app.server = http.createServer(app);
app.use('/webhook', bot.middleware());
app.server.listen(8080);
```
## Initialize
```javascript
let bot = new FaceBot(options)
```
options – Object
- `token` – Facebook Page access token
- `verify` – Facebook Webhook verification token. 
- `pageId` – Facebook Page ID. To set a welcome message.

## Events
#### Messages
```javascript
bot.on('message', (payload, reply) => {
  let text = payload.message.text;
  console.log(text);
});
```
#### Subscribe to postback events
```javascript
bot.on('postback', (payload, reply) => {
  if (payload.postback === 'start') {
    console.log('Hello,  my friend!');
  }
});
```
####  with specific payload
```javascript
// Specify a payload followed by a colon
bot.on('postback:start', (payload, reply) => {
  reply('text', 'Let\'s start our conversation.', (err) => {
      if (err) throw err
    })
});
```
#### Delivery
```javascript
bot.on('delivery', (payload, reply) => {
  console.log('Message delivered');
});
```


