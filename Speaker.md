## Example 1: `Speaker` ##

Goal: Say "click" before clicking a target.

Sound: http://wiki.sikuli-api.googlecode.com/git/sounds/click.wav
```
ScreenRegion r = ... some find() ...

// say "click"
Speaker speaker = new DesktopSpeaker();
speaker.play(new URL("http://wiki.sikuli-api.googlecode.com/git/sounds/click.wav"));

// click the region
Mouse mouse = new DesktopMouse();
mouse.click(r.getCenter());
```

## Example 2: `SpeakerPlayable` ##

Suppose we want to demonstrate a sequence of clicks on a live interface while providing voice narration.
We can first define a utility function as follows:
```
void demonstrate(URL targetURL, URL soundURL){
	ScreenRegion s = new DesktopScreenRegion();
	
	// find the target
	Target target = new ImageTarget(targetURL);
	ScreenRegion r = s.wait(target,5000);

	Canvas canvas = new DesktopCanvas();
	canvas.addBox(r);		
	// display the canvas while the speaker is playing the given sound
	canvas.displayWhile(new SpeakerPlayable(soundURL));

	// click the region
	Mouse mouse = new DesktopMouse();
	mouse.click(r.getCenter());
}
```

This function will click the target specified by `targetURL` and play the sound file
specified by `soundURL`. We use `SpeakerPlayable` as an argument to `canvas.displayWhile`
in order to play the voice narration while displaying a box around each target.

Below is an example of using `demonstrate` to demonstrate a three-step clicking sequence.

### Step 1: Click "Videos" ###

![http://wiki.sikuli-api.googlecode.com/git/images/speaker/step1.png](http://wiki.sikuli-api.googlecode.com/git/images/speaker/step1.png)

| Target | ![http://wiki.sikuli-api.googlecode.com/git/images/speaker/videos.png](http://wiki.sikuli-api.googlecode.com/git/images/speaker/videos.png) |
|:-------|:--------------------------------------------------------------------------------------------------------------------------------------------|
| Sound  | http://wiki.sikuli-api.googlecode.com/git/sounds/click-videos.wav                                                                           |

```
targetURL = new URL("http://wiki.sikuli-api.googlecode.com/git/images/speaker/videos.png");
soundURL = new URL("http://wiki.sikuli-api.googlecode.com/git/sounds/click-videos.wav");
demonstrate(targetURL, soundURL);
```

### Step 2: Click "Gaming" ###

![http://wiki.sikuli-api.googlecode.com/git/images/speaker/step2.png](http://wiki.sikuli-api.googlecode.com/git/images/speaker/step2.png)

| Target | ![http://wiki.sikuli-api.googlecode.com/git/images/speaker/gaming.png](http://wiki.sikuli-api.googlecode.com/git/images/speaker/gaming.png) |
|:-------|:--------------------------------------------------------------------------------------------------------------------------------------------|
| Sound  | http://wiki.sikuli-api.googlecode.com/git/sounds/click-gaming.wav                                                                           |

```
targetURL = new URL("http://wiki.sikuli-api.googlecode.com/git/images/speaker/gaming.png");
soundURL  = new URL("http://wiki.sikuli-api.googlecode.com/git/sounds/click-gaming.wav"); 
demonstrate(targetURL, soundURL);
```

### Step 3: Click "Play" ###
![http://wiki.sikuli-api.googlecode.com/git/images/speaker/step3.png](http://wiki.sikuli-api.googlecode.com/git/images/speaker/step3.png)

| Target | ![http://wiki.sikuli-api.googlecode.com/git/images/speaker/play.png](http://wiki.sikuli-api.googlecode.com/git/images/speaker/play.png) |
|:-------|:----------------------------------------------------------------------------------------------------------------------------------------|
| Sound  | http://wiki.sikuli-api.googlecode.com/git/sounds/click-play.wav                                                                         |

```
targetURL = new URL("http://wiki.sikuli-api.googlecode.com/git/images/speaker/play.png");
soundURL  = new URL("http://wiki.sikuli-api.googlecode.com/git/sounds/click-play.wav"); 
demonstrate(targetURL, soundURL);
```

`YouTube` video of this three step demonstration with narration:

<a href='http://www.youtube.com/watch?feature=player_embedded&v=pN4aXkZaOgY' target='_blank'><img src='http://img.youtube.com/vi/pN4aXkZaOgY/0.jpg' width='425' height=344 /></a>