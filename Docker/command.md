### Remove multiple images related to particular image name

```
docker rmi --force $(docker images -q "image_name" | uniq')
```