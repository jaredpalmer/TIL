# Tracking Pixel 

TIL you can write a tracking pixel with ~ 14 lines of Node.js and Express

```javascript
import http from 'http'
import express from 'express'

const app = express()

const trackImg = Buffer.from('R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7', 'base64');

app.get('/api/track/:campaign/:list/:id', (req, res) => {
  res.writeHead(200, {
    'Content-Type': 'image/gif',
    'Content-Length': trackImg.length
  })

  const { campaign, list, id } = req.params 
  const { things } = req.query
  
  // db.save() 
  
  res.end(trackImg)
})
...
http.createServer(app).listen(3000, => console.log('listening on port 3000'))
```
Wherever you want to track an open event, just drop in an `img` tag with the url, params and/or query like so:

```html
<img src="http://example.com/api/track/1234/12/1?things=xxx" height="1" width="1">
```
