# Simple API Source2Image Openshift example
## Steps
- Intall S2I
- Build the image: `s2i build . <BASEIMAGE> <IMAGESTREAM>` (`s2i build . fortinj66/centos7-s2i-nodejs:8.1.4 s2i-simpleapi`)
- Tag the image: `docker tag s2i-simpleapi <DOCKER-REGISTRY-HOST>/<NAMESPACE>/<IMAGESTREAM>:<TAG>` (`docker tag s2i-simpleapi myregistry.com/dieter/s2i-simpleapi:latest`)
- Login to the Openshift cluster: `oc login <OPENSHIFT-HOST>` and provide your username and password
- Get a registry token: `oc whoami -t`
- Login to the Docker Registry: `docker login -p <TOKEN> -u <USERNAME> <DOCKER-REGISTRY-LOCATION>`
- Push the image: `docker push <DOCKER-REGISTRY-HOST>/<NAMESPACE>/<IMAGESTREAM>:<TAG>` (`docker push myregistry.com/dieter/s2i-simpleapi:latest`)
- Create a new app based on this image: `oc new-app <NAMESPACE>/<IMAGESTREAM>:<TAG>` (`oc new-app dieter/s2i-simpleapi:latest`)
- Expose the service: `oc expose svc <SERVICENAME>` (`oc expose svc s2i-simpleapi`)
- Get the route: `oc get route s2i-simpleapi`
- Do a curl