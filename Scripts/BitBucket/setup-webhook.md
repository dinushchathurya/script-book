### Setup BitBucket Webhook 

```
https://<jenkins-server-public-ip>:8080/bitbucket-scmsource-hook/notify/
```

#### If you are using local Jenkins server, then use the following URL

If you are using local Jenkins server, then you need to use a tool like ngrok to expose your local Jenkins server to the internet. 

```
https://<ngrok-public-url>/bitbucket-scmsource-hook/notify/
```