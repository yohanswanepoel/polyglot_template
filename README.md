# polyglot_template
This is a polyglot application to demonstrate working OpenShift environment. It uses different techniques to demonstrate use cases such as:
* Onboarding: Single OpenShift Catalogue item that provisions complete environment
* How different technologies such as Java and Python can work together
* Breakig up of a monolith - each component has it's own database
* Secure and standardised builds using Source to Image
* Can be used to show innerloop development using OpenShift DO commandline

![Architecture Image](https://raw.githubusercontent.com/yohanswanepoel/polyglot_template/master/docs/arch.png)

1. The template is stored in GIT and exposed on the OpenShift catalogue
2. A user requests the complete environment using the template
3. The template triggers S2I builds for Python and Java compnents and provisions. Build 4. config pulls source directly from GIT
4. The user interacts with the Managent UI via OpenShift Router
5. The router routes request messages to the Management UI service. Allowing scaling
6. The management UI interacts with the Provider API via REST using the internal service network
7. The management UI interacts with the Reliant Party API via REST using the internal service network

## Deploy template

### Pre-Reqs
* Access to pypi or a suitable internal repository. Internal repo requires config during deploy
* Access to Java repo or a suitable internal repository. Internal repo requires POM file changes in Provider API pom.xml

### Deploy
* Import template. If you have permission put it in [openshift] project or you can import it in your own project
```bash
oc create -f full_environment.json -n <project>
```
* Deploy template through UI to set variables or using CLI
* List variables in CLI
```bash
oc process --parameters -f full_environment.json
```
* Deploy template
```bash
oc process --parameters -n <project> polyglot-sample
```
For more information see the OpenShift documentation

## Clean up environment
```bash
oc project [your project]
oc delete --all deploymentconfig,imagestream,buildconfig,route,service,secret
```

