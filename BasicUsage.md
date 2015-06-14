## Find an image target on the screen ##
Suppose this is what you see on the screen

![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/findImageIcon.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/findImageIcon.png)

Suppose you have captured an image of the Pictures icon and saved it as `pictures_icon.png`

![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/pictures_icon.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/pictures_icon.png)

You could find the location of the icon using the code as follows:
```
ScreenRegion s = new DesktopScreenRegion();
Target target = new ImageTarget(new File("pictures_icon.png"));
ScreenRegion r = s.find(target);
```

`s` is the default screen region which corresponds to the entire screen on your default monitor. `r` holds the screen region occupied by the Pictures icon that was found by Sikuli's image recognition engine. You can print out the (x,y) location as follows:
```
System.out.println(r.getBounds());
```

If the target image is hosted online, you could give the URL of the image as the parameter to `ImageTarget`'s constructor. For example, suppose the URL is `https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/pictures_icon.png`.
```
ScreenRegion s = new DesktopScreenRegion();
Target target = new ImageTarget(new URL("https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/pictures_icon.png"));
ScreenRegion r = s.find(target);
```

## Finding an image target and click on it ##

A common reason people want to find an image target on the screen is to tell a GUI robot to click on that target. You can accomplish this using Sikuli API as follows:

```
ScreenRegion s = new DesktopScreenRegion();
Target target = new ImageTarget(new File("pictures_icon.png"));
ScreenRegion r = s.find(target);

// Create a mouse object
Mouse mouse = new DesktopMouse();
// Use the mouse object to click on the center of the target region
mouse.click(r.getCenter());
```

Sikuli API provides methods to simulate mouse and keyboard operations through the `Mouse` and `Keyboard` interfaces. The default implementations are `DesktopMouse` and `DesktopKeyboard`, that can perform mouse and keyboard operations over the entire desktop.

## Finding an image target and highlight it ##

You may wonder whether Sikuli has really found the target you want to find. It would be useful to visualize the result of each find operation. Sikuli API provides a convenient class called `Canvas` that can help you draw annotations such as boxes, circles, and labels on the screen. For example, the code snippet below draws a rectangle around a screen region returned by Sikuli's find operation:

```
// Construct a Canvas object of the type DesktopCanvas
Canvas canvas = new DesktopCanvas();
// Add a box around a screen region 'r'
canvas.box(r);
// Add a label on the screen region r
canvas.label(r, "WE FOUND IT!!");
// Display the canvas for 3 seconds
canvas.display(3);
```

And this is what you will see:
![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/screenPainter.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/screenPainter.png)