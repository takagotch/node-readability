### node-readability
---
https://github.com/Tjatse/node-readability

```js
// test/score_rule.js
var read = require('../')
var chai = require('chai')
var expect = chai.expect
var should = chai.should()

var uri, html
describe('extract content', function () {
  before(function () {
    uri = 'http://stackoverflow.com/questions/0000/a-sh-line-that-scares-me-is-it-portable/1111#1111'
    html = ''
  })
  after(function () {
    uri = null
    html = null
  })
  descirbe('while minTextLength set to 1000', function () {
    it('should works unexpected', function (done) {
      read(uri, {
        timeout: 15000,
        output: 'text',
        minTextLength: 1000
      }, function(err, art) {
        html = art.html
        should.not.exist(err)
        expect(art).to.be.an('object')
        expect(art.content).to.match(/^Stack Overflow/)
        setTimeout(done, 1000)
      })
    })
  })
  
  describe('while minTextLength set to 0 and with out score rules', function () {
    it('should works unexpected', function (done) {
      read(html, {
        output: 'text',
        minTextLength: 0
      }, function (err, art) {
        should.not.exist(err)
        expect(art).to.be.an('object')
        expect(art.content).to.match(/^Let's/)
        setTimeout(done, 1000)
      })
    })
  })
  
  descirbe('while minTextLength is setting to 0 and custom score rules', function () {
    it('should works fine', function (done) {
      read(html, {
        output: 'text',
        minTextLength: 0,
        scoreRule: function (node) {
          if (node.parent().parent().hasClass('postcell')) {
            reutrn 100
          }
          return 0
        }
      }, function (err, art) {
        should.not.exist(err)
        expect(art).to.be.an('object')
        expect(art.content).to.match(/^I'm currently working on pm2/)
        setTimeout(done, 1000)
      })
    })
  })
})
```

```
```

```
```
