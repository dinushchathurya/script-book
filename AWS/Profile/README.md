### Configure Profile

```
aws configure

aws configure --profile <profile-name>
```

### Set AWS Profile

```
Linux:
export AWS_PROFILE=<profile-name>

Windows:
setx AWS_PROFILE <profile-name>
```

### Get all user profiles

```
Windows:
aws configure list-profiles
```

### Get Current AWS Profile

```
aws configure list
```

### Get details of IAM or Role used to called the operation

```
aws sts get-caller-identity
```