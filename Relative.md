## `ScreenRegion` relative to `ScreenRegion` ##

![http://wiki.sikuli-api.googlecode.com/git/images/relative/regionRight.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/regionRight.png)
```
ScreenRegion s = Relative.to(r).right(100).getScreenRegion();
```


---


![http://wiki.sikuli-api.googlecode.com/git/images/relative/regionLeft.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/regionLeft.png)

```
ScreenRegion s = Relative.to(r).left(100).getScreenRegion();
```

---

![http://wiki.sikuli-api.googlecode.com/git/images/relative/regionAbove.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/regionAbove.png)

```
ScreenRegion s = Relative.to(r).above(30).getScreenRegion();
```

---

![http://wiki.sikuli-api.googlecode.com/git/images/relative/regionBelow.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/regionBelow.png)

```
ScreenRegion s = Relative.to(r).below(30).getScreenRegion();
```

---

![http://wiki.sikuli-api.googlecode.com/git/images/relative/regionWider.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/regionWider.png)

```
ScreenRegion s = Relative.to(r).wider(10).getScreenRegion();
```

---

![http://wiki.sikuli-api.googlecode.com/git/images/relative/regionTaller.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/regionTaller.png)

```
ScreenRegion s = Relative.to(r).taller(10).getScreenRegion();
```

---

## `ScreenLocation` relative to `ScreenRegion` ##

![http://wiki.sikuli-api.googlecode.com/git/images/relative/regionCenter.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/regionCenter.png)

```
ScreenLocation p = Relative.to(r).center().getScreenLocation();
```

---


![http://wiki.sikuli-api.googlecode.com/git/images/relative/regionTopLeft.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/regionTopLeft.png)

```
ScreenLocation p = Relative.to(r).topLeft().getScreenLocation();
```

---

![http://wiki.sikuli-api.googlecode.com/git/images/relative/regionTopRight.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/regionTopRight.png)

```
ScreenLocation p = Relative.to(r).topRight().getScreenLocation();
```

---

![http://wiki.sikuli-api.googlecode.com/git/images/relative/regionBottomRight.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/regionBottomRight.png)

```
ScreenLocation p = Relative.to(r).bottomRight().getScreenLocation();
```

---

![http://wiki.sikuli-api.googlecode.com/git/images/relative/regionBottomLeft.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/regionBottomLeft.png)

```
ScreenLocation p = Relative.to(r).bottomLeft().getScreenLocation();
```

---

## `ScreenLocation` relative to `ScreenLocation` ##

![http://wiki.sikuli-api.googlecode.com/git/images/relative/locationLeft.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/locationLeft.png)

```
ScreenLocation p = Relative.to(x).left(100).getScreenLocation();
```

---

![http://wiki.sikuli-api.googlecode.com/git/images/relative/locationRight.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/locationRight.png)

```
ScreenLocation p = Relative.to(x).right(100).getScreenLocation();
```

---

![http://wiki.sikuli-api.googlecode.com/git/images/relative/locationAbove.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/locationAbove.png)

```
ScreenLocation p = Relative.to(x).above(30).getScreenLocation();
```

---

![http://wiki.sikuli-api.googlecode.com/git/images/relative/locationBelow.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/locationBelow.png)

```
ScreenLocation p = Relative.to(x).below(30).getScreenLocation();
```

---

## Chaining ##

![http://wiki.sikuli-api.googlecode.com/git/images/relative/chaining1.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/chaining1.png)

```
ScreenLocation p = Relative.to(r).right(100)
	.below(30).bottomRight().right(100)
	.getScreenLocation();
```

---

![http://wiki.sikuli-api.googlecode.com/git/images/relative/chaining2.png](http://wiki.sikuli-api.googlecode.com/git/images/relative/chaining2.png)

```
ScreenLocation p = Relative.to(r).center()
	.right(100).above(30)
	.getScreenLocation();
```

---


