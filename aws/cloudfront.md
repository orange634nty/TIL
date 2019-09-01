Cloud Front
---

公式：https://aws.amazon.com/jp/cloudfront/

要はCDN  
Lambda@Edge とかも使える

## CloudFront でおま国

AWS の CloudFront を使って地域制限（国単位）をかけられる

- [コンテンツの地理的ディストリビューションの制限](https://docs.aws.amazon.com/ja_jp/AmazonCloudFront/latest/DeveloperGuide/georestrictions.html)
- [AWS Cloudfrontの地域制限機能を使って特定地域からのアクセスを遮断する](https://beyondjapan.com/blog/2016/09/aws-cloudfront-specificarea-blocking/)

CloudFront の Distribution Settings > Restrictions > Geo Restriction から設定可能
