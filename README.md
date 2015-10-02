# Overview

This container is the basis by which multiprocess StackEngine services are 
built. 

Upon choosing [`runit`](http://smarden.org/runit/index.html) as the init system
for such a container, the assumption is that it will need to be started. 
Everything else is placing init scripts in `/etc/sv/<service-name>`.

# Usage

## Building from this Image

```Dockerfile
# Sample Dockerfile
FROM stackhub/base-runit
MAINTAINER awesome_communitymember <myaddress@example.com>

# Lot's of cool stuff here

```

For an example see our 
[`stackhub/base-confd`](https://github.com/stackhub/base-confd/blob/master/Dockerfile) 
image that makes it easy to leverage StackEngine Service Discovery.

## Developing Interactively with this Image

If you would like to build your own multi-process container from this image or
play directly with `runit` run a detached container and contect to it.

```
%> docker run -d --name good_idea stackhub/base_runit
%> docker exec -it good_idea sh
/ #
```

A typical workflow might be to: 

* install a process like haproxy, nginx or prometheus manually with the 
  `apk` package manager
* get the init script correct for starting, stopping and reloading the process
* ensure that the logging is done properly (e.g. STDOUT and STDERR) so that
  `docker logs` is the single source of truth for process information
* ensure that when the process fails the container dies (i.e. avoids the 
  "zombie container" problem)
* Write a Dockerfile from this research, build and test it.  

# Compatibility 

* [x] StackEngine Ecosystem
* [x] General Docker Ecosystem

This image is generally useful as it does not leverage any of the special 
features of the StackEngine Container Application Center.

# License

MIT