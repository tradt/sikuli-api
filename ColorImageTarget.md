# Introduction #

`ColorImageTarget` lets you define targets based on color patterns. It also takes into account of textures to make sure a blue star won't match anything that happens to be blue. The motivation behind `ColorImageTarget` is that Sikuli's image recognition by default pays attention mostly to texture patterns. In some occasions it may fail to distinguish targets that differ only in colors. For example, a normal `ImageTarget` may sometimes see a blue circle and a red circle as exactly the same. `ColorImageTarget` provides a solution for this problem.

## Finding a red box ##

Consider the following view of a list of calendars, each calendar is denoted by color box.

![http://wiki.sikuli-api.googlecode.com/git/images/colorImageTarget/calendars.png](http://wiki.sikuli-api.googlecode.com/git/images/colorImageTarget/calendars.png)

Suppose we want to use the image below to find the red box.

![http://wiki.sikuli-api.googlecode.com/git/images/colorImageTarget/redBox.png](http://wiki.sikuli-api.googlecode.com/git/images/colorImageTarget/redBox.png)

Using an `ImageTarget` like below,
```
// Wrong 
URL url = new URL("http://wiki.sikuli-api.googlecode.com/git/images/colorImageTarget/redBox.png")
Target target = new ImageTarget(url);
ScreenRegion r = s.find(target);
canvas.addBox(r).display(3);
```
The purple box is incorrectly returned as the top match.

![http://wiki.sikuli-api.googlecode.com/git/images/colorImageTarget/wrong_match.png](http://wiki.sikuli-api.googlecode.com/git/images/colorImageTarget/wrong_match.png)

Using a `ColorImageTarget` like below,
```
// Correct
URL url = new URL("http://wiki.sikuli-api.googlecode.com/git/images/colorImageTarget/redBox.png")
Target target = new ColorImageTarget(url);
ScreenRegion r = s.find(target);
canvas.addBox(r).display(3);
```
The red box is correctly identified.

![http://wiki.sikuli-api.googlecode.com/git/images/colorImageTarget/correct_match.png](http://wiki.sikuli-api.googlecode.com/git/images/colorImageTarget/correct_match.png)

