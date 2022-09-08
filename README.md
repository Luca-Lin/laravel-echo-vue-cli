# laravel-echo and pusher-js

Use `laravel-echo` and `pusher-js` front end package to connect self `laravel-websocket` server

## Environment to setting PUSHER_KEY and laravel websocket server host

vue-cli project can read `VUE_APP` prefix env

```
cp .env .env.local
```

## Connect setting

- setting on your want to connect page
```javascript
import Echo from 'laravel-echo';
import Pusher from 'pusher-js';
window.Pusher = Pusher;
window.Echo = new Echo({
    broadcaster: 'pusher',
    key: process.env.VUE_APP_WEBSOCKETS_KEY,
    wsHost: process.env.VUE_APP_WEBSOCKETS__SERVER,
    wsPort: 6001,
    forceTLS: false,
    disableStats: true,
    enabledTransports: ['ws']
});
```
- console.log my laravel event
```javascript
export default {
  name: 'App',
  ...
  
  mounted() {
    window.Echo.channel('channel')
      .listen('LineBotMessage', (e) => {
        console.log(e);
      });
  }
}
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
