# discord-r9k

Framework for R9K and other bots.

## Documentation

### `addMessageTrigger(trigger, callback)`

#### `trigger`

A The trigger can be one of the following types:

- `String` The callback will be triggered if the message matches the String exactly
- `RegExp` If the message matches the RegExp, the callback will be triggered, the callback argument will include the list of matches returned by [`String.match()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match)
- `Array` All array elements are treated as separate triggers

#### `callback`

A function that will be called if the trigger is matched.

The callback has one argument, an object containing the following fields:

- `user` the user that triggered this event
- `userId` that users, id
- `channelId` the id of the channel
- `message` the message that triggered this event
- `matches` any matches if the trigger was a regular expression
- `event` the full [event](https://izy521.gitbooks.io/discord-io/content/Events.html) from discord.io that triggered this event
- `bot` this discord.io [client](https://izy521.gitbooks.io/discord-io/content/Methods/Client.html) object, can be used to respond asynchronously

If the callback returns a String, it will be sent as a message to the channel this event was triggered from. If you want to respond to an event asynchronously, you can use the `bot` object to send a message.

```javascript
addMessageTrigger('!someTrigger', (opts) => {
  returnsAPromise().then(result => opts.bot.sendMessage({
    message: result,
    to: opts.channelId,
  }));
});
```

## Further reading

See the [Discord developer docs](https://discordapp.com/developers/), or the docs for [discord.io](https://www.npmjs.com/package/discord.io), the library that powers this bot.
