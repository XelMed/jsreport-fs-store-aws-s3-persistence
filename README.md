# jsreport-fs-store-aws-s3-persistence-all-options
[![NPM Version](http://img.shields.io/npm/v/jsreport-fs-store-aws-s3-persistence.svg?style=flat-square)](https://npmjs.com/package/jsreport-fs-store-aws-s3-persistence)

**Make jsreport [fs store](https://github.com/jsreport/jsreport-fs-store) persisting entities into AWS S3.**


## Installation

> npm install jsreport-fs-store
> npm install jsreport-fs-store-aws-s3-persistence-all-options

Create an IAM user with permissions to S3 and SQS and copy the access key and secret access key.
Create a bucket and copy its name. Then alter the jsreport configuration:
```js
"store": {
  "provider": "fs"
},
"extensions": {
  "fs-store": {
    "persistence": {
      "provider": "aws-s3"
    }
  },
  "fs-store-aws-s3-persistence": {
    "accessKeyId": "...",
    "secretAccessKey": "..."
    "bucket": "..."
    // the rest is otional
    "lock": {
      "queueName": "jsreport-lock.fifo",
      "region": "us-east-1",
      "enabled": true,
      "attributes": {}
    },
    options:{ //any options for S3
    }
  }
}
```

This persistence implementation also guarantees consistency for parallel access from multiple instances. This is assured using locking mechanism enabling only single write at once. The locking is implemented trough AWS SQS. The queue is automatically created during the instance startup with attributes specified in the configuration `lock`. You can disable it by setting `false` to `lock.enabled`.
