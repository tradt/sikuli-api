# Introduction #

`MultiStateTarget` lets you define a target that may look differently according its state. The most common examples are checkboxes and radio buttons.

## Finding the state of a lock ##

Suppose the following two image files are in the working directory:

![http://wiki.sikuli-api.googlecode.com/git/images/multistate/locked.png](http://wiki.sikuli-api.googlecode.com/git/images/multistate/locked.png)
`locked.png`
![http://wiki.sikuli-api.googlecode.com/git/images/multistate/unlocked.png](http://wiki.sikuli-api.googlecode.com/git/images/multistate/unlocked.png)
`unlocked.png`

To create a target for the lock icon that has two states: locked and unlocked

```
MultiStateTarget target = new MultiStateTarget();
target.addState(new ImageTarget(new File("locked.png")), "locked");
target.addState(new ImageTarget(new File("unlocked.png")), "unlocked");
```

Then to find this lock icon and display its state:

```
ScreenRegion s = new DesktopScreenRegion();
ScreenRegion r = s.find(target);

Canvas canvas = new ScreenRegionCanvas(s);
canvas.addLabel(Relative.to(r).topRight().getScreenLocation(), (String) r.getState());
canvas.display(3);
```

The result:

![http://wiki.sikuli-api.googlecode.com/git/images/multistate/network_unlocked.png](http://wiki.sikuli-api.googlecode.com/git/images/multistate/network_unlocked.png)

## Finding checkboxes and their states ##

Suppose the following two image files are in the working directory:

![http://wiki.sikuli-api.googlecode.com/git/images/multistate/checked.png](http://wiki.sikuli-api.googlecode.com/git/images/multistate/checked.png)
`checked.png`
![http://wiki.sikuli-api.googlecode.com/git/images/multistate/unchecked.png](http://wiki.sikuli-api.googlecode.com/git/images/multistate/unchecked.png)
`unchecked.png`

To create a target for a checkbox that has two states: checked and unchecked:

```
MultiStateTarget checkbox = new MultiStateTarget();
checkbox.addState(new ImageTarget(new File("checked.png")), "yes");
checkbox.addState(new ImageTarget(new File("unchecked.png")), "no");
```

Then to find all the checkboxes and display their states:

```
ScreenRegion s = new DesktopScreenRegion();
List<ScreenRegion> checkboxes = s.findAll(checkbox);
for (ScreenRegion c : checkboxes){
	String state = (String) c.getState();
	canvas.addBox(c);
	ScreenLocation labelLocation = Relative.to(c).topRight().getScreenLocation();
	canvas.addLabel(labelLocation, state);
}
```

The result:

![http://wiki.sikuli-api.googlecode.com/git/images/multistate/checkboxes.png](http://wiki.sikuli-api.googlecode.com/git/images/multistate/checkboxes.png)
