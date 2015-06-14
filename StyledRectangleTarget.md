`StyledRectangleTarget` is designed to look for rectangles that have a particular visual style.
To specify a `StyledRectangleTarget`, you simply provide an image to illustrate
the line and corner style of a rectangle. For instance, suppose you wish to look for
all the buttons on an interface that have rounded corners. You can take a screenshot image of one of the
buttons that have the said rounded corners. Then you can use this image to define a `StyleRectangleTarget`
to look for all the other buttons with the same rounded corners, even if these other buttons
have different labels or have different sizes.

# Example: Calculator #

Consider the calculator interface below. Let's say we want to find all the buttons.

![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/Calculator.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/Calculator.png)

First, we take a screenshot of a button.

| Screenshot | URL |
|:-----------|:----|
| ![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/CalculatorButton.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/CalculatorButton.png) | ![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/CalculatorButton.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/CalculatorButton.png) |

## Wrong: Using `ImageTarget` ##

Let's use an `ImageTarget` and see how many buttons can be found.

1. Create an `ImageTarget` and limit the result to 20 matches.
```
URL url = new URL("http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/CalculatorButton.png");
Target target = new ImageTarget(url);
target.setLimit(20);
```

2. Use this image target to find all similar looking buttons.
```
ScreenRegion s = new DesktopScreenRegion();
List<ScreenRegion> rs = s.findAll(target);
```

3. Display a box around each region returned by `findAll()`
```
for (ScreenRegion r : rs){
	canvas.addBox(r);
}
canvas.display(3);
```

Below is the result. Only 10 out of 20 buttons are successfully found. Many are not found because the label text looks too different.

![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/CalculatorResultWrong.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/CalculatorResultWrong.png)

## Correct: Using `StyledRectangleTarget` ##

Let's use a `StyledRectangleTarget` instead of an `ImageTarget`. Sikuli will only consider the style of the rectangles (lines and corners),  ignoring the content inside the rectangle.

Create an `StyledRectangleTarget` and limit the result to 20 matches.
```
URL url = new URL("http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/CalculatorButton.png");
Target target = new StyledRectangleTarget(url);
target.setLimit(20);
```

The rest of the code is the same as above. The result is shown below. We are able to find all twenty buttons..

![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/CalculatorResult.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/CalculatorResult.png)

## Explanation ##

What is the secret behind `StyledRectangleTarget`?

Given an image of the button:

![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/CalculatorButton.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/CalculatorButton.png)

First, we identify the four corners in this example image.

![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/corners.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/corners.png)

Second, we look at the interface and find all matching corners.

![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/matchedCorners.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/matchedCorners.png)

Finally, we group the matched corners into valid, non-overlapping rectangles.

![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/rectangles.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/rectangles.png)

# Example: Java Swing Buttons #

Consider the Java Swing dialog box below. Notice that some buttons are longer than the others.

![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/ButtonGroups.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/ButtonGroups.png)

Let's take a screenshot of the button that says _Wally_ to use as an example.
| Screenshot | URL |
|:-----------|:----|
| ![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/wally.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/wally.png) | ![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/wally.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/wally.png) |

```
URL url = new URL("http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/wally.png");
Target target = new StyledRectangleTarget(url);
```

Below is the result. Eleven of twelve buttons are found. The only button not found (i.e., Eddie) has a different style.
![http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/ButtonGroupsResult.png](http://wiki.sikuli-api.googlecode.com/git/images/styledRectangleTarget/ButtonGroupsResult.png)