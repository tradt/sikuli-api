<a href='http://www.youtube.com/watch?feature=player_embedded&v=22yNhSgplDg' target='_blank'><img src='http://img.youtube.com/vi/22yNhSgplDg/0.jpg' width='425' height=344 /></a>

## What’s sikuli-slides? ##

sikuli-slides is a new tool that enables you to automate and test graphical user interfaces (GUI) using presentation slides by adding screenshots and annotating them. sikuli-slides enables users to automate GUIs and produce an interactive screenshot by screenshot tutorials without having to write code.

## What’s sikuli-slides for? ##

sikuli-slides can be used to automate and test anything you see on the screen using your presentation slides. sikuli-slides is useful for automating repetitive tasks and teaching other people how to use a website or a software feature in a visual and interactive way. For example, sikuli-slides can be used to perform the actions that users want to do when they follow screenshot by screenshots tutorials. It can be used to control your computer and show you how to use a particular application or a feature at real time.

## How does sikuli-slides work? ##

You create a `PowerPoint` presentation file that consists of a sequence of screenshots of a GUI and specify the actions to execute on each GUI element such as a button on the screenshot. When you are done with creating your slides, save the presentation file as .pptx file and open it in sikuli-slides. sikuli-slides will open the file and determines what targets to find on the screen and what actions to execute based on the created presentation slides.

## What actions can I perform in sikuli-slides? ##

You can perform any of the following input events: left click, right click, double click, keyboard typing, and drag and drop.

## How to represent the different actions? ##
Insert a text box that contains the action to be executed and draw any shape around the target on the screenshot. The accepted text values that can be added to the text box include: click, right click, double click, drag and drop, exist, not exist, browser.

| **Action** | **Text box value (case insensitive)** |
|:-----------|:--------------------------------------|
| Left click	| Click                                 |
| Right click	| Right Click                           |
| Double Click	| Double Click                          |
| Keyboard Typing	| Type                                  |
| Drag and drop | Drag and drop                         |
| Open default browser	| Browser                               |

Prior to sikuli-slides 1.2.0, sikuli-slides uses the following special shapes to represent each action.
| **DEPRECATED in 1.2.0** | **DEPRECATED in 1.2.0**|
|:------------------------|:-----------------------|
| **Action**              | **Shape**              |
| left click	             | Rectangle              |
| right click	            | Oval                   |
| double click	           | Frame                  |
| typing	                 | Textbox that contains the text to be typed |
| drag and drop           | Rounded rectangle connected by an arrow |
| open default browser	   | Cloud that contains the URL to be opened |

## How can I write my code in sikuli-slides? ##

There is no need to write a single line of code in sikuli-slides, in fact your code is your presentation slides.

## How can I run my presentation file in sikuli-slides? ##

usage:
```
$ java -jar sikuli-slides-1.2.0.jar presentation_file.pptx [-h] [-oldsyntax] [-p <precision>] [-w <max_wait_time>]
```
```
$ sikuli-slides -- help
     -h                   help
     -oldsyntax           Forces the system to use the old syntax that uses special shapes to represent actions. The
                          syntax is based on the following annotations: Rectangle shape: left click. Rounded rectangle:
                          drag and drop. Frame: double click. Oval: right click. Text Box: Keyboard typing. Cloud: open
                          URL in default browser.
     -p <precision>       The precision value to control the degree of fuzziness of the image recognition search. It is a
                          10-point scale where 1 is the least precise search and 10 is the most precise search. (default
                          is 7).
     -w <max_wait_time>   The maximum time to wait in milliseconds to find a target on the screen (default 15000 ms).
```

## sikuli-slides 1.2.0 - What's new? ##
  * New syntax: Use any shape as a target image and text box as an input action. You can specify the user input action in a separate text box and the target images using any shape, so there is no need to memorize the meaning of each shape. This makes sikuli-slides more easy and customizable so users can customize the meaning of each shape.
  * Add multiple targets per slide support but with one input action per slide. For example, you can perform left click action on multiple targets in one slide.
  * Set the order of performing input actions. If you have multiple targets on the screen, you can specify the order in which the action is executed by inserting the numeric order into the shape.
  * Sound support: Play sound while running your visual automation. This allows you to add more informative and interactive experience for your automation as well as to test voice recognition applications.
  * Text annotation: Display an overlay text on the screen. This can be an effective way to display informative text on the screen.
  * Add new visual testing operations that can be used to know whether something is visible on the screen or not.
    * Exist: check whether the target image is visible on the screen.
    * Not Exist: check whether the target image is invisible on the screen.


## sikuli-slides 1.1.0 - What's new? ##
  * Detect identical targets on the screen: added new algorithm that uniquely identifies a target among identical targets on the screen such as checkboxes, radio buttons, etc.
  * Added double click action using frame shape.
  * Bug fixes.