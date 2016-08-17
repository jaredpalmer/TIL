# Creating Commnad Line Tools with Node

### Make a new project
```bash
mdkir my-cli && cd my-cli
npm init -y
```

### Make your script.
Some things to keep in mind:
  - Use `path.join(__dirname, '...')` to reference things inside of your project within your project.
  - Use `process.cwd()` to reference things within the end-users' project

```javascript
#! /usr/bin/env node
// my-cli.js

var electron = require('electron')
var spawn = require('cross-spawn')
var path = require('path')
var chalk = require('chalk')

// This script let's you bundle any project into an Electron app 
// Note: main.js is not shown, but it is identical to electron-quick-starts's main.js

process.stdout.write('\x1bc') // clear console
console.log()
console.log()
console.log(chalk.cyan('Compiling...'))  // pretty output

var child = spawn(electron, [path.join(__dirname, './main.js')] , { stdio: 'inherit' })


// Handle error
child.on('close', function (code) {
  if (code !== 0) {
     console.error('Could not bundle prototype.')
     console.log()
     console.log()
     return
  }
})

```


### Update `package.json`
To make a script available as an executable, you need to specify it in `bin` like so:
```json
{
  "name": "<my-cli>",
  "version": "1.0.1",
  "description": "Quickly run Framer prototypes within Electron.",
  "bin": {
    "<command-to-run-my-cli>": "<my-cli.js>"
  }
}
```

### Local Development
Inside you CLI project's root directory, run `npm link`. This will install your executable. Any local edits within your project will be effective immediately. However,
if you make changes to the name or location of `my-cli.js`, you may need to manually remove it from your local `bin`. The error will tell you the path where it is installed.
Run `cd /path/to/bin ** rm -rf <command-to-run-your-cli>`. You may need to run `npm link` once again.


### Publish to NPM 
Update your version number and run:
```bash
npm publish
```


**Awesome CLI node packages**
  - [cross-spawn](https://github.com/IndigoUnited/node-cross-spawn) - Cross-platform `spawn` and `spawnSync`
  - [fs-extra](https://github.com/jprichardson/node-fs-extra) - Better file-system methods
  - [ora](https://github.com/sindresorhus/ora) - Cool terminal spinner
  - [commander](https://github.com/tj/commander.js) - CLI interface helper
  - [execa](https://github.com/sindresorhus/execa) - Better child process
  - [update-notifier](https://github.com/yeoman/update-notifier) - Update notifications for your CLI app
  - [opn](https://github.com/sindresorhus/opn) - Opens stuff like websites, files, executables. Cross-platform.
  - [chalk](https://github.com/chalk/chalk) - Pretty terminal console colors
  - [columnify](https://github.com/timoxley/columnify) - Create text-based columns suitable for console output. (like homebrew) 

