# Proof of Concept (POC) for Java Unit Testing

| **Author** | **Created On** | **Last Updated** | **Document Version** |
| ---------- | -------------- | ---------------- | -------------------- |
| **Parasharam Desai** | 28-01-2024 | 30-01-2024 | V1 |

## Table of Contents

1. [Introduction](#introduction)
2. [Testing Framework](#testing-framework)
3. [Overview](#overview)
4. [Prerequisites](#prerequisites)
5. [Steps](#steps)
    - [Cloning a Java App](#cloning-a-java-app)
    - [Install Java 17 and Maven](#install-java-17-and-maven)
    - [Add the JUnit dependency in pom.xml file](#add-the-junit-dependency-in-pomxml-file)
    - [Add Maven dependency in pom.xml file](#add-maven-dependency-in-pomxml-file)
    - [Revise Surefire Plugin Configuration in pom.xml](#revise-surefire-plugin-configuration-in-pomxml)
    - [Uncomment the version of Surefire Plugin and change the version](#uncomment-the-version-of-surefire-plugin-and-change-the-version)
    - [Run Java Unit Test](#run-java-unit-test)
    - [Generate HTML report with Surefire](#generate-html-report-with-surefire)
6. [POC Conclusion](#poc-conclusion)
7. [Contact Information](#contact-information)
8. [Resources and References](#resources-and-references)

## Introduction 

Unit testing in Java is a crucial practice that involves testing individual units or components of Java code to ensure their correctness and functionality. Java unit testing is typically performed by Java developers and is an essential part of the software development process. Below, I'll provide the steps of performing unit testing in Java.

## Testing Framework

Java unit testing is often facilitated by testing frameworks, with JUnit being one of the most popular choices. These frameworks provide a structured and organized way to write and execute unit tests. Some other frameworks like TestNG and Mockito are also commonly used in Java unit testing.

## Overview

The developer has already authored the unit test cases for the application.

You can find these test cases located in the directory path: 

    src/test/java/com/opstree/microservice/salary.

JUnit, a testing framework, plays a pivotal role in enabling Java unit testing within this context.

    Repository Link: [OT-MICROSERVICES](https://github.com/OT-MICROSERVICES/salary-api.git)

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/e4437f15-a559-43a4-9367-eb7aecca1f78)

## Prerequisites

**Java Version 17** (mentioned in pom.xml)  

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/3a93c93a-5008-418e-b2f5-ff7e1ef1bef4)

**Maven** - As it simplifies the process of managing project dependencies, including testing dependencies.

**JUnit** - As it's a library on which the project's tests is depended on. 

## Steps

### Cloning a Java App

Within the directory, make a clone of the repository.

    mkdir snaatak-P7
    cd snaatak-P7
    git clone https://github.com/OT-MICROSERVICES/salary-api.git

### Install Java 17 and Maven

As the salary code is Java-based, it is designed to be compatible with Java version 17. It is advisable to install Maven, a crucial tool for managing and building Java projects.

    sudo apt update
    sudo apt install openjdk-17-jdk
    sudo apt install maven

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/4c12c52e-dcba-48bd-aa1f-94a94c42dfdf)

### Add the JUnit dependency in pom.xml file.

    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/52947b33-cef9-42c7-970c-3e39a862f4a7)

### Add maven dependency in pom.xml file.

    <dependency>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
        <type>maven-plugin</type>
    </dependency>

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/6bced278-8a21-4959-89ed-7596ead60bd8)

### Revise Surefire Plugin Configuration in pom.xml

Address compatibility issue with JUnit by uncommenting and updating surefire plugin version.

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/76800f61-50ac-4ba7-99f2-13058980cdb2)

### Uncomment the version of Surefire Plugin and also change the version from 2.17 to 3.0.0

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/090207f8-7a0a-4cd8-ace0-fe47aaecb1c7)

### Run Java Unit Test

    mvn test 

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/7bd0ec27-bffe-48c2-ac85-8f4a93bbfe75)

![image](https://github.com/avengers-p7/Documentation/assets/156056709/6ac027a8-85e3-4b31-8ad1-8da93035cf82)

### Generate HTML report with Surefire.

This command will generate an html report. To access unit test report, navigate to the target > site > right-click > Open in Browser.

    mvn surefire-report:report

![image](https://github.com/avengers-p7/Documentation/assets/156056709/486dbecd-8438-4367-a5b3-ab123ac27a3a)
![image](https://github.com/avengers-p7/Documentation/assets/156056709/39df6f1b-f373-4db4-9cdf-f904c1c544ba)
![image](https://github.com/avengers-p7/Documentation/assets/156056709/de771f0f-419e-4ab9-ae3b-643d8282b271)

### POC Conclusion

In summary, Java unit testing is vital for ensuring code quality, reliability, and maintainability in software development. Utilizing best practices, including employing a dependable testing framework like JUnit, writing isolated test cases, and automating testing with tools like Maven and Gradle, enables developers to validate code units effectively. Embracing test-driven development (TDD) methodologies and regular test report reviews contribute to the creation of robust, error-free software. Java unit testing lays the foundation for high-quality applications, playing a crucial role in early issue detection and overall improvement of the software development lifecycle.

## Contact Information

|    Name                                   | Email Address                    |
|-------------------------------------------|----------------------------------|
| **[Parasharam Desai](https://github.com/Parasharam-Desai)** | parasharam.desai.snaatak@mygurukulam.co |

## Resources and References

|     Description                  | References  
| ---------------------------------| ------------------------------------------------------------------- |
|     Documentation Template       | [Link](https://github.com/OT-MICROSERVICES/documentation-template/wiki/Application-Template) |
| JUnit – Generating HTML Reports  | [Link](https://howtodoinjava.com/junit5/junit-html-report) |
