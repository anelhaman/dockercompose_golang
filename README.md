## Invention over Configuration

```
.
├── docker-compose.yml
└── golang
    ├── app.go
    └── dockerfile
```

1 directory, 4 files


## dockerfile

```
FROM golang:1.8
WORKDIR /go/src/app
COPY . .

RUN go get github.com/gin-gonic/gin
RUN go install github.com/gin-gonic/gin
```

## app.go
```
package main

import "github.com/gin-gonic/gin"

func main() {
	r := gin.Default()
	r.GET("/ping", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "pong",
		})
	})
	r.Run()
}
```

## docker-compose.yml

```
version: '3.4'
services:
  golang:
    build:
      context: ./golang
      dockerfile: dockerfile
    container_name: golang
    command: ["go","run","app.go"]
    ports:
      - "8001:8080"
```


# Command to use on docker compose

## docker-compose

start docker-compose

```
docker-compose up -d 
```

can use **--build** at the first time build project.

stop and remove 
```
docker-compose down
```

show all containers running
```
docker container ls
```

and then show all within exited containers, use **ls -a**

## hub.docker.com

for download image  [anelhaman/dockercompose_golang](https://hub.docker.com/r/prch12/docker_golang/)
