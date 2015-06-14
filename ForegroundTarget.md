Purpose: Find foreground targets based on whether they have textures (as opposed to textureless background)

## Finding a foreground target ##

![http://wiki.sikuli-api.googlecode.com/git/images/foregroundTarget/piggie1.png](http://wiki.sikuli-api.googlecode.com/git/images/foregroundTarget/piggie1.png)
```
Target t = new ForegroundTarget();
ScreenRegion s = r.find(t);
```

## Finding multiple foreground targets ##

![http://wiki.sikuli-api.googlecode.com/git/images/foregroundTarget/piggie2.png](http://wiki.sikuli-api.googlecode.com/git/images/foregroundTarget/piggie2.png)
```
Target t = new ForegroundTarget();
List<ScreenRegion> a = r.findAll(t);
```