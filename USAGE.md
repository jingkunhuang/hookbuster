# Quick Start Guide

## After Installation

Once hookbuster is installed, you can use it in two modes:

---

## 🎮 Interactive Mode (Demo Mode)

Simply run the command without any environment variables:

```bash
hookbuster
```

Or if installed locally:

```bash
npx hookbuster
```

You'll see an interactive CLI that prompts you for:

1. **Access Token**: Your Webex Teams bot or user access token
2. **Target Host**: Where to forward events (default: localhost)
3. **Port**: The port number where your application is listening
4. **Resource**: Which Webex resources to monitor (rooms, messages, memberships, etc.)
5. **Events**: Which events to forward for the selected resource

### Example Interactive Session:

```
  ,----------------------------------------------------------.
  |                                                          |
  |    _   _             _    _               _              |
  |   | | | | ___   ___ | | _| |__  _   _ ___| |_ ___ _ __   |
  |   | |_| |/ _ \ / _ \| |/ / '_ \| | | / __| __/ _ \ '__|  |
  |   |  _  | (_) | (_) |   <| |_) | |_| \__ \ ||  __/ |     |
  |   |_| |_|\___/ \___/|_|\_\_.__/ \__,_|___/\__\___|_|     |
  |                                                          |
  |                                                          |
  `----------------------------------------------------------'

? Enter your access token > YourWebexAccessToken123...
✓ Token authenticated as Bot Name
? Enter a target hostname or IP address > localhost
? Enter a port you will forward messages to > 5000
? Select resource [ a - all, r - rooms, m - messages, mm - memberships, aa - attachmentActions ] > a

INFO: Listening for events from the rooms resource
INFO: Registered handler to forward rooms:created events
INFO: Registered handler to forward rooms:updated events
INFO: Listening for events from the messages resource
INFO: Registered handler to forward messages:created events
INFO: Registered handler to forward messages:deleted events
...
```

---

## 🚀 Deployment Mode (Automated)

Set environment variables for automated startup:

```bash
export TOKEN="your_webex_access_token"
export PORT="5000"
export TARGET="localhost"  # Optional, defaults to localhost

hookbuster
```

Or inline:

```bash
TOKEN="your_token" PORT="5000" hookbuster
```

In this mode, hookbuster automatically:
- Authenticates with your token
- Registers for ALL event types (firehose mode)
- Forwards all events to the specified TARGET:PORT

---

## 📋 Common Use Cases

### 1. Local Development with a Test Server

**Terminal 1 - Start your test server:**
```bash
# Simple test server that logs received events
node -e "
const http = require('http');
http.createServer((req, res) => {
  if (req.method === 'POST') {
    let body = '';
    req.on('data', chunk => body += chunk);
    req.on('end', () => {
      console.log('Event received:', JSON.parse(body));
      res.writeHead(200);
      res.end('OK');
    });
  }
}).listen(5000, () => console.log('Listening on port 5000'));
"
```

**Terminal 2 - Start hookbuster:**
```bash
TOKEN="your_token" PORT="5000" hookbuster
```

### 2. Testing with Javabot

If you're testing with [Javabot](https://github.com/WebexSamples/javabot):

**Terminal 1 - Start Javabot:**
```bash
cd javabot
# Configure javabot to listen on port 5000
java -jar javabot.jar
```

**Terminal 2 - Start hookbuster:**
```bash
TOKEN="your_bot_token" PORT="5000" hookbuster
```

Now message your bot in Webex Teams and it should respond!

### 3. Behind a Firewall

Perfect for when your application can't receive webhooks:

```bash
# Your app listens on localhost:8080
# Hookbuster forwards Webex events to it
TOKEN="your_token" PORT="8080" hookbuster
```

---

## 🔑 Getting Your Access Token

### For Bots:
1. Go to [Webex Developer Portal](https://developer.webex.com/my-apps)
2. Create a new Bot
3. Copy the Bot Access Token

### For Personal Use:
1. Go to [Webex Developer Portal](https://developer.webex.com/docs/api/getting-started)
2. Log in
3. Copy your personal access token (expires in 12 hours)

---

## 🎯 Resource Options

When running interactively, you can choose which resources to monitor:

| Option | Alias | Description | Events Available |
|--------|-------|-------------|------------------|
| **All** | `a` | All resources | All events |
| **Rooms** | `r` | Webex spaces | created, updated |
| **Messages** | `m` | Chat messages | created, deleted |
| **Memberships** | `mm` | Room members | created, updated, deleted |
| **Attachment Actions** | `aa` | Card interactions | created |

---

## 📊 What Happens When Events Arrive?

When a Webex event occurs, hookbuster:

1. Receives the event via WebSocket
2. Logs it to the console
3. Forwards it as an HTTP POST request to your target

### Event Format:
```json
{
  "id": "event-unique-id",
  "resource": "messages",
  "event": "created",
  "data": {
    "id": "message-id",
    "roomId": "room-id",
    "personId": "person-id",
    "personEmail": "user@example.com",
    "text": "Hello World",
    "created": "2024-01-01T12:00:00.000Z"
  }
}
```

Your application receives this as a standard HTTP POST request.

---

## 🛑 Stopping Hookbuster

Press `Ctrl+C` to gracefully shutdown. Hookbuster will:
1. Stop all active listeners
2. Deregister event handlers
3. Close WebSocket connections
4. Exit cleanly

---

## 🔍 Troubleshooting

### "Token not authenticated"
- Verify your access token is valid
- Check if the token has expired (personal tokens expire in 12 hours)
- Ensure no extra spaces or characters in the token

### "Connection refused" when forwarding
- Verify your target application is running
- Check the port number is correct
- Ensure no firewall is blocking the port

### No events being received
- Verify the bot is a member of the space (for room/membership events)
- Check that you're triggering the right event type
- Ensure your token has appropriate permissions

---

## 📖 Full Documentation

For more details, see:
- [README.md](README.md) - Complete project documentation
- [INSTALL.md](INSTALL.md) - Installation options and troubleshooting

---

## 💡 Pro Tips

1. **Use deployment mode for production** - Set environment variables instead of interactive prompts
2. **Start with "all" events** - See everything that's happening, then narrow down
3. **Log received events** - Always log what your target app receives for debugging
4. **Keep it running** - Use process managers like PM2 or systemd for production
5. **One token per app** - Use the same token for hookbuster and your app for consistency

---

Enjoy using hookbuster! 🚀
