# docker-nginx-gcs-proxy
A Docker image for running Nginx as a caching proxy for Google Cloud Storage.

This is the Git repo for the Docker image built automatically at Docker Hub - 
[socialwifi/nginx-gcs-proxy](https://hub.docker.com/r/socialwifi/nginx-gcs-proxy/).

## Usage

```bash
cd nginx-gcs-proxy/
docker build -t nginx-gcs-proxy .
docker run -d -e -p 8080:8080 nginx-gcs-proxy
curl -v http://127.0.0.1:8080/<bucket>/<object>
```

## Configuration

The following tables lists the configurable environment variables of nginx-gcs-proxy and their default values.

Variable | Description | Default
--- | --- | ---
`LISTEN_PORT` | Server listen port | 8080
`NOT_FOUND_MEANS_INDEX` | When requested path is not found in the bucket, return index.html. Useful when serving single page apps, like Angular, React, Ember. Possible values: "true", "false". | false

## Health-checking

```bash
curl -v http://127.0.0.1:8080/healthz/

```
```
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 8080 (#0)
> GET /healthz/ HTTP/1.1
> Host: 127.0.0.1:8080
> User-Agent: curl/7.55.1
> Accept: */*
> 
< HTTP/1.1 200 OK
< Server: nginx
< Date: Wed, 17 Jan 2018 14:22:23 GMT
< Content-Type: application/octet-stream
< Content-Length: 0
< Connection: keep-alive
< 
* Connection #0 to host 127.0.0.1 left intact
```

## Building

```bash
docker build nginx-gcs-proxy -t nginx-gcs-proxy

```

## Testing

```bash
docker run --rm -e nginx-gcs-proxy nginx -t
```
