# group4App1
Jenkins Shared Library:
Jenkins Shared Library avoids repeating the same code in many different pipelines. Copying and pasting the same code into different Jenkins pipelines can become an absolute headache. It implements concept of D.R.Y (Don’t Repeat Yourself).
You can store your “reusable bits” in a Shared Library in Jenkins.
Reusable custom code in Jenkins can
•	read a configuration file
•	perform a code review of the application (e.g. using a tool like SonarQube)
•	do some checks on the target environment
•	perform a deployment
A shared library is a collection of independent Groovy scripts which you pull into your Jenkinsfile at runtime.

How you create a Jenkins library, step-by-step:
a.	First you create your Groovy scripts (see further below for details), and add them into your Git repository.
b.	Then, you add your Shared Library into Jenkins from the Manage Jenkins screen.
c.	Finally, you pull the Shared Library into your pipeline using this annotation (usually at the top of your Jenkinsfile):
 ![image](https://user-images.githubusercontent.com/127508807/231302567-c41f2911-d3a7-46bf-a306-93a3ce51eb22.png)

 
1.	Create the shared library
First you need to create a Git repository which will contain your library of functions (steps). 
In your repository, create a directory called vars. This will hold your custom steps. Each of them will be a different.groovy file underneath your vars directory, e.g.
vars/
    joyceApp.groovy
    benApp.groovy
    josephApp.groovy
    chineduApp.groovy

2.	Add your custom steps
Each of your custom steps is a different.groovy file inside your vars/ directory. In Jenkins terminology, these are called Global Variables, which is why they are located inside vars/.
Create a file for your custom step, and fill in the code. For example:
![image](https://user-images.githubusercontent.com/127508807/231302395-d6337d88-634b-4bda-9c93-57e7fb673036.png)

 
After writing that, you should write your custom code within the braces { }. You can also add parameters to your method as illustrated above.

3.	Set up the library in Jenkins
Now you’ve created your library with custom steps, you need to tell Jenkins about it.
You can define a shared library by configuring the library using the Jenkins web console. It is better to add from the web console, because it shares the library across all of your build jobs.
To add your shared library (I’m using techopsteam5 repository on GitHub as an example):
In Jenkins, go to Manage Jenkins → Configure System. Under Global Pipeline Libraries, add a library with the following settings:
•	Name: pipeline-library-techopsteam5
•	Default version: Specify a Git reference (branch or commit SHA), e.g. main
•	Retrieval method: Modern SCM
•	Select the Git type
•	Project repository:  https://github.com/Ben-Aroh/group4App1.git

4.	Use the library in a pipeline
To use the shared library in a pipeline, you add @Library('your-library-name') to the top of your pipeline definition, or Jenkinsfile. Then call your step by name, e.g. App followed by the application Code Https repoUrl as below:

@Library (‘pipeline-library-name’) _
groovyScriptName ‘your application repoUrl'

NOTE: The underscore (_) is not a typo! You need this underscore if the line immediately after the @Library annotation is not an import statement.

5.	Run the pipeline above, and the output should look something like this:
 
 ![image](https://user-images.githubusercontent.com/127508807/231302265-c0e00b3b-398e-4444-9a69-12aaa4438a27.png)

