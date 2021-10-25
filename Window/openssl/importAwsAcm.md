# aws acm 용 추출


### key.pem 만드는 법
openssl pkcs12 -in website.xyz.com.pfx -nocerts -out privatekey.pem

비번 입력하고, PEM pass도 동일하게 작성

### key.pem 비번 해체
openssl rsa -in privatekey.pem -out withoutpw-privatekey.pem

### cert.pem 만드는 법
openssl pkcs12 -in website.xyz.com.pfx -clcerts -nokeys -out cert-file.pem

### chain.pem 만드는 법
openssl pkcs12 -in website.xyz.com.pfx -cacerts -nokeys -chain -out ca-chain.pem


### [AWS 공식 가이드 문서]

https://aws.amazon.com/ko/blogs/security/how-to-import-pfx-formatted-certificates-into-aws-certificate-manager-using-openssl/
