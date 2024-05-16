# Labo03 - Run a first container

## Pedagogical intent

In this lab, you'll:

* Get to grips with the first Docker commands,
* Run your first Docker
* Familiarize yourself with port publishing

---

Note: the docker engine must be running

## Task 01 - Get to grips with the first Docker commands

* List all images present on your installation

[INPUT]
```bash
docker images
```

[OUTPUT]
```
REPOSITORY                    TAG       IMAGE ID       CREATED        SIZE
gcr.io/k8s-minikube/kicbase   v0.0.42   dbc648475405   6 months ago   1.2GB
```

* Get the official Nginx image using this command

[INPUT]
```bash
docker pull nginx
```

[OUTPUT]
```
Using default tag: latest
latest: Pulling from library/nginx
09f376ebb190: Pull complete
a11fc495bafd: Pull complete
933cc8470577: Pull complete
999643392fb7: Pull complete
971bb7f4fb12: Pull complete
45337c09cd57: Pull complete
de3b062c0af7: Pull complete
Digest: sha256:a484819eb60211f5299034ac80f6a681b06f89e65866ce91f356ed7c72af059c
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview nginx
```

Note : do you see the different layer uploaded ?

* List -again- all image present on your installation

[INPUT]
```bash
docker images
```

[OUTPUT]
```
REPOSITORY                    TAG       IMAGE ID       CREATED        SIZE
nginx                         latest    e784f4560448   12 days ago    188MB
gcr.io/k8s-minikube/kicbase   v0.0.42   dbc648475405   6 months ago   1.2GB
```

Note : 188 MB is the size of your image... check it.

```
Not sure what to do here...
docker inspect nginx
docker image history nginx
```

* List -again- all image present on your installation

[INPUT]
```bash
docker images
```

[OUTPUT]
```
REPOSITORY                    TAG       IMAGE ID       CREATED        SIZE
nginx                         latest    e784f4560448   12 days ago    188MB
gcr.io/k8s-minikube/kicbase   v0.0.42   dbc648475405   6 months ago   1.2GB
```

* List all Docker

[INPUT]
```
docker ps -a
```

[OUTPUT]
```
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## Task 02 - Run the container

* Run Nginx Docker

[INPUT]
```
docker run nginx
```

[OUTPUT]
```
On windows, the process is attached to the terminal

/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/05/16 06:42:30 [notice] 1#1: using the "epoll" event method
2024/05/16 06:42:30 [notice] 1#1: nginx/1.25.5
2024/05/16 06:42:30 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2024/05/16 06:42:30 [notice] 1#1: OS: Linux 5.15.90.1-microsoft-standard-WSL2
2024/05/16 06:42:30 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/05/16 06:42:30 [notice] 1#1: start worker processes
2024/05/16 06:42:30 [notice] 1#1: start worker process 29
2024/05/16 06:42:30 [notice] 1#1: start worker process 30
2024/05/16 06:42:30 [notice] 1#1: start worker process 31
2024/05/16 06:42:30 [notice] 1#1: start worker process 32
2024/05/16 06:42:30 [notice] 1#1: start worker process 33
2024/05/16 06:42:30 [notice] 1#1: start worker process 34
2024/05/16 06:42:30 [notice] 1#1: start worker process 35
2024/05/16 06:42:30 [notice] 1#1: start worker process 36
2024/05/16 06:42:30 [notice] 1#1: start worker process 37
2024/05/16 06:42:30 [notice] 1#1: start worker process 38
2024/05/16 06:42:30 [notice] 1#1: start worker process 39
2024/05/16 06:42:30 [notice] 1#1: start worker process 40
```

* Can you reach the default page of nginx

Note : By default, Nginx is listening on port 80

[INPUT]
```
On windows
choco install curl

curl localhost
```

[OUTPUT]
```
On windows :

curl : Impossible de se connecter au serveur distant
Au caractère Ligne:1 : 1
+ curl localhost
+ ~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation : (System.Net.HttpWebRequest:HttpWebRequest) [Invoke-WebRequest], WebException
    + FullyQualifiedErrorId : WebCmdletWebResponseException,Microsoft.PowerShell.Commands.InvokeWebRequestCommand
 
```

* Stop this first attempt

[INPUT]
```
docker stop <id>
```

[OUTPUT]
```
fed3e715ee46
```

## Task 03 - Familiarize yourself with port publishing

* Make it possible to reach nginx with this command

[Publish a port](https://docs.docker.com/network/#published-ports)

[INPUT]
```
docker run -p 127.0.0.1:8080:80 nginx
curl localhost:8080
Not working on Powershell / Windows. We need :
curl http://localhost:8080

```

[OUTPUT]
```
StatusCode        : 200
StatusDescription : OK
Content           : <!DOCTYPE html>
                    <html>
                    <head>
                    <title>Welcome to nginx!</title>
                    <style>
                    html { color-scheme: light dark; }
                    body { width: 35em; margin: 0 auto;
                    font-family: Tahoma, Verdana, Arial, sans-serif; }
                    </style...
RawContent        : HTTP/1.1 200 OK
                    Connection: keep-alive
                    Accept-Ranges: bytes
                    Content-Length: 615
                    Content-Type: text/html
                    Date: Thu, 16 May 2024 06:48:08 GMT
                    ETag: "661e8b67-267"
                    Last-Modified: Tue, 16 Apr 2024 ...
Forms             : {}
Headers           : {[Connection, keep-alive], [Accept-Ranges, bytes], [Content-Length, 615], [Content-Type, text/html]...}
Images            : {}
InputFields       : {}
Links             : {@{innerHTML=nginx.org; innerText=nginx.org; outerHTML=<A href="http://nginx.org/">nginx.org</A>; outerText=nginx.org; tagName=A; href=http://nginx.org/}, @{innerHTML=nginx.com; innerText=nginx.com;
                    outerHTML=<A href="http://nginx.com/">nginx.com</A>; outerText=nginx.com; tagName=A; href=http://nginx.com/}}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 615

```

* Stop and delete the container

[INPUT]
```
docker stop 214ac01e2431
docker rm 214ac01e243
```

[OUTPUT]
```
214ac01e2431
214ac01e2431
```

* Delete the image

[INPUT]
```
//TODO delete the image
```

[OUTPUT]
```
//TODO
```
