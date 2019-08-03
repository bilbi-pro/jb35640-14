# Friday Practice

## Subject to be covered:
- Git Operations
- Build Frameworks & Build Targets
- Jenkins
  - Management & configurations
  - Jenkins cluster simulation
  - Jenkins Pipeline:
    - Plugins 
    - Triggers

- SDLC – implementing using SonarQube


## Introduction:
In this practice we will provide a CI environment and build a simple maven project and we will deploy its output into a running tomcat and into new Docker Container.
We will mix all the knowledge we collected so far.
Please follow carefully after each step of this manual, since the exercise is a bit complex.

### User story:
You are a DevOps engineer, that called by a client to provide him full CI environment for POC purpose. 
The client gave you the following demands:
- Since it is a POC environment, he doesn’t want you to create or install any new server. The whole SLN should be running from your work station completely
- Since he gave you only single workstation to present the POC, and you need to simulate multiple server environment, using docker based solution is advised.
- The environment should build from the following components:
  - One Jenkins master
  - 2 Jenkins Slaves
  - 1 SonarQube server
  - 1 Nexus server
- Since the containers might failing from time to time, you need to provide some data persistency. Using folder-based mounts it is advised.
- Since this is a POC, no access to source code of the organization is allowed
- You must provide 1 pipelines, that includes SCM pull, build, test and publish into Nexus. Publishing to the nexus repository will be based on the branch type, meaning, develop will publish into a “develop” repository, and master will be published into a “master” repository. Also, in case of security scan fails, the artifact will be published into a “suspected” repository. The client demands that the developers will able to work against single repository rather that those 3 mentioned.
- The client wants to be able see the unit tests results in the Jenkins job’s page. Using the Junit plugin \build step to achieve that
- The client wants to be able see the security scans results in the Jenkins job’s page.
- When the artifact passes the security check, the artifact marked as “passed_sec” in it’s repository

## Important notes:
- You will need to create a new Git repo for the project. The git repo should have 2 branches, master and develop
> TASK 1: Create the Git Repo, with the proper settings defined

- The source code will be generated from following site: https://start.spring.io/ 
  - Make sure you are selecting the following configs:
    - Project= Maven Project
    - Language=Java
    - SpringBoot=2.1.6
    - Group=%your name group%
    - Artifact= %Choose your own%
    - Packaging=War
    - Java=8

> Task 2 (Bonus): Create automatic script to get the code  
> Tip: open browser’s developer tools


## Steps to solve this exercise:
- Read and understand
- Build the Code Infra (Code & Git Repo)
- Draw a temp Diagram with the current knoledge you have collected
- Build the Code Infra (Code & Git Repo)

## SLN:
Build the Code Infra (Code & Git Repo)
* create new repository in github
*
> mkdir ~/Desktop/par12
>
> git clone ${REPOURI} .
> git checkout -b develop
> ##DOWNLOADING THE ZIP
> curl -Ls 'https://start.spring.io/starter.zip?type=maven-project&language=java&bootVersion=2.1.6.RELEASE&baseDir=demo&groupId=com.example&artifactId=demo&name=demo&description=Demo%20project%20for%20Spring%20Boot&packageName=com.example.demo&packaging=war&javaVersion=1.8' -H 'accept-encoding: gzip, deflate, br' -H 'accept-language: en-US,en;q=0.9' -H 'user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.103 Safari/537.36' -H 'accept: */*' -H 'referer: https://start.spring.io/' -H 'authority: start.spring.io' -H 'cookie: __cfduid=dc48cf73d23147e14da2c90cd435145be1564732074; _ga=GA1.2.1833892980.1564732081; _gid=GA1.2.1365990929.1564732081; _gat_UA-2728886-19=1; _ga=GA1.3.1833892980.1564732081; _gid=GA1.3.1365990929.1564732081; _gat_UA-2728886-24=1; notice_behavior=none' –compressed -o code.zip
>
> unzip code.zip -d .
>
> rm code.zip
>
>git add .
>
> Git commit -m “initial commit”
>
> git push -u origin develop

## Build Env:
> mkdir -p /par12/{js1,jm,nexus,SonarQube}
> chmod +777 -R /par12
>
>> docker run -d --restart=always --name="jenkins_master" \
>>    -v /par12/jm/:/var/jenkins_home/ \
>>    -p 18080:8080 \
>>    -p 50000:50000 \
>>    jenkins/jenkins:lts
>
>> docker run -d --restart=always --name="nexus" \
>>    -v /par12/nexus:/nexus-data/ \
>>    -p 18081:8081 \
>>    sonatype/nexus3
>
>> docker run -d --restart=always --name="sonarqube" \
>>    -/par12/SonarQube/:/opt/sonarqube/data/ \
>>    -p 19000:9000 \
>>    sonarqube
>
>> docker run -d --restart=always --name="jenkins_slave1" \
>    -v /par12/js1/:/home/jenkins/ \
>    jenkins/slave
