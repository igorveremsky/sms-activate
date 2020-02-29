# SMS Activate API
![npm](https://img.shields.io/npm/v/sms-activate)
![npm](https://img.shields.io/npm/dy/sms-activate)
[![CodeFactor](https://www.codefactor.io/repository/github/jsopn/sms-activate/badge)](https://www.codefactor.io/repository/github/jsopn/sms-activate)

## Installation
NPM:
`npm install sms-activate`

Yarn:
`yarn add sms-activate`

## Usage

```js
const SMSActivate = require('sms-activate')
const sms = new SMSActivate('token')

const balance = await sms.getBalance()

if (balance > 0) {
  const { id, number } = await sms.getNumber('ya')
  await sms.setStatus(id, 1)

  const waitForCode = setInterval(async () => {
    const code = await sms.getCode(id)
    if (code) {
      clearInterval(waitForCode)
      await sms.setStatus(id, 6)

      console.log(code)
    }
  }, 1000)
} else {
  console.log('You don\'t have enough money')
}

```