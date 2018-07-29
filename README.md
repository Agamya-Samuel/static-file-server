# static-file-server
Tiny, simple static file server using environment variables for configuration

Available on Docker Hub at https://hub.docker.com/r/halverneus/static-file-server/

Environment variables with defaults:
```bash
# Optional Hostname for binding. Leave black to accept any incoming HTTP request
# on the prescribed port.
HOST=
# If assigned, must be a valid port number.
PORT=8080
# Automatically serve the index file for a given directory (default). If set to
# 'false', URLs ending with a '/' will return 'NOT FOUND'.
SHOW_LISTING=true
# Folder with the content to serve.
FOLDER=/web
# URL path prefix. If 'my.file' is in the root of $FOLDER and $URL_PREFIX is
# '/my/place' then file is retrieved with 'http://$HOST:$PORT/my/place/my.file'.
URL_PREFIX=
# Paths to the TLS certificate and key. If one is set then both must be set. If
# both set then files are served using HTTPS. If neither are set then files are
# served using HTTP.
TLS_CERT=
TLS_KEY=
```

Matching configuration YAML settings. YAML settings are individually overridden
by the corresponding environment variable. The following is an example
configuration file with defaults. Pass in the path to the configuration file
using the command line option ('-c', '-config', '--config').

```yaml
host: ""
port: 8080
show-listing: true
folder: /web
url-prefix: ""
tls-cert: ""
tls-key: ""
```

### Without Docker
```bash
PORT=8888 FOLDER=. ./serve
```
Files can then be accessed by going to http://localhost:8888/my/file.txt

### With Docker
```bash
docker run -d -v /my/folder:/web -p 8080:8080 halverneus/static-file-server:latest
```
This will serve the folder "/my/folder" over http://localhost:8080/my/file.txt

Any of the variables can also be modified:
```bash
docker run -d -v /home/me/dev/source:/content/html -v /home/me/dev/files:/content/more/files -e FOLDER=/content -p 8080:8080 halverneus/static-file-server:latest
```

### Also try...
```bash
./serve help
# OR
docker run -it halverneus/static-file-server:latest help
```
This maybe a cheesy program, but it is convenient and less than 6MB in size.