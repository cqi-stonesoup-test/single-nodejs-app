# Simple Container Based App   
# test
## Build containerized app using the Stone Soup  

This repo contains a a simple container based app that can be built and deployed on Stone Soup build environment.
The application itself can run and shows a simple web page with these same instructions using a simple node.js server to serve up HTML pages. 

You can use the default managed stone soup environment with CLI access or you can create your own stone soup backend by cloning `https://github.com/redhat-appstudio/infra-deployments.git` and installing a developer version on your own cluster. 

Skip steps 1 and 2 if you are using a staging or managed stone soup instance
  
  1.  Bootstrap your cluster       `./hack/bootstrap-cluster.sh preview  `
  2.  Create a project for your app `oc new-project demo`  
  
  3.  Create an Application with the following yaml 
```
apiVersion: appstudio.redhat.com/v1alpha1
kind: Application
metadata:
  name: single-nodejs-app
spec:
  description: "single-nodejs-app built in Stone Soup"
  displayName: single-nodejs-app
```
  4.  Create an Component with the following yaml   
```
apiVersion: appstudio.redhat.com/v1alpha1
kind: Component
metadata:
  name: single-nodejs-app
spec:
  componentName: single-nodejs-app
  application: single-nodejs-app
  containerImage: quay.io/jduimovich0/single-nodejs-app
  source:
    git:
      url: https://github.com/jduimovich/single-nodejs-app
      devfileUrl: https://raw.githubusercontent.com/jduimovich/appstudio-e2e-demos/main/demos/single-nodejs-app/devfiles/devfile.yaml
  build:
    containerImage: quay.io/jduimovich0/single-nodejs-app
```

Stone soup will build and deploy your application. In the manage stone soup environment use the UI to browse to your running application.  

If are using CLI only to access, use `oc get routes` to find the URL to your application.


 
