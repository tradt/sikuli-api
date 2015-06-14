

# How can I ask Sikuli to only look at a specific region? #

Suppose you want Sikuli to look at only a specific region within the mobile device's touch screen area because either (1) you don't want Sikuli to be distracted by pattens in other areas or (2) you want Sikuli to run faster by giving it a smaller area to search.

![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/screenRegion/local_goal.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/screenRegion/local_goal.png)

First, you need to determine the location and size of the region. Suppose the location is (20,80) and the width and height of the region are 360 and 125 respectively. You can specify these numbers as parameters as you construct a `ScreenRegion` object:

```
ScreenRegion s = new DesktopScreenRegion(20,80,360,125);
```

To check if the region you specify does correspond to the region you want Sikuli to watch on the screen, you can use a Canvas object to draw a rectangular box to visualize the region on the screen.
```
// Use a DesktopCanvas to draw a box around the region 
// in order to visualize if the region is correctly specified
Canvas canvas = new DesktopCanvas();
canvas.addBox(s);
canvas.addLabel("Sikuli Will Look Only Here");
canvas.display(3);
```

![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/screenRegion/local_visualization.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/screenRegion/local_visualization.png)

Now you can ask Sikuli to look for a particular image icon in this restricted region.

Suppose you want Sikuli to look for
![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/pictures_icon.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/pictures_icon.png)
and the path to this image file is `pictures_icon.png`, you can write:
```
ScreenRegion s = new DesktopScreenRegion(20,80,360,125);
ScreenRegion result = s.find(new ImageTarget(new File("pictures_icon.png")));
```

Suppose you want Sikuli to look for
![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/galaxy_ok_button.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/galaxy_ok_button.png) and
and the path to this image file is `galaxy_ok_button.png`, you can write:
```
ScreenRegion ok_button_result = s.find(new ImageTarget(new File("galaxy_ok_button.png")));
```
But Sikuli will not be able to find this button because it is outside of the region Sikuli is asked to look at. In this case, the `s.find()` method will return `null`.


# How can I ask Sikuli to look at a region relative to a target? #

Suppose you want Sikuli to click on the `Settings` button. But there is another button that looks exactly the same. How can you ask Sikuli to look at the right place and click on the right target?

![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/screenRegion/relative_goal.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/screenRegion/relative_goal.png)

The strategy is to look for a distinctive visual landmark around your target and ask Sikuli to look for that landmark first. Then you can ask Sikuli to look at a region relative to that landmark.

In this example, you can ask Sikuli to look for the paragraph describing that button:

![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/screenRegion/relative_landmark.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/screenRegion/relative_landmark.png)

Then you can ask Sikuli to look specifically at the right of this paragraph.

The code below accomplishes this strategy. It makes use of the `Relative.to` expression. A`ScreenPainter` object draws both regions to help you visualize whether you got the right regions, which is useful for debugging.
```
ScreenRegion s = new DesktopScreenRegion();
ScreenRegion autoCompleteText = s.find(new ImageTarget(new File("autoCompleteText.png"));
ScreenRegion right = Relative.to(autoCompleteText).right(150).getScreenRegion();		
		
Canvas painter = new DesktopCanvas();
canvas.addBox(autoCompleteText);
canvas.addBox(right);
canvas.display(3);
```

![https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/screenRegion/relative_visualization.png](https://dl.dropbox.com/u/5104407/SikuliAPIWikiImages/screenRegion/relative_visualization.png)

Once you are sure you ask Sikuli to look at the right region, you can ask it to look for the `Settings` button and click on it.
```
ScreenRegion settings_button_region = right.find(new ImageTarget(new File("settings_button.png")));
Mouse mouse = new DesktopMouse();
mouse.click(settings_button_region.getCenter());
```