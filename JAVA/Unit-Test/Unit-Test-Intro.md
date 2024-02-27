#  Unit Testing Introduction

| **Author** | **Created On** | **Last Updated** | **Document Version** |
| ---------- | -------------- | ---------------- | -------------------- |
| **Parasharam & Vishal** | 23-01-2024 | 23-01-2024 | V1 |

***


# Table of Contents

* [Introduction](#introduction)
* [What is Unit Testing?](#what-is-unit-testing)
* [Why is Unit Testing Important?](#why-is-unit-testing-important)
* [Unit Testing Advantages](#unit-testing-advantages)
* [Unit Testing Disadvantages](#unit-testing-disadvantages)
* [Best Practices for Unit Testing](#best-practices-for-unit-testing)
* [Contact Information](#contact-information)
* [Resources and References](#resources-and-references)

***
# Introduction

Welcome to the documentation on Unit and Unit Testing in Software Development. This guide aims to provide a comprehensive understanding of the concepts surrounding unit testing within a software application.

***

# What is Unit Testing?

A **unit** refers to the smallest testable part of a software program, such as a function or method. 

A **module,** which is nothing but a single unit of software, can also be considered a unit. The goal of unit testing is to test each unit, including modules, in isolation to ensure they work as intended before integrating them into the larger system.

**Unit testing** is a type of software testing where individual units or components of a software application are tested to ensure they meet their design and behavior requirements. These units can be functions, methods, or classes, and they are tested in isolation, without any dependencies on external components.

<img width="560" length="300" alt="ut" src="https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/cdfe8356-c6ea-407f-800a-01063a1d21b4">


***
## Types of Unit Testing

| Manual Unit Testing                                                                                               | Automated Unit Testing                                                                                                  |
|-------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Manual testing involves human testers creating test cases, testing software without automation tools, and providing final reports.                                               | Automated testing utilizes tools for testing, making it faster and more efficient compared to manual testing.            |
| Testers manually execute test cases and observe software behavior, potentially allowing for human errors.         | Automation tools execute test cases automatically, reducing the chance of human errors and providing consistent results. |
| Manual testing is slower due to human involvement and can be time-consuming.                                      | Automated testing is faster since it's performed with automation tools, saving time and resources.                        |
| It's suitable for scenarios where human judgment and intuition are required, such as exploratory testing.         | Best suited for repetitive tasks, regression testing, and scenarios where rapid testing is needed, ensuring reliability. |


***

# Why is Unit Testing important?

Unit testing offers several benefits, including:

| **Benefits**                         | **Description**                                                                                          |
|--------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Early bug detection**              | Testing individual units helps identify issues early in the development cycle, reducing overall bug fixing costs.                                                     |
| **Improved code quality**            | Unit tests ensure that each unit functions as expected, leading to a more robust and reliable codebase.                                                             |
| **Faster development**               | Unit tests provide a safety net for developers, allowing them to refactor and improve the codebase with confidence.                                                   |
| **Better collaboration**             | Unit tests help developers understand the expected behavior of individual units, making it easier for teams to collaborate and maintain the codebase. |

***

# Unit Testing Advantages

There are many advantages to unit testing, including the following:

| Point                                                  | Explanation                                                       |
|--------------------------------------------------------|-------------------------------------------------------------------|
| **Early problem identification**                           | Identifying issues early reduces the likelihood of compound errors. |
| **Cost-effectiveness of early fixing**                     | Addressing problems in the early stages of development is usually less expensive than fixing them later. |
| **Simplified debugging process**                           | Early detection of issues simplifies the debugging process.        |
| **Agile codebase modifications**                           | Developers can swiftly make changes to the codebase as needed.     |
| **Code reuse and migration**                               | Enables developers to reuse code and migrate it to new projects.    |

***

# Unit Testing Disadvantages

While unit testing is integral to any software development and testing strategy, there are some aspects to be aware of. Disadvantages to unit testing include the following:

| Point                                                         | Explanation                                            |
|---------------------------------------------------------------|--------------------------------------------------------|
| **Tests may not uncover every bug**                                | Despite thorough testing, it's possible for some bugs to remain undetected.                    |
| **Limited scope of unit tests**                                    | Unit tests focus on specific sets of data and functionality, not integration aspects.           |
| **Increased test code complexity**                                 | Writing tests may require more lines of code compared to the actual code being tested.          |
| **Learning curve for implementing unit testing**                   | Developers might need to acquire new skills, such as using specific automated testing tools.    |

***

# Best Practices for Unit Testing

| Point                                                         | Explanation                                                                                   |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| **Write tests before implementing functionality (TDD)**           | Following Test-Driven Development (TDD) methodology involves writing tests prior to coding.   |
| **Keep tests simple and isolated**                                 | Tests should focus on a single unit and be kept simple for better readability and debugging.   |
| **Write tests that are easy to understand and maintain**          | Ensure test cases are written in a clear and understandable manner to facilitate maintenance.  |
| **Ensure tests are independent and stateless**                    | Tests should not rely on external state to maintain consistency and independence.             |
| **Use test doubles for isolating units from dependencies**        | Employ mocks, stubs, and fakes to isolate units under test from external dependencies.        |
| **Aim for high test coverage without sacrificing quality**        | Strive for comprehensive test coverage while ensuring tests are meaningful and effective.     |
| **Continuously maintain and update tests as codebase evolves**    | Regularly update and refactor tests to align with changes in the codebase and requirements.    |

***

# Contact Information

|    Name                                   | Email Address                    |
|-------------------------------------------|----------------------------------|
| **[Parasharam Desai](https://github.com/Parasharam-Desai)** | parasharam.desai.snaatak@mygurukulam.co |

***

# Resources and References

| **Description**                                           |  **Source**                             |
|---------------------------------------------------------|-----------------------------------------------|
| What Exactly Is a Unit in Unit Testing?                    | [Link](https://www.blinkingcaret.com/2016/04/27/what-exactly-is-a-unit-in-unit-testing/) |
| YouTube Video: What is Unit Testing?                       | [Link](https://www.youtube.com/watch?v=So0gxfFGmLs) |
| Advantage & Disadvantage Of Unit Testing.                  | [Link](https://www.techtarget.com/searchsoftwarequality/definition/unit-testing) |
| Unit Testing Best Practices.                              | [Link](https://www.softwaretestinghelp.com/unit-testing-best-practices/) |
| Types of Unit testing. | [Link](https://www.geeksforgeeks.org/software-engineering-differences-between-manual-and-automation-testing/) |
