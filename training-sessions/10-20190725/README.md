Here is the practice me made in the class:

##par10-1 
1. write pipeline 
2. jobs params: 
    - ART_NAME -> the name of the artifact
    - ART_GROUP -> the name of the artifact 3 
    - ART_VERSION -> the naAe of the artifact 4 
    - GIT_BRANCH - > the source branch to use 5 
3. use some "X" plugin, to read the pom.xml file 
    - if "ART_NAME" is empty, use the name difined in the pom.xml 
    - if "ART_GROUP" is empty, use the name difined in the pom.xml 
    - if "A10-_VERSION" is empty, use the name difined in the pom.xml 
        Please remember! to add the current build number
4. if the build was with branch "master" publish to "release", else to 1 
5. prompt the user input question, "to deploy to local tomcat?",
    if user selects "yes" the war file will be copied to tomcat's webapp directory "/usr/share/tomcat/webapps" 
    - DONOT RESTART TOMCAT

Plugins to use:
- input
- readpom 30 31 
 
