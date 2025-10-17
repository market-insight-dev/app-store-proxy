# iTunes API Proxy Server

A simple Node.js proxy server to bypass iTunes Search API blocking from Cloudflare Workers.

## Local Development

### Requirements
- Node.js 18+ 
- npm or yarn

### Installation and Running

```bash
cd proxy
npm install
npm start
```

Server will start at `http://localhost:3000`

### Testing

```bash
# Health check
curl http://localhost:3000/health

# Proxy request to iTunes API
curl "http://localhost:3000/proxy?url=https://itunes.apple.com/search?term=spotify&country=us&entity=software&limit=5"
```

---

## Security

Production recommendations:

1. **Rate limiting** - add `express-rate-limit`
2. **API keys** - protect endpoint from public access
3. **HTTPS** - use SSL certificate (Let's Encrypt)
4. **Monitoring** - set up UptimeRobot or similar service

### Example of adding rate limiting:

```bash
npm install express-rate-limit
```

```javascript
// Add to server.js:
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 1 * 60 * 1000, // 1 minute
  max: 100, // 100 requests per IP
});

app.use('/proxy', limiter);
```

---

## Support

If you encounter issues:
1. Check server logs
2. Check health endpoint: `curl https://your-proxy/health`
3. Make sure port 3000 is open (or PORT env variable is set)

