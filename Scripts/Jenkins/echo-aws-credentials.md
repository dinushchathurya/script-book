### Echo AWS Credentials

```
node {
    def creds

    stage('Echo AWS Credentials') {      
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID' credentialsId: '<your-credential-id>', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            creds = "\nUser: ${AWS_ACCESS_KEY_ID}\nPassword: ${AWS_SECRET_ACCESS_KEY}\n"
        }
        println creds
    }
}
```