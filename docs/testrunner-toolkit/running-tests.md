---
id: running-tests
title: Running Tests in Testrunner Toolkit
sidebar_label: Running Tests
---

import useBaseUrl from '@docusaurus/useBaseUrl';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

export const Highlight = ({children, color}) => ( <span style={{
      backgroundColor: color,
      borderRadius: '2px',
      color: '#fff',
      padding: '0.2rem',
    }}>{children}</span> );

Before you begin testing we suggest visiting the [Testrunner Toolkit](testrunner-toolkit.md) home page as well as the [configuration](configuration.md) page.

## What You'll Need

Refer to the requirements listed on the [Installation](/testrunner-toolkit/installation) page.

## Create a Configuration

Creating a configuration is a crucial step before you begin testing. Without the `config.yml`, `saucectl` has no idea which framework to use during testing. Please visit the [Configuration](configuration.md) page for detailed information on how to create or edit a configuration.

## Run Your First Test

Run the following command to execute you first test and to ensure Testrunner works properly:


```bash
saucectl run
```

:::note default test location
Unless you specify a test directory, `saucectl` executes tests based on the framework's default test directory. For example with a cypress test, `saucectl` will attempt to locate `cypress.json`, as well as the default `cypress` directory.
 
Consult your desired framework's documentation for more information about the default test locations.
:::

`saucectl` then kicks off a test run and will:
* pull the necessary docker images/layers (e.g. `saucelabs/stt-cypress-mocha-node:v<tag>`)
* copy/mount your test files to the docker container
* run the tests within the docker container
* display the test results in the console

Testrunner Toolkit will then execute the test based on the information in `config.yml`. 

## Test on Sauce Labs

<p><small>supported frameworks: <Highlight color="#25c2a0">cypress</Highlight></small></p>

If you wish to run your tests on Sauce Labs VMs, simply run the following command:

```bash
saucectl run --test-env sauce
```

If you wish to increase your VM concurrency you can also use the flag `--ccy <vm number>`. 

```bash
saucectl run --test-env sauce --ccy 2
```

You can also designate `concurrency` in the `config.yml` like so:

```yaml {2}
sauce:
  concurrency: 3
  region: us-west-1
```

Please note that VM concurrency depends on the suite number rather than the number of `.spec.js |.test.js` files. Plese visit the [CLI Reference](/testrunner-toolkit/saucectl#ccy) for more information regarding command parameters:

> Your concurrency and VM entitlements also depend on your Sauce Labs subscription tier. For more information please visit the [pricing guide](https://saucelabs.com/pricing)

### Cross-Browser Tests

<p><small>supported frameworks: <Highlight color="#25c2a0">cypress</Highlight></small></p>

When you run tests on Sauce Labs VMs you have access to a wide range of OS + browser combinations. In order to test against multiple different browsers, you can indicate the desired combinations in the `suites` > `browser` field:

```yaml {4,11,18}
suites:
  # Chrome
  - name: "Swag Labs Login Chrome"
    browser: "chrome"
    platformName: "Windows 10"
    screenResolution: "1400x1050"
    config:
      testFiles: [ "**/login.*" ]
  # MicrosoftEdge
  - name: "Swag Labs Login MicrosoftEdge"
    browser: "MicrosoftEdge"
    platformName: "Windows 10"
    screenResolution: "1400x1050"
    config:
      testFiles: [ "**/login.*" ]
 # Firefox
   - name: "Swag Labs Login Firefox"
     browser: "firefox"
     platformName: "Windows 10"
     screenResolution: "1400x1050"
     config:
       testFiles: [ "**/login.*" ]
```

> For full examples, please [visit this repository](https://github.com/saucelabs-training/demo-js/tree/master/testrunner-toolkit)

### Using Sauce Connect

If you're running tests on Sauce Labs VMs, but the site under test is protected behind strict network security/policies, you can utilize [Sauce Connect Proxy](/secure-connections/sauce-connect) to circumvent the problem.

You can use the `--tunnel-id` flag with `saucectl` in order to use an existing Sauce Connect tunnel with your test session:

```bash
saucectl run --tunnel-id <tunnel-id>
```

> For more information on how to use the `--tunnel-id` flag, please visit the [CLI Reference](/testrunner-toolkit/saucectl#tunnel-id).

To enable Sauce Connect Proxy in the `config.yml`, use the `tunnel` field:

```yaml {3,4}
sauce:
  concurrency: 3
  tunnel:
    id: sauce-ci-tunnel
  region: us-west-1
```

> For more information regarding how to install, setup, and configure Sauce Connect Proxy, please visit the [Sauce Connect Proxy documentation](/secure-connections/sauce-connect)

### Analyze Test Results in Sauce Labs

After tests complete, Testrunner Toolkit uploads the test assets (logs, test results, and test videos) to your [Sauce Labs account](https://app.saucelabs.com) and displays a job link like so:

```html
https://app.saucelabs.com/tests/<job-number>
```
From this job link you can review, share, and analyze the test results just as you would with any other test framework executed on Sauce Labs.

### Quick demo

<img src={useBaseUrl('img/stt/saucectl-demo.gif')} alt="saucectl Demo" />

## Automation Framework Examples

The examples here show how Pipeline testing can be used. Try them and find your own use cases. 

Every __Testrunner__ image comes with a preconfigured setup that allows you to focus on writing tests instead of tweaking with the configurations. Our initial `testrunner` flavors come either with Cypress, Playwright, or TestCafe as an automation framework. 


Below are example snippets in the following frameworks: [Cypress](https://github.com/cypress-io/cypress), [Playwright](https://playwright.dev/#version=v1.0.1&path=docs%2Fcore-concepts.md&q=browser), and [TestCafe](https://devexpress.github.io/testcafe/documentation/reference/test-api/testcontroller/browser.html).


<Tabs
  defaultValue="cypress"
  values={[
    {label: 'Cypress', value: 'cypress'},
    {label: 'Playwright', value: 'playwright'},
    {label: 'TestCafe', value: 'testcafe'},
  ]}>

<TabItem value="cypress">

<!--https://github.com/saucelabs/saucectl/blob/master/tests/e2e/cypress/integration/example.test.js-->

```js
context('Actions', () => {
		beforeEach(() => {
			cy.visit('https://example.cypress.io/commands/actions')
		})
		it('.type() - type into a DOM element', () => {
			// https://on.cypress.io/type
			cy.get('.action-email')
				.type('fake@email.com').should('have.value', 'fake@email.com')
		})
	})
```

</TabItem>
<TabItem value="playwright">

The Playwright testrunner image also exposes a global `browser` variable that represents Playwright's [`Browser class`](https://playwright.dev/#version=v1.0.2&path=docs%2Fcore-concepts.md&q=browser). In addition to that you also have access to a pre-generated [browser context](https://playwright.dev/#version=v1.0.2&path=docs%2Fcore-concepts.md&q=browser-contexts) via `context` as well as to a [page frame](https://playwright.dev/#version=v1.0.2&path=docs%2Fcore-concepts.md&q=pages-and-frames) via `page`.

<!--https://github.com/saucelabs/saucectl/blob/master/tests/e2e/playwright/example.test.js
-->
```js
describe('saucectl demo test', () => {
	test('should verify title of the page', async () => {
		await page.goto('https://www.saucedemo.com/');
		expect(await page.title()).toBe('Swag Labs');
	});
});
```

</TabItem>
<TabItem value="testcafe">

<!--https://github.com/saucelabs/saucectl/blob/master/tests/e2e/testcafe/example.test.js
-->
```js
import { Selector } from 'testcafe';
fixture `Getting Started`
	.page `http://devexpress.github.io/testcafe/example`

const testName = 'testcafe test'
test(testName, async t => {
	await t
		.typeText('#developer-name', 'devx')
		.click('#submit-button')
		.expect(Selector('#article-header').innerText).eql('Thank you, devx!');
});
```

</TabItem>
</Tabs>
