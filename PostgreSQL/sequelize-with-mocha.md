# Setup Mocha on a Sequelize ORM project

 - Create a local test DB the same as your `development` one but with `_test` appended to the name.
 - Make sure your Express app is wrapped in a function that accepts your Sequelize models.

```javascript
// app.js
import express from 'express'
import cookieParser from 'cookie-parser'
import bodyParser from 'body-parser'

export default function app(models) {
  const app = express()
  app.use(bodyParser.json())
  app.use(bodyParser.urlencoded({ extended: false }))
  app.use(cookieParser())

  app.use(logger.requestLogger((req, res) => {
    (res)
    return {
      method: req.method,
      path: req.path,
      ...req.body
    }
  }))
  
  ...
  
  app.get('/v1/users', (req, res) => {
    models.User.findAll({limit: 10}).then(users => {
      if (users) res.status(200).json(users)
    }).catch(e => {
      res.status(500).json({ error: e, message: e.message })
    })
  })
  ...
  
  return app
}

```
- Create a seed function 

```javascript
// test/seed.js

export default function seed(models) {
    return models.User.create({
      firstName: 'Jared',
      lastName: 'Palmer',
      email: 'jared@blah.com',
      Chapter: {
        name: 'New York',
        location: '10016',
      },
      Company: {
        name: 'Acme',
        email: 'info@acme.com',
      }
    }, {
      include: [models.Chapter, models.Company] // super cool shortcut to make related rows in one step
    })
  .catch(e => console.log(e))
}
```
- Leverage Sequelize's Sync to reset the DB for each test.
```javascript
// test/routes_spec.js

process.env.NODE_ENV = 'test'

import chai, { expect } from 'chai'
import chaiHttp from 'chai-http'

import app from '../app'
import models from '../db/models/index'
import seed from './seed'
import logger from 'logfmt'

chai.use(chaiHttp)

const app = api(models)

describe('API Routes', () => {

  // start with a fresh DB 
  beforeEach(done => {
    models.sequelize.sync({ force: true, match: /_test$/, logging: false })
    .then(() => {
      return seed(models)
    }).then(() => {
      done()
    })

  })
  
  describe('GET /v1/users', (done) => {
    it('should get a list of users', (done) => {
      chai.request(app)
      .get('/v1/users')
      .end((err, res) => {
        expect(res.status).to.equal(200)
        expect(res).to.be.json
        expect(res.body).to.be.a('array')
        done()
      })
    })
  })
  
})

```
 - if you have not done so already, you'll need another script actually run your express app like so

```javascript
 // bin/www
 
import http from 'http'
import app from '../app'
import models from '../db/models/index'

const api = app(models)

http.createServer(api).listen(3000, () => {
  console.log('starting server on port 3000')
})

```
- add scripts to your package.json (assumes you have babel-cli, babel-core, etc. installed)

```json
...
"scripts": {
    "test": "mocha --compilers js:babel-register",
    "test:watch": "npm test -- --watch",
    "start": "babel-node bin/www"
  },
...
```
Go ahead and TDD
