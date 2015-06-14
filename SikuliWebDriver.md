# `SikuliFirefoxDriver` #

`SikuliFirefoxDriver` extends Selenium's `FirefoxDriver` by adding Sikuli's image search capability. It is useful for automating interactions with highly visual interfaces such as Google Map.

![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/webdriver/concept.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/webdriver/concept.png)

![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/webdriver/logo.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/webdriver/logo.png)

## Use ##

`findImageElement()` is the method that allows one to find an element using an image. For example, the code below opens Firefox, opens Google Code's homepage, and locates the logo image of Google Code.
```
SikuliFirefoxDriver driver = new SikuliFirefoxDriver();		
driver.get("http://code.google.com");
ImageElement image = driver.findImageElement(new URL("http://code.google.com/images/code_logo.gif"));
```

Since `SikuliFirefoxDriver` directly inherits from Selenium's `FirefoxDriver` class, you can use all existing methods provided by `FirefoxDriver` such as the example below that uses `findElement(By ...)` to locate Google Code's search box and enter "Sikuli" as a search string:
```
driver.findElement(By.id("gsearchInput"));
driver.sendKeys("Sikuli");
```

## Setup ##

If you use Maven, add the dependency statements below to your project's `pom.xml`:
```
<dependency>
	<groupId>org.sikuli</groupId>
	<artifactId>sikuli-webdriver</artifactId>
	<version>1.0.1</version>
</dependency>
```


## Google Map example ##

Here is an complete example that demonstrates how one can use `SikuliFirefoxDriver` to drive interactions with a web page using both image recognition (Sikuli) and DOM (Selenium). This example performs the sequence of the operations below:

  1. _Selenium_: Enter "`Denver, CO`" as search terms, finding the search box using element ID `gbqfq`
  1. _Sikuli_: Click on ![https://dl.dropbox.com/u/5104407/lakewood.png](https://dl.dropbox.com/u/5104407/lakewood.png) to zoom in to the Lakewood region.
  1. _Sikuli_: Click on ![https://dl.dropbox.com/u/5104407/kendrick_lake.png](https://dl.dropbox.com/u/5104407/kendrick_lake.png) to zoom in to the Kendrick Lake region.
  1. _Sikuli_: Click on ![https://dl.dropbox.com/u/5104407/satellite.png](https://dl.dropbox.com/u/5104407/satellite.png) to switch to the satellite view.
  1. _Sikuli_: Click on ![https://dl.dropbox.com/u/5104407/plus.png](https://dl.dropbox.com/u/5104407/plus.png) to zoom in within the current view.
  1. _Selenium_: Click on the LINK button, finding the button using element ID `link`

```
package org.sikuli.webdriver.examples;

import java.io.IOException;
import java.net.URL;

import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebElement;
import org.sikuli.webdriver.ImageElement;
import org.sikuli.webdriver.SikuliFirefoxDriver;

public class GoogleMapExample {
	
	public static void main(String[] args) throws IOException {
		
		SikuliFirefoxDriver driver = new SikuliFirefoxDriver();		
		
		// visit Google Map
		driver.get("https://maps.google.com/");
		
		// enter "Denver, CO" as search terms
		WebElement input = driver.findElement(By.id("gbqfq"));
		input.sendKeys("Denver, CO");		
		input.sendKeys(Keys.ENTER);

		ImageElement image;
		
		// find and click on the image of the lakewood area
		image = driver.findImageElement(new URL("https://dl.dropbox.com/u/5104407/lakewood.png"));
		image.doubleClick()	;		
		
		// find and click on the image of the kendrick lake area
		image = driver.findImageElement(new URL("https://dl.dropbox.com/u/5104407/kendrick_lake.png"));
		image.doubleClick();

		// find and click the Satellite icon to switch to the satellite view
		image = driver.findImageElement(new URL("https://dl.dropbox.com/u/5104407/satellite.png"));		
		image.click();

		// find and click the plus button to zoom in
		image = driver.findImageElement(new URL("https://dl.dropbox.com/u/5104407/plus.png"));
		image.click();
		
		// find and click the link button
		WebElement linkButton = driver.findElement(By.id("link"));
		linkButton.click();
				
	}

}

```

<a href='http://www.youtube.com/watch?feature=player_embedded&v=ylVu30h0AD4' target='_blank'><img src='http://img.youtube.com/vi/ylVu30h0AD4/0.jpg' width='425' height=344 /></a>

## Page Object ##

You can define page objects with image elements using the `@FindByImage` annotation. It can be used together with the `@FindBy` annotation provided by Selenium.

```
public class GoogleMapPage {

	@FindBy(how = How.ID, using = "gbqfq")
	private WebElement searchInput;

	@FindByImage(url = "https://dl.dropbox.com/u/5104407/plus.png")
	private ImageElement plus;
	
	public void zoomIn(){
		plus.click();
	}

	public void searchFor(String text) {
		searchInput.clear();
		searchInput.sendKeys(text);
		searchInput.submit();
	}
}
```

Below is a more complete example:

```
import java.io.IOException;

import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.FindBy;
import org.openqa.selenium.support.How;
import org.sikuli.webdriver.ImageElement;
import org.sikuli.webdriver.SikuliFirefoxDriver;
import org.sikuli.webdriver.support.FindByImage;
import org.sikuli.webdriver.support.SikuliPageFactory;

public class PageObjectsExample {
	public static void main(String[] args) throws IOException {

		SikuliFirefoxDriver driver = new SikuliFirefoxDriver();
		driver.get("http://map.google.com/");

		GoogleMapPage page = SikuliPageFactory.initElements(driver, GoogleMapPage.class);
		page.searchFor("Denver, CO");		
		
		DenverArea denverMap = SikuliPageFactory.initElements(driver, DenverArea.class);
		denverMap.lakewood.doubleClick();
		
		denverMap.searchFor("hotel");
		
		denverMap.zoomIn();

	}
	
	public static class DenverArea extends GoogleMapPage {
		@FindByImage(url = "https://dl.dropbox.com/u/5104407/lakewood.png")
		public ImageElement lakewood;				
	} 
	
	public static class GoogleMapPage {

		@FindBy(how = How.ID, using = "gbqfq")
		private WebElement searchInput;

		@FindByImage(url = "https://dl.dropbox.com/u/5104407/plus.png")
		private ImageElement plus;
		
		public void zoomIn(){
			plus.click();
		}

		public void searchFor(String text) {
			searchInput.clear();
			searchInput.sendKeys(text);
			searchInput.submit();
		}
	} 

}

```