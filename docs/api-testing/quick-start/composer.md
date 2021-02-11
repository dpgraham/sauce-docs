---
id: composer
title: Test Composer Guide
sidebar_label: Test Composer Guide
description: The API Fortress Composer offers unparalleled flexibility and ease-of-use with everything at your fingertips to build tests in minutes and eliminate many duplicate tasks. Users of all skill levels may begin using the Composer with little or no training to quickly generate sophisticated functional tests. These tests may easily be reused as end-to-end integration tests
---

The API Fortress Composer offers unparalleled flexibility and ease-of-use with everything at your fingertips to build tests in minutes and eliminate many duplicate tasks. Users of all skill levels may begin using the Composer with little or no training to quickly generate sophisticated functional tests. These tests may easily be reused as end-to-end integration tests and load (stress) tests. In turn, load tests may easily be reused as monitors for performance testing.  

:::note Special Note about End-to-End Tests / Integration Tests

Creating a series of independent tests that:

* each hit one endpoint
* and run in a specific order

isn't a proper testing methodology. 

It doesn't allow for optimal testing of how each API interacts with each other. For that reason, the API Fortress composer is very flexible and allows you to create a single "test" that can handle a series of API calls. 

For example __Search__ > __Add to Cart__ > __Checkout__ can and should all be inside of one smart test, and not three separate tests.  

Read the following page to learn more about [Integration / Multistep Testing](/api-testing/intro-to-integration-testing) 
 
:::

## Test Composer Versions

Begin using the Composer by selecting from two versions in terms of views. 

* __Visual__ - The Visual Composer does not require coding expertise, and provides real-time suggestions via predictive text to help you create ideal API tests for your needs. 

* __Code__ - The Code view is for users who are more comfortable working in code rather than a visual UI. 

With either Visual or Code view, easily make calls and add assertions for testing your APIs, and insert variables wherever needed. For more information, visit our [API Testing University](#) to research best practices and find detailed guidance.

[![](https://apifortress.com/doc/wp-content/uploads/2019/06/VisualCodeView-1.jpg)](https://apifortress.com/doc/wp-content/uploads/2019/06/VisualCodeView-1.jpg)

### Visual vs. Code View

[![](https://apifortress.com/doc/wp-content/uploads/2019/06/numberpic.png)](https://apifortress.com/doc/wp-content/uploads/2019/06/numberpic.png)

**(1)** All of the available components can be seen by clicking on Add Request / Assertions.

[![](https://apifortress.com/doc/wp-content/uploads/2019/06/components.png)](https://apifortress.com/doc/wp-content/uploads/2019/06/components.png)

If a component is not valid for the operation you are conducting, it will not be made available to help avoid mistakes. For instance, if you don’t add a POST first, you can not add a POST Body or POST Param. NOTE: Free accounts do not give you access to all available components.  
  
Read descriptions of each component in the Reference section of API Fortress Documentation.

**(2)** This button allows you to easily transform an existing component into another component of the same type.

**(3)** Global Parameters are variables that are available to be used throughout a test. Reference these variables simply by calling it within the test using the convention:  “${VARIABLE}”.  
  
Input Sets are a group of input variables representing a scenario. The test will be executed once for each input set, overriding the variable values into your test.

[![](https://apifortress.com/doc/wp-content/uploads/2019/06/params.png)](https://apifortress.com/doc/wp-content/uploads/2019/06/params.png)

**(4)** HTTP Client - the APIFortress http client is very similar to many other http clients out there. You can make GET/POST/PUT/PATCH/DELETE calls and see their responses.  
A key difference in our HTTP client comes from your ability to generate a test for the API you are calling right from there. If you click the “Generate Test” button, API Fortress will create a test for you based on the API’s behavior and response.

[![](https://apifortress.com/doc/wp-content/uploads/2019/06/Httpclient.png)](https://apifortress.com/doc/wp-content/uploads/2019/06/Httpclient.png)

## Additional Topics

Learn how to create a test quickly [here.](/api-testing/quick-start)