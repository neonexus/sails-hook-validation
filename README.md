sails-hook-validation
=====================

[![Build Status](https://travis-ci.org/lykmapipo/sails-hook-validation.svg?branch=master)](https://travis-ci.org/lykmapipo/sails-hook-validation)

[![Tips](https://img.shields.io/gratipay/lykmapipo.svg)](https://gratipay.com/lykmapipo/)

[![Support via Gratipay](https://cdn.rawgit.com/gratipay/gratipay-badge/2.3.0/dist/gratipay.svg)](https://gratipay.com/lykmapipo/)

Custom validation error messages for sails model.

*Note: This requires Sails v0.11.0+.  If v0.11.0+ isn't published to NPM yet, you'll need to install it via Github.*

## Installation
```sh
$ npm install --save sails-hook-validation
```

## Usage
- Add `validationMessages` static property in your sails model
```js
//this is example
module.exports = {
    attributes: {
        username: {
            type: 'string',
            required: true
        },
        email: {
            type: 'email',
            required: true
        }
    },
    //model validation messages definitions
    validationMessages: { //hand for i18n & l10n
        email: {
            required: 'Email is required',
            email: 'Provide valid email address',
            unique: 'Email address is already taken'
        },
        username: {
            required: 'Username is required'
        }
    }
};
```
- Now you can call your `Model.create` and `Model.update` and other static model method that invoke `Model.validate()`. If there is any validation error `sails-hook-validation` will put your custom errors message in `error.Errors` in the error object returned by those methods.
```js
//anywhere in your codes if
//you invoke
 User
    .create({}, function(error, user) {

        expect(error.Errors.email).to.exist;

        expect(error.Errors.email[0].message)
            .to.equal(User.validationMessages.email.email);

        expect(error.Errors.email[1].message)
            .to.equal(User.validationMessages.email.required);


        expect(error.Errors.username).to.exist;
        expect(error.Errors.username[0].message)
            .to.equal(User.validationMessages.username.required);

        done();
    });
```

*Note: `sails-hook-validation` work by patch model static `validate()`, to have custom error messages at model instance level consider using [sails-model-new](https://github.com/lykmapipo/sails-model-new)*

## Testing

* Clone this repository

* Install all development dependencies

```sh
$ npm install
```
* Then run test

```sh
$ npm test
```

## Contribute

Fork this repo and push in your ideas. 
Do not forget to add a bit of test(s) of what value you adding.

## Licence

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE. 