# How can I ask Sikuli to find all instances of a target? #

Suppose your objective is to find all the checkboxes in this dialog window.

![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/findALl/checkboxes_goal.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/findALl/checkboxes_goal.png)

First, you need to capture a screenshot of a checkbox and use it to define an image target. You can use the `findAll()` method of the screen region object and give this image target as a parameter.  Suppose you save the screenshot as `checkbox.png` and it looks like
![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/findALl/checkbox.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/findALl/checkbox.png)

The code below will accomplish this objective:
```
ScreenRegion s = new DesktopScreenRegion();		
Target target = new ImageTarget(new File("checkbox.png")); 
List<ScreenRegion> rs = s.findAll(target);
```
`findAll()` returns a list of screen regions occupied by checkboxes. You can use a [DesktopCanvas](Canvas.md) object to draw a box around each checkbox in the list and display it on the screen; it helps you visualize what Sikuli has found.

```
// create a DesktopCanvas object to draw on the desktop
Canvas canvas = new DesktopCanvas();
// iterate through a list of screen regions and add a box around each
for (ScreenRegion r : rs){
	canvas.addBox(r);
}
// display the canvas for 3 seconds
canvas.display(3);
```
![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/findALl/checkboxes_result.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/findALl/checkboxes_result.png)