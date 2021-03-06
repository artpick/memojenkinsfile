# Memo for JenkinsFile

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
## Load external groovy file
```groovy
final someInstance = load 'SomeGroovyFile.groovy'
someInstance.doTheJob('some string')
```
**Note:**
_The external file loading does not seem to appreciate calling "remote" closure, so we have to declare methods like that:_
```groovy
def callSendEmails(String parsingResult){
    sendTheFitnesseReportByEmail parsingResult
}
return this
```
_Always **return this**, plus declare methods with **def**_

## Trigger Jenkins job from gitlab when dev branch is merged in a specific *master* branch
```groovy
import com.dabsquared.gitlabjenkins.trigger.filter.BranchFilterType

pipeline {

    agent any
    triggers {
        gitlab(triggerOnPush: true,
                triggerOnMergeRequest: false,
                skipWorkInProgressMergeRequest: true,
                ciSkip: true,
                branchFilterType: BranchFilterType.NameBasedFilter,
                includeBranchesSpec: "master",
                excludeBranchesSpec: '',
                setBuildDescription: true)
    }
 }  
```

## External documentation
* [Jenkins 2 Pipeline global explanations](http://www.slideshare.net/SlawaGiterman/delivery-pipeline-as-code-using-jenkins-20-pipeline)
