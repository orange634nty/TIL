serverless
---

## serverless frame work

just read this page, or you only need to read official doc.
https://serverless.com/framework/docs/providers/aws/guide/serverless.yml/

## important point when you deploy serverless to production

https://qiita.com/keitakn/items/22cbc3e00acb79560b87

- setup cloudwatch to export lambda execute logs
- measures to lambda cold sleep (acutually we dont need this)
- set cloud watch logRetentionInDays (default is infinity)
- use `serverless-prune-plugin` to cut code volume capacity.
   lambda save all code which you upload, even it is very old by default settings.
- set method to monitor serverless system (this time we dont need this)

## notify aws estimate every day

https://qiita.com/ishikun/items/90b766e5555421970e9f

## start stop ec2

https://dev.classmethod.jp/cloud/aws/simple-auto-start-stop-for-ec2/

## separate slack notify lambda

https://confl.arms.dmm.com/pages/viewpage.action?pageId=68491147
