# Memo for jenkisn files

## Global variables
* **BUILD_ID** : The current build ID, identical to BUILD_NUMBER for builds created in Jenkins versions 1.597+
* **JOB_NAME** : Name of the project of this build, such as "foo" or "foo/bar".
* **JENKINS_URL** : Full URL of Jenkins, such as example.com:port/jenkins/ (NOTE: only available if Jenkins URL set in "System Configuration")

## Scripts call with return
```groovy
final result = sh (returnStdout : true, script : "some sh with ${parameters}") 
```
## Load pom file
```groovy
final pom = readMavenPom file: 'pom.xml'
```
