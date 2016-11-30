# basic-boot-buildpack

This version of the buildpack can be used to install an [agent app](https://github.com/cf-platform-eng/secret-agent/tree/master/agent) to be run alongside [another app](https://github.com/cf-platform-eng/secret-agent/tree/master/passthrough) in a single container.

In this case, the "other app" will passthrough requests to the agent and return the results. The agent is running alongside the passthrough app in the same container, and cannot be reached other than through the passthrough.
 
To use this buidpack create a manifest (such as the example below) and use it to push your app. The agent will be installed by the buildpack alongside your app. Make sure to allow enough memory for both your app and the agent. The app can be scaled up and down as per any other cf application, and each new instance will get its own agent.
 
````yaml
applications:
- name: passthrough
  memory: 1G
  instances: 1
  path: target/passthrough-1.0.0.jar
  buildpack: https://github.com/cf-platform-eng/basic-boot-buildpack
 ```

##Important Note!
Before using this buildpack you will want to make sure you are pointing to the latest jre to make sure that any CVEs have been mitigated. See the detect script for how to control this.
