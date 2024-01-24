# Comprehensive Guide to Unit Testing in Software Development

| **Author** | **Created On** | **Last Updated** | **Document Version** |
| ---------- | -------------- | ---------------- | -------------------- |
| **Parasharam Desai** | 23-01-2024 | 23-01-2024 | V1 |

***

# Table of Contents

01. [Introduction](#introduction)
02. [What is Unit & Unit Testing?](#what-is-unit--unit-testing)
03. [Why is Unit Testing Important?](#why-is-unit-testing-important)
04. [Different Tools for Unit Testing](#different-tools-for-unit-testing)
05. [Comparison of Unit Testing Tools](#comparison-of-unit-testing-tools)
06. [Unit Testing Advantages](#unit-testing-advantages)
07. [Unit Testing Disadvantages](#unit-testing-disadvantages)
08. [Proof of Concept (POC)](#proof-of-concept-poc)
09. [Best Practices for Unit Testing](#best-practices-for-unit-testing)
10. [Recommendation/Conclusion](#recommendationconclusion)
11. [Contact Information](#contact-information)
12. [Resources and References](#resources-and-references)

***
# Introduction

Welcome to the documentation on Unit and Unit Testing in Software Development. This guide aims to provide a comprehensive understanding of the concepts surrounding unit testing within a software application.

***

## What is Unit & Unit Testing?

In unit testing, a **'unit'** refers to the smallest testable part of a software program, such as a function or method. A **module,** which is nothing but a single unit of software, can also be considered a 'unit.' The goal of unit testing is to test each unit, including modules, in isolation to ensure they work as intended before integrating them into the larger system.

**Unit testing** is a type of software testing where individual units or components of a software application are tested to ensure they meet their design and behavior requirements. These units can be functions, methods, or classes, and they are tested in isolation, without any dependencies on external components.

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/cdfe8356-c6ea-407f-800a-01063a1d21b4)
***

## Why is Unit Testing important?

Unit testing offers several benefits, including:

| **Benefits**                         | **Description**                                                                                          |
|--------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Early bug detection**              | Testing individual units helps identify issues early in the development cycle, reducing overall bug fixing costs.                                                     |
| **Improved code quality**            | Unit tests ensure that each unit functions as expected, leading to a more robust and reliable codebase.                                                             |
| **Faster development**               | Unit tests provide a safety net for developers, allowing them to refactor and improve the codebase with confidence.                                                   |
| **Better collaboration**             | Unit tests help developers understand the expected behavior of individual units, making it easier for teams to collaborate and maintain the codebase. |

***
## Different Tools for Unit Testing

There are various unit testing frameworks available for different programming languages. Some popular ones include:

**Comparison of Unit Testing Tools**
| #   | Tool                           | Official Link                                    | Automated Testing | Manual Testing | Integration Testing | Open Source | Supported Languages | Description                                                                                       |
| --- | ------------------------------ | ------------------------------------------------- | ----------------- | --------------- | -------------------- | ----------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| 1   | JUnit                          | [JUnit](https://junit.org/junit5/)               | Yes               | No              | No                 | Yes         | Java                 | Open-source, widely used for Java, supports TDD(Test-Driven Development).                                                                           |
| 2   | TestNG                         | [TestNG](https://testng.org/doc/index.html)      | Yes               | No              | No                 | Yes         | Java                 | Flexible, parallel testing, highly configurable.                                                                  |
| 3   | NUnit                          | [NUnit](https://nunit.org/)                      | Yes               | No              | No                 | Yes         | .NET (C#, F#)       | Popular for .NET, supports data-driven tests.                                                                            |
| 4   | Unity Test Tools                | [Unity Test Tools](https://docs.unity3d.com/560/Documentation/Manual/testing-editortestsrunner.html) | Yes               | Yes             | Yes                | No          | C#, UnityScript (JavaScript) | Essential for Unity game development, supports various test types.                                                        |
| 5   | Microsoft Unit Testing Framework | [Microsoft Unit Testing Framework](https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-dotnet-test) | Yes            | Yes             | Yes                | No          | .NET (C#, F#)       | Integrated with Visual Studio, suitable for .NET development, supports data-driven testing.                                |
| 6   | HtmlUnit                       | [HtmlUnit](http://htmlunit.sourceforge.net/)    | Yes               | No              | No                 | Yes         | Java                 | GUI-less, supports JavaScript, commonly used with JUnit and TestNG for testing web applications.                  |
| 7   | Parasoft                       | [Parasoft](https://www.parasoft.com/solutions/unit-testing/) | Yes               | Yes             | Yes                | No          | C, C++               | Proprietary tool for C and C++, offers static and dynamic analysis, comprehensive testing for large codebases.           |
| 8   | Cantata                        | [Cantata](https://www.cantata-testing.com/)     | Yes               | Yes             | Yes                | No          | C, C++               | Commercial testing framework, advanced productivity, widely used for unit and integration testing.        |
| 9   | Karma                          | [Karma](https://karma-runner.github.io/)        | Yes               | No              | Yes                | Yes         | JavaScript           | Open-source, runs tests on real devices, supports easy debugging and CI/CD integration.                    |
| 10 | pytest                | [pytest](https://docs.pytest.org/en/latest/)    | Yes               | Yes             | No                 | Yes         | Python               | Third-party library, concise syntax, user-friendly, good command-line support, extensible with plugins.        |



## Unit Testing Advantages

There are many advantages to unit testing, including the following:

- The earlier a problem is identified, the fewer compound errors occur.
- Fixing problems early is usually cheaper than fixing them later in development.
- Easier debugging processes.
- Developers can quickly make changes to the codebase.
- Developers can reuse code and migrate it to new projects.

***

## Unit Testing Disadvantages

While unit testing is integral to any software development and testing strategy, there are some aspects to be aware of. Disadvantages to unit testing include the following:

- Tests will not uncover every bug.
- Unit tests only test sets of data and its functionality -- it will not catch errors in integration.
- More lines of test code may need to be written to test one line of code -- creating a potential time investment.
- Developers may have to learn new skills to implement unit testing correctly; for example, having to learn how to use specific automated software tools.

***

## Proof of Concept (POC) for Java Base Application

Introduction 
Unit testing in Java is a crucial practice that involves testing individual units or components of Java code to ensure their correctness and functionality. Java unit testing is typically performed by Java developers and is an essential part of the software development process. Below, I'll provide the steps of performing unit testing in Java.

Testing Framework
Java unit testing is often facilitated by testing frameworks, with JUnit being one of the most popular choices. These frameworks provide a structured and organized way to write and execute unit tests. Some other frameworks like TestNG and Mockito are also commonly used in Java unit testing.

Overview
The developer has already authored the unit test cases for the application.

You can find these test cases located in the directory path: src/test/java/com/opstree/microservice/salary.

JUnit, a testing framework, plays a pivotal role in enabling Java unit testing within this context.

Repository Link: [OT-MICROSERVICES](https://github.com/OT-MICROSERVICES/salary-api.git)

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/e4437f15-a559-43a4-9367-eb7aecca1f78)

Prerequisites
Java Version 17 (mentioned in pom.xml)  

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/3a93c93a-5008-418e-b2f5-ff7e1ef1bef4)

Maven - As it simplifies the process of managing project dependencies, including testing dependencies.

JUnit - As it's a library on which the project's tests is depended on. 

Steps

## Cloning a Java App

Within the directory, make a clone of the repository.
mkdir snaatak-P7
cd snaatak
git clone https://github.com/OT-MICROSERVICES/salary-api.git


## Install Java 17 and Maven
As the salary code is Java-based, it is designed to be compatible with Java version 17. It is advisable to install Maven, a crucial tool for managing and building Java projects.
sudo apt update
sudo apt install openjdk-17-jdk
sudo apt install maven

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/4c12c52e-dcba-48bd-aa1f-94a94c42dfdf)

## Add the JUnit dependency in pom.xml file.
<dependency>
	<groupId>junit</groupId>
	<artifactId>junit</artifactId>
	<version>4.12</version>
	<scope>test</scope>
</dependency>

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/52947b33-cef9-42c7-970c-3e39a862f4a7)


## Add maven dependency in pom.xml file.
        <dependency>
		<groupId>org.apache.maven.plugins</groupId>
		<artifactId>maven-compiler-plugin</artifactId>
		<version>3.11.0</version>
		<type>maven-plugin</type>
	</dependency>

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/6bced278-8a21-4959-89ed-7596ead60bd8)

## Revise Surefire Plugin Configuration in pom.xml
Address compatibility issue with JUnit by uncommenting and updating surefire plugin version.

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/76800f61-50ac-4ba7-99f2-13058980cdb2)

## Uncomment the version of surefire plugin and also change the version from 2.17 to 3.0.0

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/090207f8-7a0a-4cd8-ace0-fe47aaecb1c7)

## Run Java Unit Test
    mvn test 

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/7bd0ec27-bffe-48c2-ac85-8f4a93bbfe75)

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/53847503-a743-4fa3-ae59-d42d5ac4d6dc)

## Generate html report with surefire.
    mvn surefire-report:report
This command will generate an html report. To access unit test report, navigate to the target > site > right-click > Open in Browser.


***

## Best Practices for Unit Testing

- Write tests before implementing the corresponding functionality (Test-Driven Development).
- Keep tests simple, isolated, and focused on a single unit.
- Write tests that are easy to understand and maintain.
- Ensure tests are independent and don't rely on external state.
- Use test doubles (mocks, stubs, and fakes) to isolate units from external dependencies.
- Aim for high test coverage, but don't sacrifice test quality for quantity.
- Continuously maintain and update tests as the codebase evolves.

***

## Recommendation/Conclusion

Unit testing is a crucial practice for building high-quality, maintainable software. By following best practices and using appropriate tools, developers can ensure their codebase is robust, reliable, and easy to maintain.

In terms of unit testing tools, the choice often depends on the programming language and the specific needs of the project. However, based on its widespread adoption, excellent features, and strong community support, I recommend considering [JUnit](https://junit.org/junit5/) for Java projects and [pytest](https://docs.pytest.org/en/latest/) for Python projects.

Choose a tool that aligns with your project's requirements and the preferences of your development team. Regardless of the tool you choose, the key is to integrate unit testing seamlessly into your development workflow for optimal results.


***

## Contact Information

|    Name                                   | Email Address                    |
|-------------------------------------------|----------------------------------|
| **[Parasharam Desai](https://github.com/Parasharam-Desai)** | parasharam.desai.snaatak@mygurukulam.co |

***

## Resources and References

| **Source**                                              | **Description**                               |
|---------------------------------------------------------|-----------------------------------------------|
| Advantage & disadvantage                                | [Definition of Unit Testing](https://www.techtarget.com/searchsoftwarequality/definition/unit-testing) |
| what is unit                                             | [What Exactly Is a Unit in Unit Testing?](https://www.blinkingcaret.com/2016/04/27/what-exactly-is-a-unit-in-unit-testing/) |
| what is unit testing                                     | [YouTube Video: What is Unit Testing?](https://www.youtube.com/watch?v=So0gxfFGmLs) |
| Unit Testing Best Practices                              | [Unit Testing Best Practices](https://www.softwaretestinghelp.com/unit-testing-best-practices/) |
| Unit Testing Tools Comparison                            | [Unit Testing Tools Comparison](https://www.softwaretestinghelp.com/unit-testing-tools/) |

