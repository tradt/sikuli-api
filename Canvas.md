This document explains how you can use a `Canvas` object to draw graphical elements on the screen in order to visualize the results of Sikuli's find operations.

## Finding a target ##
Suppose we want to find Chrome's shortcut on the desktop.

![http://wiki.sikuli-api.googlecode.com/git/images/canvas/chrome.png](http://wiki.sikuli-api.googlecode.com/git/images/canvas/chrome.png)

Suppose the desktop looks like this:

![http://wiki.sikuli-api.googlecode.com/git/images/canvas/desktop.png](http://wiki.sikuli-api.googlecode.com/git/images/canvas/desktop.png)


The code below finds the shortcut and stores the result in `r`.
```
ScreenRegion s = new DesktopScreenRegion();
URL imageUrl = new URL("http://wiki.sikuli-api.googlecode.com/git/images/canvas/chrome.png");
Target target = new ImageTarget(imageUrl);
ScreenRegion r = s.find(target);
```

## Drawing a box around a screen region ##

![http://wiki.sikuli-api.googlecode.com/git/images/canvas/box.png](http://wiki.sikuli-api.googlecode.com/git/images/canvas/box.png)

```
// create a canvas of the type "DesktopCanvas"
Canvas canvas = new DesktopCanvas();
// add a box to the canvas around the screen region 'r'
canvas.addBox(r);
// display the canvas for 3 seconds
canvas.display(3);
```

Or
```
Canvas canvas = new DesktopCanvas();
canvas.addBox(r).display(3);
```

## Drawing a label on a screen region ##

![http://wiki.sikuli-api.googlecode.com/git/images/canvas/label.png](http://wiki.sikuli-api.googlecode.com/git/images/canvas/label.png)

```
// create a canvas of the type "DesktopCanvas"
Canvas canvas = new DesktopCanvas();
// add a label and display for 3 seconds
canvas.addLabel(r, "This is Chrome").display(3);
```

## Drawing a label above a screen region (using `Relative`) ##

![http://wiki.sikuli-api.googlecode.com/git/images/canvas/labelAbove.png](http://wiki.sikuli-api.googlecode.com/git/images/canvas/labelAbove.png)

```
Canvas canvas = new DesktopCanvas();
canvas.addLabel(Relative.to(r).above(30).getScreenRegion(), "This is Chrome");
canvas.display(3);
```

## Drawing a box and a label ##

![http://wiki.sikuli-api.googlecode.com/git/images/canvas/box_label.png](http://wiki.sikuli-api.googlecode.com/git/images/canvas/box_label.png)

```
Canvas canvas = new DesktopCanvas();
canvas.addBox(r);
canvas.addLabel(r, "This is Chrome");
canvas.display(3);
```

## Setting the style of graphical elements ##

![http://wiki.sikuli-api.googlecode.com/git/images/canvas/style.png](http://wiki.sikuli-api.googlecode.com/git/images/canvas/style.png)

```
Canvas canvas = new DesktopCanvas();
canvas.addBox(r).withLineColor(Color.green).withLineWidth(5);
canvas.addLabel(r, "This is Chrome").withColor(Color.red).withFontSize(20);
canvas.display(1);
```

## Drawing boxes for a list of targets ##

![http://wiki.sikuli-api.googlecode.com/git/images/canvas/list.png](http://wiki.sikuli-api.googlecode.com/git/images/canvas/list.png)

```
// create a target based on an image of a checkbox
URL imageUrl = new URL("http://wiki.sikuli-api.googlecode.com/git/images/canvas/checkbox.png");
Target target = new ImageTarget(imageUrl);

// find all the checkboxes and save the results
// in 'rs', which is a list of screen regions
ScreenRegion s = new DesktopScreenRegion();
List<ScreenRegion> rs = s.findAll(target);

// create a canvas and add a box for each screen region in the list
Canvas canvas = new DesktopCanvas();
for (ScreenRegion r : rs){
	canvas.addBox(r);
}

// display the canvas for 3 seconds
canvas.display(3);
```