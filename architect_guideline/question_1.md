# QUESTION 1 Docker Container

### guideline by pijar

1. Introduction.md (https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/01-docker-terraform/docker-sql/01-introduction.md)
2. Try to understand concept of docker container
3. Open docker desktop
4. Make new folder -> go to that folder -> Open terminal in that folder

If we want bash, we need to overwrite `entrypoint`:

```bash
docker run -it \
    --rm \
    --entrypoint=bash \
    python:3.9.16-slim
```
5. Try to execute that command, but modify with task in question 1, it should be python:3.13
6. After that pulling process, it become like this in terminal : root@xxxxx:/# (you should see something like this, it means you successfully go inside docker with bash)
7. try to get python version and pip version
8. Question 1 done
