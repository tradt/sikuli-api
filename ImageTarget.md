The typical usage of the Sikuli API consists of three steps:

  1. Define a screen region
  1. Specify a target
  1. Invoke `find()` to find the target in the screen region

An `ImageTarget` uses an image to specify a target to find in the second step. Below is an example of these three steps.

```
// Define a screen region (default to the entire screen on the default monitor)
ScreenRegion fullScreen = new DesktopScreenRegion();
// Specify a target (in this case an image target based on a file)
Target imageTarget = new ImageTarget(new File("targetImage.png"));
// Invoke find()
ScreenRegion foundRegion = s.find(imageTarget);
```

# Creating an Image Target #

The simplest method to create an `ImageTaget` is from an image file in the local filesystem.
```
Target target = new ImageTarget(new File("targetImage.png"));
```

Another method to create an `ImageTarget`  is from an URL, for example:
```
Target target = new ImageTarget(new URL("http://www.mysite.com/targetImage.png"));
```

The third method to create an `ImageTarget` is from a `BufferedImage`. A `BufferedImage` typically holds an image loaded in the memory. This method is useful when you want to manipulate an image before using that image as a target. For example, the code below loads an image, chooses a subimage, and uses the subimage to create an `ImageTarget`.
```
BufferedImage bigImage = ImageIO.read(new File("targetImage.png"));
BufferedImage smallImage = bigImage.subImage(50,50,100,100);
Target target = new ImageTarget(smallImage);	
```

# Controlling Image Recognition #

Sikuli performs _fuzzy_ image recognition. Fuzzy image recognition is important because it enables Sikuli to take a target and find a matching element on the screen even if the element looks slightly different from the target.

To control the degree of _fuzziness_ in image recognition, you can set the minimum score using the method `setMinScore()`. When a match is found, a score is assigned by the image recognition engine. This score indicates how similar the match is to the target specified. A high score close to 1 means the match must be very similar to the target specified. In this case, the image recognition is less fuzzy. A low score means a match only somehow similar is acceptable; image recognition is more fuzzy.

Here is an example of setting the minimum score to 0.7.
```
Target target = new ImageTarget(new File("targetImage.png"));
target.setMinScore(0.7);
```