# node-toptbsdk


为了更好的使用ES6/7开发，对淘宝官方Node.js版的topsdk进行修改，使用方法和官方一致，不同的是返回Promise结果。淘宝官方的sdk中使用[urllib](https://github.com/node-modules/urllib)作为Http工具，这里修改为使用[request](https://github.com/request/request)。

## 安装
```
npm install node-toptbsdk --save
```

## 使用方法
### Promise
```javascript
const TopClient = require('node-toptbsdk');

const client = new TopClient({
  appkey: 'appkey',
  appsecret: 'appsecret',
});

await client.execute('alibaba.aliqin.fc.sms.num.send', {
  extend: '123456',
  sms_type: 'normal',
  sms_free_sign_name: '阿里大于',
  rec_num: '12345678912',
  sms_template_code: 'SMS_8985285',
  sms_param: {
    customer: 'Ray'
  }
})

```
### Async / await
```javascript
const TopClient = require('node-toptbsdk');

async function sendSms() {
  const client = new TopClient({
    appkey: 'appkey',
    appsecret: 'appsecret',
    REST_URL: 'https://eco.taobao.com/router/rest'
  });

  let result;
  try {
    result = await client.execute('alibaba.aliqin.fc.sms.num.send', {
      extend: '123456',
      sms_type: 'normal',
      sms_free_sign_name: '阿里大于',
      rec_num: '12345678912',
      sms_template_code: 'SMS_8985285',
      sms_param: {
        customer: 'Ray'
      }
    });
  } catch (err) {
    console.error(err);
  }

  console.log(result);
}
```
### 注意
默认是POST，如果使用GET等，execute的第三个参数请输入，如：
```javascript
...
client.execute('alibaba.aliqin.fc.sms.num.send', {
  extend: '123456',
  ...
}, 'GET')
...
```

## License
MIT
