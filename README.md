# basic-boot-buildpack

This is the most basic buildpack imaginable. It will run a spring boot application. That is all.

It is designed to be used with the [multi-buildpack](https://github.com/cloudfoundry-incubator/multi-buildpack) for things like installing agents implemented in spring-boot, to be run alongside other applications inside a container.

The buildpack is hard-coded to return false during the detect phase, so it will not be activated by apps pushed via cf push.
 
To use it to run an app add this buildpack directly to the push command (via the -b flag) or declare it in the app's manifest.
 
````yaml
 applications:
 - name: my-boot-app
   memory: 512M
   instances: 1
   path: target/my-boot-app.jar
   buildpack: https://github.com/cf-platform-eng/basic-boot-buildpack
 ```

##Important Note!
Before using this buildpack you wil want to make sure you are pointing to the latest jre to make sure that any CVEs have been mitigated. See the detect script for how to control this.
