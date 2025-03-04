---
title: "WebDriver Bidi APIs"
linkTitle: "WebDriver Bidi APIs"
weight: 11
aliases: ["/documentation/ko/webdriver/bidi_apis/"]
---

{{% pageinfo color="warning" %}}
<p class="lead">
   <i class="fas fa-language display-4"></i> 
   Page being translated from 
   English to Korean. Do you speak Korean? Help us to translate
   it by sending us pull requests!
</p>
{{% /pageinfo %}}

In Selenium 4, new Evented APIs were introduced that
allow users to be able to capture events from the
browser as they happen rather than using the
traditional approach of Request/Response that
WebDriver has used for other APIs.

Internally WebDriver will create a WebSocket connection
to the browser for events and commands to be transmitted.

The following list of APIs will be growing as the Selenium
project works through supporting real world use cases. If there
is a missing API, please raise a [feature request](https://github.com/SeleniumHQ/selenium/issues/new?assignees=&labels=&template=feature.md).

## Mutation Observation

Mutation Observation is the ability to capture events via
WebDriver BiDi when there are DOM mutations on a specific
element in the DOM.

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
WebDriver driver = new FirefoxDriver();


HasLogEvents logger = (HasLogEvents) driver;

AtomicReference<DomMutationEvent> seen = new AtomicReference<>();
CountDownLatch latch = new CountDownLatch(1);
logger.onLogEvent(domMutation(mutation -> {
    seen.set(mutation);
    latch.countDown();
}));

driver.get("http://www.google.com");
WebElement span = driver.findElement(By.cssSelector("span"));

((JavascriptExecutor) driver).executeScript("arguments[0].setAttribute('cheese', 'gouda');", span);

assertThat(latch.await(10, SECONDS)).isTrue();
assertThat(seen.get().getAttributeName()).isEqualTo("cheese");
assertThat(seen.get().getCurrentValue()).isEqualTo("gouda");


  {{< /tab >}}
  {{< tab header="Python" >}}
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.wait import WebDriverWait

driver = webdriver.Chrome()
async with driver.log.mutation_events() as event:
    pages.load("dynamic.html")
    driver.find_element(By.ID, "reveal").click()
    WebDriverWait(driver, 5)\
        .until(EC.visibility_of(driver.find_element(By.ID, "revealed")))

assert event["attribute_name"] == "style"
assert event["current_value"] == ""
assert event["old_value"] == "display:none;"

  {{< /tab >}}
  {{< tab header="CSharp" >}}
IWebDriver driver = new FirefoxDriver();
driver.Url = "http://www.google.com";
// Please help with a .NET example
  {{< /tab >}}
  {{< tab header="Ruby" >}}
require 'selenium-webdriver'
driver = Selenium::WebDriver.for :firefox
begin
  driver.on_log_event(:mutation) { |mutation| mutations.push(mutation) }
  driver.navigate.to url_for('dynamic.html')
  driver.find_element(id: 'reveal').click
  wait.until { mutations.any? }
  mutation = mutations.first
  expect(mutation.element).to eq(driver.find_element(id: 'revealed'))
  expect(mutation.attribute_name).to eq('style')
  expect(mutation.current_value).to eq('')
  expect(mutation.old_value).to eq('display:none;')
ensure
  driver.quit
end
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
let {Builder, By} = require('selenium-webdriver');
driver = new Builder().forBrowser('firefox').build();

(async function test(){

    const cdpConnection = await driver.createCDPConnection('page')
    await driver.logMutationEvents(cdpConnection, function (event) {
        assert.strictEqual(event['attribute_name'], 'style')
        assert.strictEqual(event['current_value'], '')
        assert.strictEqual(event['old_value'], 'display:none;')
    })

    await driver.get("https://www.google.com")

    let element = driver.findElement({ id: 'reveal' })
    await element.click()
    let revealed = driver.findElement({ id: 'revealed' })
    await driver.wait(until.elementIsVisible(revealed), 5000)

})();
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
val driver = FirefoxDriver()
driver.get("http://www.google.com")
// Please help us create an example for Kotlin
  {{< /tab >}}
{{< /tabpane >}}
