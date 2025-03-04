---
title: "Localiser des éléments"
linkTitle: "Localiser des éléments"
weight: 3
aliases: ["/documentation/fr/webdriver/locating_elements/"]
---

### Localiser des éléments

Une des techniques fondamentales à maîtriser lorsque l'on utilise WebDriver
consiste à chercher des éléments sur une page.
WebDriver offre pour cela un ensemble pré-défini de type de selecteurs,
parmi lesquels la recherche d'une élément par son attribut ID:

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
WebElement cheese = driver.findElement(By.id("fromage"));
  {{< /tab >}}
  {{< tab header="Python" >}}
driver.find_element(By.ID, "fromage")
  {{< /tab >}}
  {{< tab header="CSharp" >}}
IWebElement element = driver.FindElement(By.Id("fromage"));
  {{< /tab >}}
  {{< tab header="Ruby" >}}
cheese = driver.find_element(id: 'cheese')
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
const fromage = driver.findElement(By.id('fromage'));
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
val cheese: WebElement = driver.findElement(By.id("cheese"))
  {{< /tab >}}
{{< /tabpane >}}

Comme démontré dans cet exemple, la localisation des éléments à l'aide de WebDriver
se fait via une instance de l'objet `WebDriver`.
La méthode `findElement(By)` retourne un autre type d'objet fondamental, un `WebElement`.

* `WebDriver` represente la navigateur
* `WebElement` represente un noeud particulier du DOM
  (un lien, un champ texte, etc.)

Un fois que l'on a obtenu la référence de l'élément web qui a été "trouvé",
on peut encore réduire la portée de notre recherche
en utilisant le même appel de méthode sur l'instance de cet objet:

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
WebElement fromage = driver.findElement(By.id("fromage"));
WebElement cheddar = fromage.findElement(By.id("cheddar"));
  {{< /tab >}}
  {{< tab header="Python" >}}
fromage = driver.find_element(By.ID, "fromage")
cheddar = fromage.find_elements_by_id("cheddar")
  {{< /tab >}}
  {{< tab header="CSharp" >}}
IWebElement fromage = driver.FindElement(By.Id("fromage"));
IWebElement cheddar = fromage.FindElement(By.Id("cheddar"));
  {{< /tab >}}
  {{< tab header="Ruby" >}}
fromage = driver.find_element(id: 'fromage')
cheddar = fromage.find_element(id: 'cheddar')
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
const fromage = driver.findElement(By.id('fromage'));
const cheddar = fromage.findElement(By.id('cheddar'));
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
val cheese = driver.findElement(By.id("cheese"))
val cheddar = cheese.findElement(By.id("cheddar"))
  {{< /tab >}}
{{< /tabpane >}}

Nous pouvons faire cela car les types _WebDriver_ et _WebElement_
implémentent tous deux l'interface [_SearchContext_](//seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/SearchContext.html).
Dans WebDriver, ce principe est connu sous le nom de _role-based interface_.
Les interfaces basées sur le rôle nous permettent de déterminer
si une implémentation particulière de driver supporte une fonctionnalité donnée.
Ces interfaces sont clairement définies et tente d'adhérer au principe de responsabilité unique.
Vous pouvez en lire plus sur le design de WebDriver et sur quels drivers supportent quels rôles dans le chapitre [Un Autre Chapitre Qui Aura Un Nom](#).
<!-- TODO: A new section needs to be created for the above.-->

Par conséquent, l'interface _By_ utilisée précédement fournit également
d'autres stratégies de localisation. Une recherche imbriquée peut ne pas
être la startégie la plus adaptée pour trouver notre cheddar
puisqu'elle nécessite que deux instructions séparées soient envoyées au navigateur ;
tout d'abord rechercher un élément ayant pour ID "fromage",
puis une recherche pour "cheddar" dans ce contexte plus restreint.

Pour améliorer légèrement les performances, nous pourrions essayer
un sélecteur (une stratégie de localisation) plus spécifique :
WebDriver supporte la localisation d'élément via sélecteur CSS,
nous permettant de combiner les deux sélecteurs précédents en un seul:

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
driver.findElement(By.cssSelector("#fromage #cheddar"));
  {{< /tab >}}
  {{< tab header="Python" >}}
cheddar = driver.find_element_by_css_selector("#fromage #cheddar")
  {{< /tab >}}
  {{< tab header="CSharp" >}}
driver.FindElement(By.CssSelector("#fromage #cheddar"));
  {{< /tab >}}
  {{< tab header="Ruby" >}}
driver.find_element(css: '#fromage #cheddar')
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
const cheddar = driver.findElement(By.css('#fromage #cheddar'));
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
driver.findElement(By.cssSelector("#cheese #cheddar"))
  {{< /tab >}}
{{< /tabpane >}}

### Localiser plusieurs éléments

Il est possible que le document web sur lequel nous travaillons
dispose d'une liste ordonnée de nos fromages préférés:

```html
<ol id=fromage>
 <li id=cheddar>…
 <li id=brie>…
 <li id=rochefort>…
 <li id=camembert>…
</ol>
```
Puisque plus de fromage est sans conteste meilleur, et qu'il serait lourd
de devoir récupérer chaque item un par un, une technique supérieure est d'utiliser
la forme plurielle `findElements(By)`. Cette méthode retourne une collection
d'éléments web. Si un seul élement a été trouvé, la méthode renverra tout de même
une collection (d'un seul élément). Si aucun élément ne correspond au sélécteur,
la collection retournée sera alors vide.


{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
List<WebElement> pleinDeFromage = driver.findElements(By.cssSelector("#fromage li"));
  {{< /tab >}}
  {{< tab header="Python" >}}
plein_de_fromage = driver.find_elements_by_css_selector("#fromage li")
  {{< /tab >}}
  {{< tab header="CSharp" >}}
IReadOnlyList<IWebElement> pleinDeFromage = driver.FindElements(By.CssSelector("#fromage li"));
  {{< /tab >}}
  {{< tab header="Ruby" >}}
plein_de_fromage = driver.find_elements(css: '#fromage li')
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
const pleinDeFromage = driver.findElements(By.css('#fromage li'));
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
val muchoCheese: List<WebElement>  = driver.findElements(By.cssSelector("#cheese li"))
  {{< /tab >}}
{{< /tabpane >}}

### Stratégie de sélection des éléments

WebDriver possède huit stratégies de localisation pré-définies différentes:

| Sélecteur         | Description                                                                                            |
| ----------------- | ------------------------------------------------------------------------------------------------------ |
| class name        | Localise les éléments dont le nom de la classe contient la valeur recherchée (nom composés non permis) |
| css selector      | Localise les éléments correspondant à un sélecteur CSS                                                 |
| id                | Localise les éléments dont l'attribut ID correspond à la valeur recherchée                             |
| name              | Localise les éléments dont l'attribut NAME correspond à la valeur recherchée                           |
| link text         | Localise les éléments de type ancre (lien) dont le texte visible correspond à la valeur recherchée     |
| partial link text | Localise les éléments de type ancre (lien) dont le texte visible contient la valeur recherchée         |
| tag name          | Localise les éléments dont le nom de tag correspond à la valeur recherchée                             |
| xpath             | Localise les éléments correspondant à un chemin XPath                                                  |

### Astuces d'utilisation des sélecteurs

En règle général, si des ID HTML sont disponibles, uniques et prédictibles avec constance,
alors il est préférable d'utiliser cette stratégie pour la localisation d'élément sur une page.
Elle a tendance à être très rapide et évite les longs traitements liés à des traversées complexes du DOM.

Si des IDs uniques ne sont pas disponibles, un sélecteur CSS bien écrit
est la méthode de localisation la plus adaptée. Un sélecteur XPath marchera
aussi bien qu'un sélecteur CSS, cependant sa syntaxe est plus complexe, et souvent,
plus compliquée à débugguer. Même si les sélecteur XPath sont très flexibles,
ils sont rarement testés d'un point de vue performance par les fournisseurs de navigateur
et ont donc tendance à être assez lents.

Les stratégies basés sur _linkText_ et _partialLinkText_ sont
contraingnantes du fait qu'elles ne fonctionnent
que sur des éléments de type lien hypertexte. De plus, elles
sont implémentées au sein de WebDriver via des sélecteurs XPath.

Le nom de tag est une façon dangereuse de localiser des éléments.
Il y a fréquemment de multiples éléments ayant le même tag sur une page.
Cette stratégie est principalement utile lorsque utilisée avec la méthode
_findElements(By)_, renvoyant une collection des élements.

Au final, la recommendation est de garder ses sélecteurs aussi compacts et lisibles que possible.
Demander à WebDriver de traverser la structure du DOM est une opération très coûteuse,
de fait plus le scope de recherche sera restreint, meilleures seront les performances.

## Relative Locators

**Selenium 4** brings Relative Locators which are previously
called as _Friendly Locators_. This functionality was
added to help you locate elements that are nearby other elements.
The Available Relative Locators are:

* *above*
* *below*
* *toLeftOf*
* *toRightOf*
* *near*

_findElement_ method now accepts a new method `withTagName()`
which returns a RelativeLocator.

**NOTE**: Java bindings now support `with(By)` instead of `withTagName()` allowing users to pick
locator of their choice like _By.id_, _By.cssSelector_  etc.
This feature landed in **Selenium4 - beta3**

### How does it work

Selenium uses the JavaScript function
[getBoundingClientRect()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect)
to find the relative elements. This function returns
properties of an element such as
right, left, bottom, and top.

Let us consider the below example for understanding the relative locators.

{{< figure src="/images/documentation/webdriver/relative_locators.png" class="img-responsive text-center" alt="Relative Locators">}}

### above()

Returns the WebElement, which appears
above to the specified element

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
import static org.openqa.selenium.support.locators.RelativeLocator.with;

WebElement passwordField= driver.findElement(By.id("password"));
WebElement emailAddressField = driver.findElement(with(By.tagName("input"))
                                                  .above(passwordField));
  {{< /tab >}}
  {{< tab header="Python" >}}
from selenium.webdriver.support.relative_locator import with_tag_name

passwordField = driver.find_element(By.ID, "password")
emailAddressField = driver.find_element(with_tag_name("input").above(passwordField))
  {{< /tab >}}
  {{< tab header="CSharp" >}}
using static OpenQA.Selenium.RelativeBy;

IWebElement passwordField = driver.FindElement(By.Id("password"));
IWebElement emailAddressField = driver.FindElement(WithTagName("input").Above(passwordField));
  {{< /tab >}}
  {{< tab header="Ruby" >}}
password_field= driver.find_element(:id, "password")
email_address_field = driver.find_element(relative: {tag_name: 'input', above:password_field})
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
let passwordField = driver.findElement(By.id('password'));
let emailAddressField = await driver.findElement(withTagName('input').above(passwordField));
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
val passwordField = driver.findElement(By.id("password"))
val emailAddressField = driver.findElement(with(By.tagName("input")).above(passwordField))
  {{< /tab >}}
{{< /tabpane >}}


### below()

Returns the WebElement, which appears
below to the specified element

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
import static org.openqa.selenium.support.locators.RelativeLocator.with;

WebElement emailAddressField= driver.findElement(By.id("email"));
WebElement passwordField = driver.findElement(with(By.tagName("input"))
	                                          .below(emailAddressField));
  {{< /tab >}}
  {{< tab header="Python" >}}
from selenium.webdriver.support.relative_locator import with_tag_name

emailAddressField = driver.find_element(By.ID, "email")
passwordField = driver.find_element(with_tag_name("input").below(emailAddressField))
  {{< /tab >}}
  {{< tab header="CSharp" >}}
using static OpenQA.Selenium.RelativeBy;

IWebElement emailAddressField = driver.FindElement(By.Id("email"));
IWebElement passwordField = driver.FindElement(WithTagName("input").Below(emailAddressField));
  {{< /tab >}}
  {{< tab header="Ruby" >}}
email_address_field= driver.find_element(:id, "email")
password_field = driver.find_element(relative: {tag_name: 'input', below: email_address_field})
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
let emailAddressField = driver.findElement(By.id('email'));
let passwordField = await driver.findElement(withTagName('input').below(emailAddressField));
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
val emailAddressField = driver.findElement(By.id("email"))
val passwordField = driver.findElement(with(By.tagName("input")).below(emailAddressField))
  {{< /tab >}}
{{< /tabpane >}}


### toLeftOf()

Returns the WebElement, which appears
to left of specified element

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
import static org.openqa.selenium.support.locators.RelativeLocator.with;

WebElement submitButton= driver.findElement(By.id("submit"));
WebElement cancelButton= driver.findElement(with(By.tagName("button"))
                                            .toLeftOf(submitButton));
  {{< /tab >}}
  {{< tab header="Python" >}}
from selenium.webdriver.support.relative_locator import with_tag_name

submitButton = driver.find_element(By.ID, "submit")
cancelButton = driver.find_element(with_tag_name("button").
                                   to_left_of(submitButton))
  {{< /tab >}}
  {{< tab header="CSharp" >}}
using static OpenQA.Selenium.RelativeBy;

IWebElement submitButton = driver.FindElement(By.Id("submit"));
IWebElement cancelButton = driver.FindElement(WithTagName("button").LeftOf(submitButton));
  {{< /tab >}}
  {{< tab header="Ruby" >}}
submit_button= driver.find_element(:id, "submit")
cancel_button = driver.find_element(relative: {tag_name: 'button', left:submit_button})
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
let submitButton = driver.findElement(By.id("submit"));
let cancelButton = await driver.findElement(withTagName("button").toLeftOf(submitButton));
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
val submitButton= driver.findElement(By.id("submit"))
val cancelButton= driver.findElement(with(By.tagName("button")).toLeftOf(submitButton))
  {{< /tab >}}
{{< /tabpane >}}


### toRightOf()

Returns the WebElement, which appears
to right of the specified element

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
import static org.openqa.selenium.support.locators.RelativeLocator.with;

WebElement cancelButton= driver.findElement(By.id("cancel"));
WebElement submitButton= driver.findElement(with(By.tagName("button"))
                                            .toRightOf(cancelButton));
  {{< /tab >}}
  {{< tab header="Python" >}}
from selenium.webdriver.support.relative_locator import with_tag_name

cancelButton = driver.find_element(By.ID, "cancel")
submitButton = driver.find_element(with_tag_name("button").
                                   to_right_of(cancelButton))
  {{< /tab >}}
  {{< tab header="CSharp" >}}
using static OpenQA.Selenium.RelativeBy;

IWebElement cancelButton = driver.FindElement(By.Id("cancel"));
IWebElement submitButton = driver.FindElement(WithTagName("button").RightOf(cancelButton));
  {{< /tab >}}
  {{< tab header="Ruby" >}}
cancel_button = driver.find_element(:id, "cancel")
submit_button = driver.find_element(relative: {tag_name: 'button', right:cancel_button})
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
let cancelButton = driver.findElement(By.id('cancel'));
let submitButton = await driver.findElement(withTagName('button').toRightOf(cancelButton));
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
val cancelButton= driver.findElement(By.id("cancel"))
val submitButton= driver.findElement(with(By.tagName("button")).toRightOf(cancelButton))
  {{< /tab >}}
{{< /tabpane >}}

### near()

Returns the WebElement, which is
at most `50px` away from the specified element.

{{< tabpane langEqualsHeader=true >}}
  {{< tab header="Java" >}}
import static org.openqa.selenium.support.locators.RelativeLocator.with;

WebElement emailAddressLabel= driver.findElement(By.id("lbl-email"));
WebElement emailAddressField = driver.findElement(with(By.tagName("input"))
                                                  .near(emailAddressLabel));
  {{< /tab >}}
  {{< tab header="Python" >}}
from selenium.webdriver.support.relative_locator import with_tag_name

emailAddressLabel = driver.find_element(By.ID, "lbl-email")
emailAddressField = driver.find_element(with_tag_name("input").
                                       near(emailAddressLabel))
  {{< /tab >}}
  {{< tab header="CSharp" >}}
using static OpenQA.Selenium.RelativeBy;

IWebElement emailAddressLabel = driver.FindElement(By.Id("lbl-email"));
IWebElement emailAddressField = driver.FindElement(WithTagName("input").Near(emailAddressLabel));
  {{< /tab >}}
  {{< tab header="Ruby" >}}
email_address_label = driver.find_element(:id, "lbl-email")
email_address_field = driver.find_element(relative: {tag_name: 'input', near: email_address_label})
  {{< /tab >}}
  {{< tab header="JavaScript" >}}
let emailAddressLabel = driver.findElement(By.id("lbl-email"));
let emailAddressField = await driver.findElement(withTagName("input").near(emailAddressLabel));
  {{< /tab >}}
  {{< tab header="Kotlin" >}}
val emailAddressLabel = driver.findElement(By.id("lbl-email"))
val emailAddressField = driver.findElement(with(By.tagName("input")).near(emailAddressLabel))
  {{< /tab >}}
{{< /tabpane >}}
