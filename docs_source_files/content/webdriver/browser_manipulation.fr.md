---
title: "Manipulation du navigateur"
weight: 3
---

{{% notice info %}}
<i class="fas fa-language"></i> Page being translated from
English to French. Do you speak French? Help us to translate
it by sending us pull requests!
{{% /notice %}}

<!-- #codeExamples -->
<!-- Remember to cover profile and extensions here -->


## Ruby

Ruby is not installed by default on Windows. Download the latest
[version](//rubyinstaller.org/downloads) and run the installer. You can
leave all settings at default values, except at the
_Installation Destination and Optional Tasks_ screen check
_Add Ruby executables to your PATH_ checkbox. To drive any browser, you have
to install `selenium-webdriver` Ruby gem. To install it, open command prompt
and type this:

```shell
gem install selenium-webdriver
```

Or, if you use [Bundler](//bundler.io), add this line to your application's
Gemfile:

```ruby
gem "selenium-webdriver"
```

And then execute the following command in prompt:

```shell
bundle install
```


## Internet Explorer

Internet Explorer is installed by default on Windows, so no installation is
needed. To drive Internet Explorer on Windows, you have to download the latest
[Internet Explorer Driver](https://selenium.dev/downloads/) and put the file
into a folder that is in `PATH`. To find out which directories are in `PATH`,
type `echo %PATH%` in command prompt.

```bat
$ echo %PATH%
C:\Ruby200\bin;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem
```

`C:\Ruby200\bin` looks like a good place. Unzip `IEDriverServer` file and
move `IEDriverServer.exe` there.

This should open a new Internet Explorer window:

```ruby
require "selenium-webdriver"
driver = Selenium::WebDriver.for :internet_explorer
```

## Browser navigation

### Navigate to

The first thing you will want to do after launching a browser is to
open your website. This can be achieved in a single line:

{{< code-tab >}}
  {{< code-panel language="java" >}}
//Convenient
driver.get("https://selenium.dev");

//Longer way
driver.navigate().to("https://selenium.dev");
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
driver.get("https://selenium.dev")
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
driver.Navigate().GoToUrl(@"https://selenium.dev");
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
# Convenient way
driver.get 'https://selenium.dev'

# Longer Way
driver.navigate.to 'https://selenium.dev'
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
await driver.get('https://selenium.dev');
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
//Convenient
driver.get("https://selenium.dev")

//Longer way
driver.navigate().to("https://selenium.dev")
  {{< / code-panel >}}
{{< / code-tab >}}

### Get current URL

You can read the current URL from the browser's address bar using:

{{< code-tab >}}
  {{< code-panel language="java" >}}driver.getCurrentUrl();{{< / code-panel >}}
  {{< code-panel language="python" >}}driver.current_url{{< / code-panel >}}
  {{< code-panel language="csharp" >}}driver.Url;{{< / code-panel >}}
  {{< code-panel language="ruby" >}}driver.current_url{{< / code-panel >}}
  {{< code-panel language="javascript" >}}await driver.getCurrentUrl();{{< / code-panel >}}
  {{< code-panel language="kotlin" >}}driver.currentUrl{{< / code-panel >}}
{{< / code-tab >}}

### Back

Pressing the browser's back button:

{{< code-tab >}}
  {{< code-panel language="java" >}}driver.navigate().back();{{< / code-panel >}}
  {{< code-panel language="python" >}}driver.back(){{< / code-panel >}}
  {{< code-panel language="csharp" >}}driver.Navigate().Back();{{< / code-panel >}}
  {{< code-panel language="ruby" >}}driver.navigate.back{{< / code-panel >}}
  {{< code-panel language="javascript" >}}await driver.navigate().back();{{< / code-panel >}}
  {{< code-panel language="kotlin" >}}driver.navigate().back() {{< / code-panel >}}
{{< / code-tab >}}


### Forward
Pressing the browser's forward button:

{{< code-tab >}}
  {{< code-panel language="java" >}}driver.navigate().forward();{{< / code-panel >}}
  {{< code-panel language="python" >}}driver.forward(){{< / code-panel >}}
  {{< code-panel language="csharp" >}}driver.Navigate().Forward();{{< / code-panel >}}
  {{< code-panel language="ruby" >}}driver.navigate.forward{{< / code-panel >}}
  {{< code-panel language="javascript" >}}await driver.navigate().forward();{{< / code-panel >}}
  {{< code-panel language="kotlin" >}}driver.navigate().forward(){{< / code-panel >}}
{{< / code-tab >}}

### Refresh

Refresh the current page:

{{< code-tab >}}
  {{< code-panel language="java" >}}driver.navigate().refresh();{{< / code-panel >}}
  {{< code-panel language="python" >}}driver.refresh(){{< / code-panel >}}
  {{< code-panel language="csharp" >}}driver.Navigate().Refresh();{{< / code-panel >}}
  {{< code-panel language="ruby" >}}driver.navigate.refresh{{< / code-panel >}}
  {{< code-panel language="javascript" >}}await driver.navigate().refresh();{{< / code-panel >}}
  {{< code-panel language="kotlin" >}}driver.navigate().refresh(){{< / code-panel >}}
{{< / code-tab >}}

### Get title

You can read the current page title from the browser:

{{< code-tab >}}
  {{< code-panel language="java" >}}driver.getTitle();{{< / code-panel >}}
  {{< code-panel language="python" >}}driver.title{{< / code-panel >}}
  {{< code-panel language="csharp" >}}driver.Title;{{< / code-panel >}}
  {{< code-panel language="ruby" >}}driver.title{{< / code-panel >}}
  {{< code-panel language="javascript" >}}await driver.getTitle();{{< / code-panel >}}
  {{< code-panel language="kotlin" >}}driver.title{{< / code-panel >}}
{{< / code-tab >}}


## Windows and tabs
WebDriver doesn't make the distinction between windows and tabs. If
your site opens a new tab or window, Selenium will let you work with it
using a window handle.  Each window has a unique identifier which remains
persistent in a single session. You can get the window handle of the
current window by using:

{{< code-tab >}}
  {{< code-panel language="java" >}}driver.getWindowHandle();{{< / code-panel >}}
  {{< code-panel language="python" >}}driver.current_window_handle{{< / code-panel >}}
  {{< code-panel language="csharp" >}}driver.CurrentWindowHandle;{{< / code-panel >}}
  {{< code-panel language="ruby" >}}driver.window_handle{{< / code-panel >}}
  {{< code-panel language="javascript" >}}await driver.getWindowHandle();{{< / code-panel >}}
  {{< code-panel language="kotlin" >}}driver.windowHandle{{< / code-panel >}}
{{< / code-tab >}}

### Switching windows or tabs

Clicking a link which opens in a
<a href="https://seleniumhq.github.io" target="_blank"> new window</a>
will focus the new window or tab on screen, but WebDriver will not know which
window the Operating System considers active.  To work with the new window
you will need to switch to it. If you have only two tabs or windows open,
and you know which window you start with, by the process of elimination
you can loop over both windows or tabs that WebDriver can see, and switch
to the one which is not the original.

However, Selenium 4 provides a new api
<a href="https://selenium.dev/documentation/fr/webdriver/browser_manipulation/#create-new-window-or-new-tab-and-switch"> NewWindow </a>
which creates a new tab (or) new window and automatically switches to it.

{{< code-tab >}}
  {{< code-panel language="java" >}}
//Store the ID of the original window
String originalWindow = driver.getWindowHandle();

//Check we don't have other windows open already
assert driver.getWindowHandles().size() == 1;

//Click the link which opens in a new window
driver.findElement(By.linkText("new window")).click();

//Wait for the new window or tab
wait.until(numberOfWindowsToBe(2));

//Loop through until we find a new window handle
for (String windowHandle : driver.getWindowHandles()) {
    if(!originalWindow.contentEquals(windowHandle)) {
        driver.switchTo().window(windowHandle);
        break;
    }
}

//Wait for the new tab to finish loading content
wait.until(titleIs("Selenium documentation"));
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
from selenium import webdriver
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Start the driver
with webdriver.Firefox() as driver:
    # Open URL
    driver.get("https://seleniumhq.github.io")

    # Setup wait for later
    wait = WebDriverWait(driver, 10)

    # Store the ID of the original window
    original_window = driver.current_window_handle

    # Check we don't have other windows open already
    assert len(driver.window_handles) == 1

    # Click the link which opens in a new window
    driver.find_element(By.LINK_TEXT, "new window").click()

    # Wait for the new window or tab
    wait.until(EC.number_of_windows_to_be(2))

    # Loop through until we find a new window handle
    for window_handle in driver.window_handles:
        if window_handle != original_window:
            driver.switch_to.window(window_handle)
            break

    # Wait for the new tab to finish loading content
    wait.until(EC.title_is("SeleniumHQ Browser Automation"))
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
//Store the ID of the original window
string originalWindow = driver.CurrentWindowHandle;

//Check we don't have other windows open already
Assert.AreEqual(driver.WindowHandles.Count, 1);

//Click the link which opens in a new window
driver.FindElement(By.LinkText("new window")).Click();

//Wait for the new window or tab
wait.Until(wd => wd.WindowHandles.Count == 2);

//Loop through until we find a new window handle
foreach(string window in driver.WindowHandles)
{
    if(originalWindow != window)
    {
        driver.SwitchTo().Window(window);
        break;
    }
}
//Wait for the new tab to finish loading content
wait.Until(wd => wd.Title == "Selenium documentation");
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
#Store the ID of the original window
original_window = driver.window_handle

#Check we don't have other windows open already
assert(driver.window_handles.length == 1, 'Expected one window')

#Click the link which opens in a new window
driver.find_element(link: 'new window').click

#Wait for the new window or tab
wait.until { driver.window_handles.length == 2 }

#Loop through until we find a new window handle
driver.window_handles.each do |handle|
    if handle != original_window
        driver.switch_to.window handle
        break
    end
end

#Wait for the new tab to finish loading content
wait.until { driver.title == 'Selenium documentation'}
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
//Store the ID of the original window
const originalWindow = await driver.getWindowHandle();

//Check we don't have other windows open already
assert((await driver.getAllWindowHandles()).length === 1);

//Click the link which opens in a new window
await driver.findElement(By.linkText('new window')).click();

//Wait for the new window or tab
await driver.wait(
    async () => (await driver.getAllWindowHandles()).length === 2,
    10000
  );

//Loop through until we find a new window handle
const windows = await driver.getAllWindowHandles();
windows.forEach(async handle => {
  if (handle !== originalWindow) {
    await driver.switchTo().window(handle);
  }
});

//Wait for the new tab to finish loading content
await driver.wait(until.titleIs('Selenium documentation'), 10000);
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
//Store the ID of the original window
val originalWindow = driver.getWindowHandle()

//Check we don't have other windows open already
assert(driver.getWindowHandles().size() === 1)

//Click the link which opens in a new window
driver.findElement(By.linkText("new window")).click()

//Wait for the new window or tab
wait.until(numberOfWindowsToBe(2))

//Loop through until we find a new window handle
for (windowHandle in driver.getWindowHandles()) {
    if (!originalWindow.contentEquals(windowHandle)) {
        driver.switchTo().window(windowHandle)
        break
    }
}

//Wait for the new tab to finish loading content
wait.until(titleIs("Selenium documentation"))

  {{< / code-panel >}}
{{< / code-tab >}}

### Create new window (or) new tab and switch
Creates a new window (or) tab and will focus the new window or tab on screen.
You don't need to switch to work with the new window (or) tab. If you have more than two windows
(or) tabs opened other than the new window, you can loop over both windows or tabs that WebDriver can see,
and switch to the one which is not the original.

__Note: This feature works with Selenium 4 and later versions.__

{{< code-tab >}}
  {{< code-panel language="java" >}}
// Opens a new tab and switches to new tab
driver.switchTo().newWindow(WindowType.TAB);

// Opens a new window and switches to new window
driver.switchTo().newWindow(WindowType.WINDOW);
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
# Opens a new tab and switches to new tab
driver.switch_to.new_window('tab')

# Opens a new window and switches to new window
driver.switch_to.new_window('window')
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
// Opens a new tab and switches to new tab
driver.SwitchTo().NewWindow(WindowType.Tab)

// Opens a new window and switches to new window
driver.SwitchTo().NewWindow(WindowType.Window)
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
# Note: The new_window in ruby only opens a new tab (or) Window and will not switch automatically
# The user has to switch to new tab (or) new window

# Opens a new tab and switches to new tab
driver.manage.new_window(:tab)

# Opens a new window and switches to new window
driver.manage.new_window(:window)
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
// Opens a new tab and switches to new tab
await driver.switchTo().newWindow('tab');

// Opens a new window and switches to new window
await driver.switchTo().newWindow('window');

  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
// Opens a new tab and switches to new tab
driver.switchTo().newWindow(WindowType.TAB)

// Opens a new window and switches to new window
driver.switchTo().newWindow(WindowType.WINDOW)
  {{< / code-panel >}}
{{< / code-tab >}}

### Closing a window or tab

When you are finished with a window or tab _and_ it is not the
last window or tab open in your browser, you should close it and switch
back to the window you were using previously.  Assuming you followed the
code sample in the previous section you will have the previous window
handle stored in a variable. Put this together and you will get:

{{< code-tab >}}
  {{< code-panel language="java" >}}
//Close the tab or window
driver.close();

//Switch back to the old tab or window
driver.switchTo().window(originalWindow);
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
#Close the tab or window
driver.close()

#Switch back to the old tab or window
driver.switch_to.window(original_window)
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
//Close the tab or window
driver.Close();

//Switch back to the old tab or window
driver.SwitchTo().Window(originalWindow);
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
#Close the tab or window
driver.close

#Switch back to the old tab or window
driver.switch_to.window original_window
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
//Close the tab or window
await driver.close();

//Switch back to the old tab or window
await driver.switchTo().window(originalWindow);
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
//Close the tab or window
driver.close()

//Switch back to the old tab or window
driver.switchTo().window(originalWindow)

  {{< / code-panel >}}
{{< / code-tab >}}

Forgetting to switch back to another window handle after closing a
window will leave WebDriver executing on the now closed page, and will
trigger a **No Such Window Exception**. You must switch
back to a valid window handle in order to continue execution.

### Quitting the browser at the end of a session

When you are finished with the browser session you should call quit,
instead of close:

{{< code-tab >}}
  {{< code-panel language="java" >}}driver.quit();{{< / code-panel >}}
  {{< code-panel language="python" >}}driver.quit(){{< / code-panel >}}
  {{< code-panel language="csharp" >}}driver.Quit();{{< / code-panel >}}
  {{< code-panel language="ruby" >}}driver.quit{{< / code-panel >}}
  {{< code-panel language="javascript" >}}await driver.quit();{{< / code-panel >}}
  {{< code-panel language="kotlin" >}}driver.quit(){{< / code-panel >}}
{{< / code-tab >}}

* Quit will:
  * Close all the windows and tabs associated with that WebDriver
  session
  * The browser process
  * The background driver process
  * Notify Selenium Grid that the browser is no longer in use so it can
   be used by another session (if you are using Selenium Grid)

Failure to call quit will leave extra background processes and ports
running on your machine which could cause you problems later.

Some test frameworks offer methods and annotations which you can hook
into to tear down at the end of a test.

{{< code-tab >}}
  {{< code-panel language="java" >}}
/**
 * Example using JUnit
 * https://junit.org/junit5/docs/current/api/org/junit/jupiter/api/AfterAll.html
 */
@AfterAll
public static void tearDown() {
    driver.quit();
}
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
# unittest teardown
# https://docs.python.org/3/library/unittest.html?highlight=teardown#unittest.TestCase.tearDown
def tearDown(self):
    self.driver.quit()
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
/*
    Example using Visual Studio's UnitTesting
    https://msdn.microsoft.com/en-us/library/microsoft.visualstudio.testtools.unittesting.aspx
*/
[TestCleanup]
public void TearDown()
{
    driver.Quit();
}
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
# UnitTest Teardown
# https://www.rubydoc.info/github/test-unit/test-unit/Test/Unit/TestCase
def teardown
    @driver.quit
end
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
/**
 * Example using Mocha
 * https://mochajs.org/#hooks
 */
after('Tear down', async function () {
  await driver.quit();
});
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}

/**
 * Example using JUnit
 * https://junit.org/junit5/docs/current/api/org/junit/jupiter/api/AfterAll.html
 */
@AfterAll
fun tearDown() {
    driver.quit()
}
  {{< / code-panel >}}
{{< / code-tab >}}

If not running WebDriver in a test context, you may consider using
`try  / finally` which is offered by most languages so that an exception
will still clean up the WebDriver session.

{{< code-tab >}}
  {{< code-panel language="java" >}}
try {
    //WebDriver code here...
} finally {
    driver.quit();
}
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
try:
    #WebDriver code here...
finally:
    driver.quit()
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
try {
    //WebDriver code here...
} finally {
    driver.Quit();
}
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
begin
    #WebDriver code here...
ensure
    driver.quit
end
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
try {
    //WebDriver code here...
} finally {
    await driver.quit();
}
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
try {
    //WebDriver code here...
} finally {
    driver.quit()
}
  {{< / code-panel >}}
{{< / code-tab >}}

Python's WebDriver now supports the python context manager,
which when using the with keyword can automatically quit the driver at
the end of execution.

```python
with webdriver.Firefox() as driver:
  # WebDriver code here...

# WebDriver will automatically quit after indentation
```

## Frames and Iframes
Frames are a now deprecated means of building a site layout from
multiple documents on the same domain. You are unlikely to work with
them unless you are working with an pre HTML5 webapp.  Iframes allow
the insertion of a document from an entirely different domain, and are
still commonly used.

If you need to work with frames or iframes, WebDriver allows you to
work with them in the same way. Consider a button within an iframe.
If we inspect the element using the browser development tools, we might
see the following:

```html
<div id="modal">
  <iframe id="buttonframe" name="myframe"  src="https://seleniumhq.github.io">
   <button>Click here</button>
 </iframe>
</div>
```

If it wasn't for the iframe we would expect to click on the button
using something like:

{{< code-tab >}}
  {{< code-panel language="java" >}}
//This won't work
driver.findElement(By.tagName("button")).click();
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
# This Wont work
driver.find_element(By.TAG_NAME, 'button').click()
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
//This won't work
driver.FindElement(By.TagName("button")).Click();
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
# This won't work
driver.find_element(:tag_name,'button').click
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
// This won't work
await driver.findElement(By.css('button')).click();
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
//This won't work
driver.findElement(By.tagName("button")).click()
  {{< / code-panel >}}
{{< / code-tab >}}

However, if there are no buttons outside of the iframe, you might
instead get a _no such element_ error. This happens because Selenium is
only aware of the elements in the top level document. To interact with
the button, we will need to first switch to the frame, in a similar way
to how we switch windows. WebDriver offers three ways of switching to
a frame.

### Using a WebElement

Switching using a WebElement is the most flexible option. You can
find the frame using your preferred selector and switch to it.

{{< code-tab >}}
  {{< code-panel language="java" >}}
//Store the web element
WebElement iframe = driver.findElement(By.cssSelector("#modal>iframe"));

//Switch to the frame
driver.switchTo().frame(iframe);

//Now we can click the button
driver.findElement(By.tagName("button")).click();
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
# Store iframe web element
iframe = driver.find_element(By.CSS_SELECTOR, "#modal > iframe")

# switch to selected iframe
driver.switch_to.frame(iframe)

# Now click on button
driver.find_element(By.TAG_NAME, 'button').click()
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
//Store the web element
IWebElement iframe = driver.FindElement(By.CssSelector("#modal>iframe"));

//Switch to the frame
driver.SwitchTo().Frame(iframe);

//Now we can click the button
driver.FindElement(By.TagName("button")).Click();
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
# Store iframe web element
iframe = driver.find_element(:css,'#modal > iframe')

# Switch to the frame
driver.switch_to.frame iframe

# Now, Click on the button
driver.find_element(:tag_name,'button').click
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
// Store the web element
const iframe = driver.findElement(By.css('#modal > iframe'));

// Switch to the frame
await driver.switchTo().frame(iframe);

// Now we can click the button
await driver.findElement(By.css('button')).click();
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
//Store the web element
val iframe = driver.findElement(By.cssSelector("#modal>iframe"))

//Switch to the frame
driver.switchTo().frame(iframe)

//Now we can click the button
driver.findElement(By.tagName("button")).click()
  {{< / code-panel >}}
{{< / code-tab >}}

### Using a name or ID
If your frame or iframe has an id or name attribute, this can be used
instead.  If the name or ID is not unique on the page, then the first
one found will be switched to.

{{< code-tab >}}
  {{< code-panel language="java" >}}
//Using the ID
driver.switchTo().frame("buttonframe");

//Or using the name instead
driver.switchTo().frame("myframe");

//Now we can click the button
driver.findElement(By.tagName("button")).click();
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
# Switch frame by id
driver.switch_to.frame('buttonframe')

# Now, Click on the button
driver.find_element(By.TAG_NAME, 'button').click()
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
//Using the ID
driver.SwitchTo().Frame("buttonframe");

//Or using the name instead
driver.SwitchTo().Frame("myframe");

//Now we can click the button
driver.FindElement(By.TagName("button")).Click();
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
# Switch by ID
driver.switch_to.frame 'buttonframe'

# Now, Click on the button
driver.find_element(:tag_name,'button').click
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
// Using the ID
await driver.switchTo().frame('buttonframe');

// Or using the name instead
await driver.switchTo().frame('myframe');

// Now we can click the button
await driver.findElement(By.css('button')).click();
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
//Using the ID
driver.switchTo().frame("buttonframe")

//Or using the name instead
driver.switchTo().frame("myframe")

//Now we can click the button
driver.findElement(By.tagName("button")).click()
  {{< / code-panel >}}
{{< / code-tab >}}

### Using an index

It is also possible to use the index of the frame, such as can be
queried using _window.frames_ in JavaScript.

{{< code-tab >}}
  {{< code-panel language="java" >}}
// Switches to the second frame
driver.switchTo().frame(1);
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
# Switch to the second frame
driver.switch_to.frame(1)
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
// Switches to the second frame
driver.SwitchTo().Frame(1);
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
# switching to second iframe based on index
iframe = driver.find_elements_by_tag_name('iframe')[1]

# switch to selected iframe
driver.switch_to.frame(iframe)
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
// Switches to the second frame
await driver.switchTo().frame(1);
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
// Switches to the second frame
driver.switchTo().frame(1)
  {{< / code-panel >}}
{{< / code-tab >}}


### Leaving a frame

To leave an iframe or frameset, switch back to the default content
like so:

{{< code-tab >}}
  {{< code-panel language="java" >}}
// Return to the top level
driver.switchTo().defaultContent();
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
# switch back to default content
driver.switch_to.default_content()
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
// Return to the top level
driver.SwitchTo().DefaultContent();
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
# Return to the top level
driver.switch_to.default_content
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
// Return to the top level
await driver.switchTo().defaultContent();
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
// Return to the top level
driver.switchTo().defaultContent()
  {{< / code-panel >}}
{{< / code-tab >}}

## Window management
Screen resolution can impact how your web application renders, so
WebDriver provides mechanisms for moving and resizing the browser
window.

### Get window size
Fetches the size of the browser window in pixels.

{{< code-tab >}}
  {{< code-panel language="java" >}}
//Access each dimension individually
int width = driver.manage().window().getSize().getWidth();
int height = driver.manage().window().getSize().getHeight();

//Or store the dimensions and query them later
Dimension size = driver.manage().window().getSize();
int width1 = size.getWidth();
int height1 = size.getHeight();
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
# Access each dimension individually
width = driver.get_window_size().get("width")
height = driver.get_window_size().get("height")

# Or store the dimensions and query them later
size = driver.get_window_size()
width1 = size.get("width")
height1 = size.get("height")
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
//Access each dimension individually
int width = driver.Manage().Window.Size.Width;
int height = driver.Manage().Window.Size.Height;

//Or store the dimensions and query them later
System.Drawing.Size size = driver.Manage().Window.Size;
int width1 = size.Width;
int height1 = size.Height;
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
# Access each dimension individually
width = driver.manage.window.size.width
height = driver.manage.window.size.height

# Or store the dimensions and query them later
size = driver.manage.window.size
width1 = size.width
height1 = size.height
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
// Access each dimension individually
const { width, height } = await driver.manage().window().getRect();

// Or store the dimensions and query them later
const rect = await driver.manage().window().getRect();
const width1 = rect.width;
const height1 = rect.height;
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
//Access each dimension individually
val width = driver.manage().window().size.width
val height = driver.manage().window().size.height

//Or store the dimensions and query them later
val size = driver.manage().window().size
val width1 = size.width
val height1 = size.height
  {{< / code-panel >}}
{{< / code-tab >}}

### Set window size

Restores the window and sets the window size.
{{< code-tab >}}
  {{< code-panel language="java" >}}driver.manage().window().setSize(new Dimension(1024, 768));{{< / code-panel >}}
  {{< code-panel language="python" >}}driver.set_window_size(1024, 768){{< / code-panel >}}
  {{< code-panel language="csharp" >}}driver.Manage().Window.Size = new Size(1024, 768);{{< / code-panel >}}
  {{< code-panel language="ruby" >}}driver.manage.window.resize_to(1024,768){{< / code-panel >}}
  {{< code-panel language="javascript" >}}await driver.manage().window().setRect({ width: 1024, height: 768 });{{< / code-panel >}}
  {{< code-panel language="kotlin" >}}driver.manage().window().size = Dimension(1024, 768){{< / code-panel >}}
{{< / code-tab >}}

### Get window position

Fetches the coordinates of the top left coordinate of the browser window.

{{< code-tab >}}
  {{< code-panel language="java" >}}
// Access each dimension individually
int x = driver.manage().window().getPosition().getX();
int y = driver.manage().window().getPosition().getY();

// Or store the dimensions and query them later
Point position = driver.manage().window().getPosition();
int x1 = position.getX();
int y1 = position.getY();
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
# Access each dimension individually
x = driver.get_window_position().get('x')
y = driver.get_window_position().get('y')

# Or store the dimensions and query them later
position = driver.get_window_position()
x1 = position.get('x')
y1 = position.get('y')
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
//Access each dimension individually
int x = driver.Manage().Window.Position.X;
int y = driver.Manage().Window.Position.Y;

//Or store the dimensions and query them later
Point position = driver.Manage().Window.Position;
int x1 = position.X;
int y1 = position.Y;
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
#Access each dimension individually
x = driver.manage.window.position.x
y = driver.manage.window.position.y

# Or store the dimensions and query them later
rect  = driver.manage.window.rect
x1 = rect.x
y1 = rect.y
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
// Access each dimension individually
const { x, y } = await driver.manage().window().getRect();

// Or store the dimensions and query them later
const rect = await driver.manage().window().getRect();
const x1 = rect.x;
const y1 = rect.y;
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
// Access each dimension individually
val x = driver.manage().window().position.x
val y = driver.manage().window().position.y

// Or store the dimensions and query them later
val position = driver.manage().window().position
val x1 = position.x
val y1 = position.y

  {{< / code-panel >}}
{{< / code-tab >}}

## Set window position

Moves the window to the chosen position.

{{< code-tab >}}
  {{< code-panel language="java" >}}
// Move the window to the top left of the primary monitor
driver.manage().window().setPosition(new Point(0, 0));
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
# Move the window to the top left of the primary monitor
driver.set_window_position(0, 0)
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
// Move the window to the top left of the primary monitor
driver.Manage().Window.Position = new Point(0, 0);
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
driver.manage.window.move_to(0,0)
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
// Move the window to the top left of the primary monitor
await driver.manage().window().setRect({ x: 0, y: 0 });
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
// Move the window to the top left of the primary monitor
driver.manage().window().position = Point(0,0)
    {{< / code-panel >}}
{{< / code-tab >}}

### Maximize window
Enlarges the window. For most operating systems, the window will fill
the screen, without blocking the operating system's own menus and
toolbars.

{{< code-tab >}}
  {{< code-panel language="java" >}}driver.manage().window().maximize();{{< / code-panel >}}
  {{< code-panel language="python" >}}driver.maximize_window(){{< / code-panel >}}
  {{< code-panel language="csharp" >}}driver.Manage().Window.Maximize();{{< / code-panel >}}
  {{< code-panel language="ruby" >}}driver.manage.window.maximize{{< / code-panel >}}
  {{< code-panel language="javascript" >}}await driver.manage().window().maximize();{{< / code-panel >}}
  {{< code-panel language="kotlin" >}}driver.manage().window().maximize(){{< / code-panel >}}
{{< / code-tab >}}

### Minimize window
Minimizes the window of current browsing context.
The exact behavior of this command is specific to
individual window managers.

Minimize Window typically hides the window in the system tray.

__Note: This feature works with Selenium 4 and later versions.__

{{< code-tab >}}
  {{< code-panel language="java" >}}driver.manage().window().minimize();{{< / code-panel >}}
  {{< code-panel language="python" >}}driver.minimize_window(){{< / code-panel >}}
  {{< code-panel language="csharp" >}}driver.Manage().Window.Minimize();{{< / code-panel >}}
  {{< code-panel language="ruby" >}}driver.manage.window.minimize{{< / code-panel >}}
  {{< code-panel language="javascript" >}}await driver.manage().window().minimize();{{< / code-panel >}}
  {{< code-panel language="kotlin" >}}driver.manage().window().minimize(){{< / code-panel >}}
{{< / code-tab >}}

### Fullscreen window

Fills the entire screen, similar to pressing F11 in most browsers.

{{< code-tab >}}
  {{< code-panel language="java" >}}driver.manage().window().fullscreen();{{< / code-panel >}}
  {{< code-panel language="python" >}}driver.fullscreen_window(){{< / code-panel >}}
  {{< code-panel language="csharp" >}}driver.Manage().Window.FullScreen();{{< / code-panel >}}
  {{< code-panel language="ruby" >}}driver.manage.window.full_screen{{< / code-panel >}}
  {{< code-panel language="javascript" >}}await driver.manage().window().fullscreen();{{< / code-panel >}}
  {{< code-panel language="kotlin" >}}driver.manage().window().fullscreen(){{< / code-panel >}}
{{< / code-tab >}}

### TakeScreenshot

Used to capture screenshot for current browsing context.
The WebDriver endpoint [screenshot](https://www.w3.org/TR/webdriver/#dfn-take-screenshot)
returns screenshot which is encoded in Base64 format.

{{< code-tab >}}
  {{< code-panel language="java" >}}
import org.apache.commons.io.FileUtils;
import org.openqa.selenium.chrome.ChromeDriver;
import java.io.*;
import org.openqa.selenium.*;

public class SeleniumTakeScreenshot {
    public static void main(String args[]) throws IOException {
        WebDriver driver = new ChromeDriver();
        driver.get("http://www.example.com");
        File scrFile = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
        FileUtils.copyFile(scrFile, new File("./image.png"));
        driver.quit();
    }
}
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
from selenium import webdriver

driver = webdriver.Chrome()

# Navigate to url
driver.get("http://www.example.com")

# Returns and base64 encoded string into image
driver.save_screenshot('./image.png')

driver.quit()

{{< / code-panel >}}
  {{< code-panel language="csharp" >}}
    using OpenQA.Selenium;
    using OpenQA.Selenium.Chrome;
    using OpenQA.Selenium.Support.UI;

    var driver = new ChromeDriver();
    driver.Navigate().GoToUrl("http://www.example.com");
    Screenshot screenshot = (driver as ITakesScreenshot).GetScreenshot();
    screenshot.SaveAsFile("screenshot.png", ScreenshotImageFormat.Png); // Format values are Bmp, Gif, Jpeg, Png, Tiff
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
require 'selenium-webdriver'
driver = Selenium::WebDriver.for :chrome

begin
  driver.get 'https://example.com/'

  # Takes and Stores the screenshot in specified path
  driver.save_screenshot('./image.png')

end
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
let {Builder} = require('selenium-webdriver');
let fs = require('fs');

(async function example() {
    let driver = await new Builder()
      .forBrowser('chrome')
      .build();

    await driver.get('https://www.example.com');
    // Returns base64 encoded string
    let encodedString = await driver.takeScreenshot();
    await fs.writeFileSync('./image.png', encodedString, 'base64');
    await driver.quit();
}())
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
import com.oracle.tools.packager.IOUtils.copyFile
import org.openqa.selenium.*
import org.openqa.selenium.chrome.ChromeDriver
import java.io.File

fun main(){
    val driver =  ChromeDriver()
    driver.get("https://www.example.com")
    val scrFile = (driver as TakesScreenshot).getScreenshotAs<File>(OutputType.FILE)
    copyFile(scrFile, File("./image.png"))
    driver.quit()
}
   {{< / code-panel >}}
{{< / code-tab >}}

###  TakeElementScreenshot

Used to capture screenshot of an element for current browsing context.
The WebDriver endpoint [screenshot](https://www.w3.org/TR/webdriver/#take-element-screenshot)
returns screenshot which is encoded in Base64 format.

{{< code-tab >}}
  {{< code-panel language="java" >}}
import org.apache.commons.io.FileUtils;
import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;
import java.io.File;
import java.io.IOException;

public class SeleniumelementTakeScreenshot {
  public static void main(String args[]) throws IOException {
    WebDriver driver = new ChromeDriver();
    driver.get("https://www.example.com");
    WebElement element = driver.findElement(By.cssSelector("h1"));
    File scrFile = element.getScreenshotAs(OutputType.FILE);
    FileUtils.copyFile(scrFile, new File("./image.png"));
    driver.quit();
  }
}
 {{< / code-panel >}}
  {{< code-panel language="python" >}}
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

# Navigate to url
driver.get("http://www.example.com")

ele = driver.find_element(By.CSS_SELECTOR, 'h1')

# Returns and base64 encoded string into image
ele.screenshot('./image.png')

driver.quit()
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
    using OpenQA.Selenium;
    using OpenQA.Selenium.Chrome;
    using OpenQA.Selenium.Support.UI;

    // Webdriver
    var driver = new ChromeDriver();
    driver.Navigate().GoToUrl("http://www.example.com");

    // Fetch element using FindElement
    var webElement = driver.FindElement(By.CssSelector("h1"));

    // Screenshot for the element
    var elementScreenshot = (webElement as ITakesScreenshot).GetScreenshot();
    elementScreenshot.SaveAsFile("screenshot_of_element.png");
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
# Works with Selenium4-alpha7 Ruby bindings and above
require 'selenium-webdriver'
driver = Selenium::WebDriver.for :chrome

begin
  driver.get 'https://example.com/'
  ele = driver.find_element(:css, 'h1')

  # Takes and Stores the element screenshot in specified path
  ele.save_screenshot('./image.jpg')
end
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
const {Builder, By} = require('selenium-webdriver');
let fs = require('fs');

(async function example() {
   let driver = await new Builder()
       .forBrowser('chrome')
       .build();

   await driver.get('https://www.example.com');
   let ele = await driver.findElement(By.css("h1"));
   // Captures the element screenshot
   let encodedString = await ele.takeScreenshot(true);
   await fs.writeFileSync('./image.png', encodedString, 'base64');
   await driver.quit();
}())
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
import org.apache.commons.io.FileUtils
import org.openqa.selenium.chrome.ChromeDriver
import org.openqa.selenium.*
import java.io.File

fun main() {
    val driver = ChromeDriver()
    driver.get("https://www.example.com")
    val element = driver.findElement(By.cssSelector("h1"))
    val scrFile: File = element.getScreenshotAs(OutputType.FILE)
    FileUtils.copyFile(scrFile, File("./image.png"))
    driver.quit()
}
  {{< / code-panel >}}
{{< / code-tab >}}

### Execute Script

Executes JavaScript code snippet in the
current context of a selected frame or window.

{{< code-tab >}}
  {{< code-panel language="java" >}}
    //Creating the JavascriptExecutor interface object by Type casting
      JavascriptExecutor js = (JavascriptExecutor)driver;
    //Button Element
      WebElement button =driver.findElement(By.name("btnLogin"));
    //Executing JavaScript to click on element
      js.executeScript("arguments[0].click();", button);
    //Get return value from script
      String text = (String) js.executeScript("return arguments[0].innerText", button);
    //Executing JavaScript directly
      js.executeScript("console.log('hello world')");
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
# Stores the header element
header = driver.find_element(By.CSS_SELECTOR, "h1")

# Executing JavaScript to capture innerText of header element
driver.execute_script('return arguments[0].innerText', header)
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
    //creating Chromedriver instance
	IWebDriver driver = new ChromeDriver();
	//Creating the JavascriptExecutor interface object by Type casting
	IJavaScriptExecutor js = (IJavaScriptExecutor) driver;
	//Button Element
	IWebElement button = driver.FindElement(By.Name("btnLogin"));
	//Executing JavaScript to click on element
	js.ExecuteScript("arguments[0].click();", button);
	//Get return value from script
	String text = (String)js.ExecuteScript("return arguments[0].innerText", button);
	//Executing JavaScript directly
	js.ExecuteScript("console.log('hello world')");
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
# Stores the header element
header = driver.find_element(css: 'h1')

# Get return value from script
result = driver.execute_script("return arguments[0].innerText", header)

# Executing JavaScript directly
driver.execute_script("alert('hello world')")
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
// Stores the header element
let header = await driver.findElement(By.css('h1'));

// Executing JavaScript to capture innerText of header element
let text = await driver.executeScript('return arguments[0].innerText', header);
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
// Stores the header element
val header = driver.findElement(By.cssSelector("h1"))

// Get return value from script
val result = driver.executeScript("return arguments[0].innerText", header)

// Executing JavaScript directly
driver.executeScript("alert('hello world')")
  {{< / code-panel >}}
{{< / code-tab >}}

### Print Page

Prints the current page within the browser

_Note: This requires Chromium Browsers to be in headless mode_


{{< code-tab >}}
  {{< code-panel language="java" >}}
    import org.openqa.selenium.print.PrintOptions;

    driver.get("https://www.selenium.dev");
    printer = (PrintsPage) driver;

    PrintOptions printOptions = new PrintOptions();
    printOptions.setPageRanges("1-2");

    Pdf pdf = printer.print(printOptions);
    String content = pdf.getContent();
  {{< / code-panel >}}
  {{< code-panel language="python" >}}
    from selenium.webdriver.common.print_page_options import PrintOptions

    print_options = PrintOptions()
    print_options.page_ranges = ['1-2']

    driver.get("printPage.html")

    base64code = driver.print_page(print_options)
  {{< / code-panel >}}
  {{< code-panel language="csharp" >}}
    // code sample not available please raise a PR
  {{< / code-panel >}}
  {{< code-panel language="ruby" >}}
    driver.navigate_to 'https://www.selenium.dev'

    base64encodedContent = driver.print_page(orientation: 'landscape')
  {{< / code-panel >}}
  {{< code-panel language="javascript" >}}
  const {Builder} = require('selenium-webdriver');
  const chrome = require('selenium-webdriver/chrome');
  let opts = new chrome.Options();
  let fs = require('fs');
  (async function example() {
  let driver = new Builder()
  .forBrowser('chrome')
  .setChromeOptions(opts.headless())
  .build();
  await driver.get('https://www.selenium.dev');
  try {
  let base64 = await driver.printPage({pageRanges:["1-2"]});
  await fs.writeFileSync('./test.pdf', base64, 'base64');
  } catch (e) {
  console.log(e)
  }
  await driver.quit();
  {{< / code-panel >}}
  {{< code-panel language="kotlin" >}}
    driver.get("https://www.selenium.dev")
    val printer = driver as PrintsPage

    val printOptions = PrintOptions()
    printOptions.setPageRanges("1-2")
    
    val pdf: Pdf = printer.print(printOptions)
    val content = pdf.content
  {{< / code-panel >}}
{{< / code-tab >}}
