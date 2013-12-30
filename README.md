# koa-session-mongoose

Mongoose storage layer for [Koa session middleware](https://github.com/hiddentao/koa-session-store). This can be used instead of [koa-session-mongo](https://github.com/hiddentao/koa-session-mongo), for a more direct integration with an existing [Mongoose](http://mongoosejs.com) connection.

## Installation
   
```
npm install koa-session-mongoose
```

## Usage

```
var session = require('koa-session-store');
var mongoose = require('mongoose');
var mongooseStore = require('koa-session-mongoose');
var koa = require('koa');

mongoose.connect('mongodb://127.0.0.1/koa_app');

var app = koa();

app.keys = ['some secret key'];  // needed for cookie-signing

app.use(session({
  store: mongooseStore.create()
}));

app.use(function *(){
  var n = this.session.views || 0;
  this.session.views = ++n;
  this.body = n + ' views';
});

app.listen(3000);
console.log('listening on port 3000');
```

You can specify collection name and expiration time (in seconds):

```
app.use(session({
  store: mongooseStore.create({
    collection: 'koaSessions',
    expires: 60 * 60 * 7	// 1 week
  })
}));

```

## Other Relevant Modules

* [koa-session-store](https://github.com/hiddentao/koa-session-store)  
* [koa-session-mongo](https://github.com/hiddentao/koa-session-mongo)

## License

The MIT License (MIT)

Copyright (c) 2013 Michael J. Bondra < [mjbondra@gmail.com](mailto:mjbondra@gmail.com) >

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.