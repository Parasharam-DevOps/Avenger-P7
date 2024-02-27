# Declarative Pipeline For JAVA Bug Analysis

| **Author** | **Created On** | **Last Updated** | **Document Version** |
| ---------- | -------------- | ---------------- | -------------------- |
| **Parasharam Desai** | 07-02-2024 | 07-02-2024 | V1 |

***


# Table of Contents

1. [Introduction](#introduction)
2. [What is Declarative Pipeline](#what-is-declarative-pipeline)
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


# What is Declarative Pipeline

Declarative Pipeline in Jenkins offers a simplified and structured approach for defining CI/CD pipelines, using a human-readable syntax with predefined sections like pipeline, stages, and agent. It's designed to be easy to read and maintain, making it suitable for users without strong scripting skills.It enforces a stricter syntax and allows for less flexibility compared to the scripted pipeline, which can be seen as an advantage for ensuring consistency and readability.
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

![image](https://github.com/avengers-p7/Documentation/assets/156056709/e2fda358-19eb-4444-aab6-8b8a259e278a)


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

                        
                   pipeline {
                                agent any
                                
                                tools {
                                    maven 'mvn'
                                }
                                
                                stages {
                                    stage("Git Checkout") {
                                        steps {
                                            script {
                                                git branch: 'main', url: 'https://github.com/Parasharam-Desai/salary-api.git'
                                            }
                                        }
                                    }
                                    
                                    stage("Bug Analysis ") {
                                        steps {
                                            script {
                                                sh 'mvn compile'
                                                sh 'mvn spotbugs:spotbugs'
                                                sh 'mvn site'
                                            }
                                        }
                                    }
                                    
                                    stage('Publish HTML Report') {
                                        steps {
                                            script {
                                                publishHTML([
                                                    allowMissing: false,
                                                    alwaysLinkToLastBuild: true,
                                                    keepAll: true,
                                                    reportDir: 'target/site',
                                                    reportFiles: 'spotbugs.html',
                                                    reportName: 'SpotBugs Report'
                                                ])
                                            }
                                        }
                                    }
                                }
                            }

**Description:**

- `mvn compile`: This command compiles the Java source code in the project.
- `mvn spotbugs:spotbugs`: This command executes the SpotBugs analysis using the SpotBugs Maven plugin. SpotBugs is a static analysis tool that identifies potential bugs in Java code.
- `mvn site`: The Maven site goal generates various reports, including a report for bug analysis.
  


**6. Evaluate Output: Based on the console output provided below, we can infer that there are a few bugs present**

![image](https://github.com/avengers-p7/Documentation/assets/156056709/837893e7-1711-4e3a-aa03-353329961d68)

![image](https://github.com/avengers-p7/Documentation/assets/156056709/b2924623-af39-4d50-b457-f8125843252c)


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
| Jenkinsfile Code          | [SJenkinsfile](https://github.com/avengers-p7/Jenkinsfile/blob/main/Declarative%20Pipeline/Java/BugAnalysis/Jenkinsfile) |
|Pipeline Generic Doc|[Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GenericDoc/jenkinsPipeline.md)|
| Set up Jenkins Pipeline job & Configure your pipeline |[Link](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Implementation/GenericDoc/jenkinsPipeline.md)|
