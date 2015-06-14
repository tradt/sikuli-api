# Sikuli Java API #

Sikuli API for Java provides image-based GUI automation functionalities to Java programmers.
It is created and will be actively maintained by [Sikuli Lab](http://lab.sikuli.org). The effort of making this API is a response to the desire of many Sikuli users to use Sikuli Script's functionalities directly in their Java programs, rather than writing Jython scripts. This new Java library
has a re-designed API and includes several new functions that were not available in the original Sikuli Script,
such as the abilities to match colors, handle events, and find geometric patterns such as rectangular buttons. Moreover, it has a greatly simplified build process based on Maven.

### Donation ###
If you find Sikuli Java API useful, please make a donation to help keep Sikuli free and open-source.

[Make a Donation via Paypal](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=XV39MHCHHK6ZY&lc=US&item_name=Sikuli&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donate_LG%2egif%3aNonHosted)

### News ###

**July 31, 2013
  * [Sikuli Slides](http://slides.sikuli.org) - 1.3.0 Release!!!**

**April 30, 2013
  * [Sikuli Slides](SikuliSlides.md) - 1.2.0 Release!!!**

**April 8, 2013
  * [Sikuli Slides](SikuliSlides.md) - 1.1.0 Release.**

**Mar 6, 2013
  * [Sikuli Slides](SikuliSlides.md) - 1.0.0 Release.**

**Nov 18, 2012 Version 1.0.2**
  * [Relative](Relative.md) for defining region/location based on another region/location
  * [Canvas](Canvas.md) for drawing graphical objects on screen
  * [MultiStateTarget](MultiStateTarget.md) for finding targets with multiple state-dependent appearances (e.g., checkboxes)

### Requirements ###

  * Java Runtime Environment (JRE) or Java Development Kit (JDK) version 1.6 or newer
  * (Optional) Apache Maven version 2.0.10 or newer, if you want to build it from source.

### Supported Platforms ###
  * Windows 7 (64/32 bits)
  * Mac OS X (64 bits)
  * Linux (64 bits) [See special instructions](LinuxInstallation.md)

## Quick Start ##

1. Read about the [basic API usage](BasicUsage.md)

1. Download the lastest sikuli-api library `sikuli-api-1.x.x-standalone.jar` from the Downloads page.

2. Use your favorite editor to compose the Hello World example as follows:

```
import java.net.MalformedURLException;
import java.net.URL;

import org.sikuli.api.*;
import org.sikuli.api.robot.Mouse;
import org.sikuli.api.robot.desktop.DesktopMouse;
import org.sikuli.api.visual.Canvas;
import org.sikuli.api.visual.DesktopCanvas;

import static org.sikuli.api.API.*;

public class HelloWorldExample {

	public static void main(String[] args) throws MalformedURLException {
					
		// Open the main page of Google Code in the default web browser
		browse(new URL("http://code.google.com"));

		// Create a screen region object that corresponds to the default monitor in full screen 
		ScreenRegion s = new DesktopScreenRegion();
				
		// Specify an image as the target to find on the screen
		URL imageURL = new URL("http://code.google.com/images/code_logo.gif");                
		Target imageTarget = new ImageTarget(imageURL);
				
		// Wait for the target to become visible on the screen for at most 5 seconds
		// Once the target is visible, it returns a screen region object corresponding
		// to the region occupied by this target
		ScreenRegion r = s.wait(imageTarget,5000);
				
		// Display "Hello World" next to the found target for 3 seconds
		Canvas canvas = new DesktopCanvas();
		canvas.addLabel(r, "Hello World").display(3);
		
		// Click the center of the found target
		Mouse mouse = new DesktopMouse();
		mouse.click(r.getCenter());
	}
}
```

### Command line ###

  1. Compile
```
$ javac -cp sikuli-api-1.x.x-standalone.jar HelloWorldExample.java
```
  1. Run
```
$ java -cp .:sikuli-api-1.x.x-standalone.jar HelloWorldExample
```


### Eclipse ###

  1. Include sikuli-api-1.x.x-standalone.jar in the build path
  1. Run

### Maven ###

Add the following dependency to your project's pom.xml.

```
<dependency>
	<groupId>org.sikuli</groupId>
	<artifactId>sikuli-api</artifactId>
	<version>1.0.2</version>
</dependency>
```

## Projects using Sikuli Java API ##
  * [SikuliFirefoxDriver](SikuliWebDriver.md) combines Sikuli and Selenium to drive Firefox
  * [node-sikuli-api](https://github.com/audreyt/node-sikuli-api) provides Sikuli API binding for Node.js
  * [sikuli-clj](https://github.com/cstrahan/sikuli-clj) provides a Clojure facade for Sikuli API
  * [Sikuli Gem](http://rubygems.org/gems/sikuli) provides binding for Ruby (coming soon)