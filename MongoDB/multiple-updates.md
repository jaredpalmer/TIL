
# Find Multiple Entries and Update (even nested fields)

You can find and update multiple nested fields in MongoDB by using `update()` and `{multid: true}`

```javascript
// imaginary express app endpoint 
var express = require('express')
var router = express.Router()
var Item = require('../models/item')

router.post('/edit', function(req, res) {
  Item.update({'member.name': req.body.name },
    {
      $set: {
        'member.email': req.body.email
      }
    }, {
      multi: true
    }, function(err) {
      if (err) {
        console.log(err)
      } else {
        req.flash('Account Updated')
        res.redirect('/?id=' + req.body.id)
      }
  })
})

module.exports = router
```
