# Unit Testing in JAVA Base Applications

| **Author** | **Created On** | **Last Updated** | **Document Version** |
| ---------- | -------------- | ---------------- | -------------------- |
| **Parasharam Desai** | 23-01-2024 | 23-01-2024 | V1 |

***


# Table of Contents

1. [Introduction](#introduction)
2. [What is Unit Testing?](#what-is-unit-testing)
3. [Different Tools for Unit Testing](#different-tools-for-unit-testing)
4. [Proof of Concept (POC) for Java Base Application](#proof-of-concept-poc-for-java-base-application)
5. [Recommendation/Conclusion](#recommendation-conclusion)
6. [Contact Information](#contact-information)
7. [Resources and References](#resources-and-references)

***
# Introduction

Welcome to the documentation on Unit and Unit Testing in Software Development. This guide aims to provide a comprehensive understanding of the concepts surrounding unit testing within a software application.

***
# What is Unit Testing?

A **unit** in software development refers to the smallest testable part, such as a function or method. Additionally, 
A **module**, which is essentially a single unit of software, can also be considered a unit. The primary objective of unit testing is to test each of these units, including modules, in isolation to ensure they function as intended before integrating them into the larger system.

**Unit testing** is a specific type of software testing where individual units or components of a software application, like functions, methods, or classes, are tested independently to verify that they meet their design and behavior requirements. These tests are conducted without any dependencies on external components.

![Unit Testing](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/cdfe8356-c6ea-407f-800a-01063a1d21b4)

# More on Unit Testing:

For a comprehensive understanding of unit testing, including its importance, advantages, disadvantages, and best practices, refer to our detailed documentation where we cover the following points:

- Why is Unit Testing Important?
- Unit Testing Advantages
- Unit Testing Disadvantages
- Best Practices for Unit Testing

**Documentation Link:** [Detailed Unit Testing Documentation](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/03-%20Java%20CI%20checks/Intro-of-Unit-Testing.md)

***
# Different Tools for Unit Testing

There are various unit testing frameworks available for different programming languages. Some popular ones include:

| **Tool Name** | **Purpose** | **Programming Language** | **Testing Types Supported** | **Ease of Learning** | **Integration with IDEs** | **Parallel Execution** | **Data-Driven Testing** | **Reports and Documentation** | **Community Support** | **Pros** | **Cons** | **Ideal Scenarios** |
|---------------|-------------|---------------------------|-----------------------------|-----------------------|---------------------------|------------------------|-------------------------|-----------------------------|------------------------|----------|----------|---------------------|
| JUnit         | Unit testing | Java | Unit testing, regression testing | Easy | Well-supported in popular IDEs like IntelliJ, Eclipse | Limited support in JUnit 4, better in JUnit 5 | Limited support | Provides basic reporting; additional tools may be needed for detailed reports | Large community | Standard in Java development | Limited support for parallel execution | Unit testing and regression testing |
| TestNG        | Versatile testing | Java | Unit testing, functional testing, end-to-end testing, integration testing | Moderate to easy | Excellent integration with popular IDEs like Eclipse, IntelliJ | Yes | Yes | Extensive reporting features, including HTML reports and custom listeners | Active community | Versatile, supports various testing types | Learning curve for beginners, can be verbose | Versatile testing needs including unit, functional, and integration testing |
| Mockito       | Mocking for unit testing | Java | Unit testing | Moderate | Integrates with popular IDEs for Java development | No direct support; can be achieved using other tools or frameworks | Limited support for parameterized tests | Limited; primarily focused on verification errors | Active community | Powerful mocking capabilities, simple syntax | Limited testing scope, not a complete testing framework | Unit testing with a focus on behavior verification |

***

# Proof of Concept (POC) for Java Base Application

For a detailed proof of concept (POC) related to Java unit testing, please refer to [Unit Testing POC](https://github.com/avengers-p7/Documentation/blob/main/Application_CI/Design/03-%20Java%20CI%20checks/Unit%20Testing/POC.md).

---

# Unit Testing in Other Languages

| **Language**         | **Documentation**                                     |
|----------------------|-------------------------------------------------------|
| **Python**           | [Python Unit Testing POC](./Python_Unit_Testing_POC.md) - Comparison of unit testing tools and a detailed POC for Python. |
| **Golang**           | [Golang Unit Testing POC](./Golang_Unit_Testing_POC.md) - Comparison of unit testing tools and a detailed POC for Golang. |

***
# Recommendation/Conclusion

In conclusion, JUnit is the recommended choice for Java unit testing due to its:

* Standardization: Widely accepted in Java development.

* Integration: Seamless integration with popular IDEs.

* Ease of Learning: Simple syntax for quick adoption.

* Community Support: Large and active community for ongoing assistance.

* Parallel Execution: Improved support for optimizing test suite performance.

* Compatibility: Works well with Maven and Gradle for versatile project setups.

By choosing JUnit, teams can ensure efficient, reliable unit testing, leading to higher code quality and faster development cycles.

***

# Contact Information

|    Name                                   | Email Address                    |
|-------------------------------------------|----------------------------------|
| **[Parasharam Desai](https://github.com/Parasharam-Desai)** | parasharam.desai.snaatak@mygurukulam.co |

***

# Resources and References

|       **Description**                                   |           **References**                    |
|---------------------------------------------------------|-----------------------------------------------|
| What Exactly Is a Unit in Unit Testing?      | [Link](https://www.blinkingcaret.com/2016/04/27/what-exactly-is-a-unit-in-unit-testing/) |
| YouTube Video: What is Unit Testing?                  | [Link](https://www.youtube.com/watch?v=So0gxfFGmLs) |
| Java Unit Testing Frameworks.           | [Link](https://www.scalosoft.com/blog/top-10-java-unit-testing-frameworks-for-2023/) |
