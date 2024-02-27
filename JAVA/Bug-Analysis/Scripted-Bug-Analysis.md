# Scripted Pipeline For JAVA Bug Analysis


| **Author** | **Created On** | **Last Updated** | **Document Version** |
| ---------- | -------------- | ---------------- | -------------------- |
| **Parasharam Desai** | 07-02-2024 | 07-02-2024 | V1 |

***


# Table of Contents

1. [Introduction](#introduction)
2. [What is Scripted Pipeline](#what-is-scripted-pipeline)
3. [Prerequisites](#prerequisites)
4. [Flow Diagram](#Flow-Diagram)
5. [Steps to run Pipeline](#steps-to-run-pipeline)
6. [Conclusion](#conclusion)
7. [Contact Information](#contact-information)
8. [Resources and References](#resources-and-references)


***
# Introduction
Establishing a Java pipeline for bug analysis typically involves leveraging a CI/CD (Continuous Integration/Continuous Deployment) tool to automate the process of building, testing, and potentially deploying your Java application. Here we will be utilizing the Spotbugs plugin for bug scanning to ensure the quality and reliability of our codebase.

If you want to learn more about Bug Analysis , refer to this detailed documentation: [Bug Analysis Documentation](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/03-%20Java%20CI%20checks/Bug%20Analysis/README.md)

# What is Scripted Pipeline
A Scripted Pipeline in Jenkins is a Groovy-based approach to defining continuous integration and continuous delivery (CI/CD) pipelines. It allows users to write pipeline scripts using Groovy syntax, providing full flexibility and customization for defining build, test, and deployment stages. Scripted Pipelines enable users to incorporate conditional logic, loops, and functions within the pipeline script to handle complex workflows and custom requirements. While offering extensive power and flexibility, Scripted Pipelines require users to have knowledge of Groovy programming and scripting concepts. They are well-suited for projects with intricate build processes or those requiring advanced automation and customization capabilities.

To know more about pipelines please follow this [Reference Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GenericDoc/jenkinsPipeline.md)




***
# Prerequisites

| **Jenkins (2.426.3)** | Enables Continuous Integration |
| ---------------- | -------------------- |
| **Java 17** | Required for compiling Jenkins and Spring Boot projects |
| **Maven(3.6.9)** | Handles build automation and dependency management |
| **Spotbug (4.8.1)** | Employed for bug analysis |
***
# Flow Diagram

![image](https://github.com/avengers-p7/Documentation/assets/156056709/406e1a2b-6fc1-4a1a-b385-fa15be608cf9)



***

# Steps to run Pipeline

**1. Fork the repository:** You can Fork the repository from GitHub - [**Repo Link**](https://github.com/Parasharam-Desai/salary-api.git).

**2. The Spotbugs plugin needs to be included in the pom.xml file.**

[Click here for reference](https://github.com/Parasharam-Desai/salary-api/blob/main/pom.xml) to view the pom.xml file.


            <plugin>
                  <groupId>com.github.spotbugs</groupId>
                  <artifactId>spotbugs-maven-plugin</artifactId>
                  <version>4.8.1.0</version>
                  <executions>
                      <execution>
                          <id>spotbugs-check</id>
                          <phase>verify</phase>
                          <goals>
                              <goal>check</goal>
                          </goals>
                      </execution>
                  </executions>
                  <dependencies>
                      <dependency>
                          <groupId>com.github.spotbugs</groupId>
                          <artifactId>spotbugs</artifactId>
                          <version>4.8.1</version>
                      </dependency>
                  </dependencies>
              </plugin>

              
* Include the Spotbugs-maven-plugin within the reporting section. This ensures that running mvn site will generate the Spot Bugs report.

              <reporting>
                  <plugins>
                      <plugin>
                          <groupId>com.github.spotbugs</groupId>
                          <artifactId>spotbugs-maven-plugin</artifactId>
                          <version>4.8.1.0</version>
                      </plugin>
                  </plugins>
              </reporting>
 

**3. Configure Maven tool in Jenkins**

Go to `Dashboard--> Manage Jenkins--> Tools` and configure maven tool.

![image](https://github.com/avengers-p7/Documentation/assets/156056444/d9ff8a0d-900a-4e4b-ac68-34507ef3348b)

**4. Set up Jenkins Pipeline job & Configure your pipeline using the detailed documentation provided in the following link:**
**

**[Reference Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GolangCI/CodeCompilation/Scripted%20Pipeline/README.md)**

**5. Now Build Your Pipelne**


        node {
            stage("Git Checkout") {
                git branch: 'main', url: 'https://github.com/Parasharam-Desai/salary-api.git'
            }
            
            stage("Bug Analysis") {
                sh 'mvn compile'
                sh 'mvn spotbugs:spotbugs'
                sh 'mvn site'
            }
            
            stage('Publish HTML Report') {
                step([$class: 'PublishHTMLPublisher', 
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'target/site',
                    reportFiles: 'spotbugs.html',
                    reportName: 'SpotBugs Report'
                ])
            }
        }

**Description:**

- `mvn compile`: This command compiles the Java source code in the project.
- `mvn spotbugs:spotbugs`: This command executes the SpotBugs analysis using the SpotBugs Maven plugin. SpotBugs is a static analysis tool that identifies potential bugs in Java code.
- `mvn site`: The Maven site goal generates various reports, including a report for bug analysis.
  


**6. Evaluate Output: Based on the console output provided below, we can infer that there are a few bugs present.**

![image](https://github.com/avengers-p7/Documentation/assets/156056709/c4f512f0-7f9f-48ef-b6d7-d38315107d7c)


![image](https://github.com/avengers-p7/Documentation/assets/156056709/9af79b6e-ba45-47a1-9330-e3f3a52387d4)


***

# Conclusion

This pipeline will clone your source code repository, compile the project using Maven, and conduct bug scanning.


# Contact Information

|    Name                                   | Email Address                    |
|-------------------------------------------|----------------------------------|
| **[Parasharam Desai](https://github.com/Parasharam-Desai)** | parasharam.desai.snaatak@mygurukulam.co |

***
# Resources and References

|       **Description**                                   |           **References**                    |
|---------------------------------------------------------|-----------------------------------------------|
| Jenkins Pipeline     | [Jenkins Pipeline Documentation](https://www.jenkins.io/doc/book/pipeline/) |
| Using Spotbug Plugins                 | [Spotbugs Maven Plugin Documentation](https://spotbugs.readthedocs.io/en/latest/maven.html) |
| Guide to use SpotBugs           | [SpotBugs Maven Configuration Guide](https://github.com/find-sec-bugs/find-sec-bugs/wiki/Maven-configuration) |
| Jenkinsfile Code          | [(Jenkinsfile](https://github.com/avengers-p7/Jenkinsfile/blob/main/Scripted%20Pipeline/Java/BugsAnalysis/Jenkinsfile) |
|Pipeline Generic Doc|[Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GenericDoc/jenkinsPipeline.md)|
| Set up Jenkins Pipeline job & Configure your pipeline |[Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GenericDoc/jenkinsPipeline.md)|
