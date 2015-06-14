<a href='http://www.youtube.com/watch?feature=player_embedded&v=lbC4-FajMx8' target='_blank'><img src='http://img.youtube.com/vi/lbC4-FajMx8/0.jpg' width='425' height=344 /></a>

<font size='4'><b>What is Sikuli-Fuzz?</b></font>

Sikuli Fuzz is a tool to automatically test graphical user interfaces (GUI) in an Android Virtual Device (AVD) setting.

<font size='4'><b>What is Fuzz testing?</b></font>

Fuzz testing is a technique to test software by applying random actions to the software and checking the resulting output for errors. Fuzzing attempts to crash a program by providing corrupted data to test against issues such as memory leaks or mode confusion.

<font size='4'><b>How does Sikuli-Fuzz work?</b></font>

Sikuli Fuzz tests Android applications in AVDs by executing a number of keyboard and mouse events that are user defined or randomly generated. The resulted images are then saved in a directory called "resultImages" for validation.


<font size='4'><b>How is Sikuli-Fuzz related to Android's UI Exerciser Monkey</b></font>

Both tools test apps in an Android Emulator environment. However Sikuli-fuzz is computer vision focused meaning that it uses the visual properties of a certain app to automatically execute actions and interact with the app.

<font size='4'><b>Setting up Sikuli-Fuzz</b></font>

Sikuli fuzz requires a directory called "screenShots" that consists of the following:
<ol>
<blockquote><li>The simulator screen named "sim_screen" for the screen area of where Sikuli-Fuzz can execute.</li>
<li>The application icon to be tested named "app_icon" for Sikuli-Fuzz to know what app to test.</li>
<li>The back icon named "back_icon" for returning to the main screen.</li>
</ol></blockquote>

<font size='4'><b>How can I run Sikuli-Fuzz?</b></font>

```
$ java -jar sikuli-fuzz-0.9.0.jar [-options] 
```
where options include:
```
java -jar sikuli-fuzz-0.9.0.jar -h
  -h			 help
  -help			 help
  -t <text>		 specifies text to type.
  -type <text>		 specifies text to type.
  -s <direction>	 1 to scroll up and -1 for down
  -scroll <direction>	 1 to scroll up and -1 for down
  -r <num_of_tasks>	 number of random tasks to execute
  -random <num_of_tasks> number of random tasks to execute
  -ct <wait_time>	 wait time after clicks in milliseconds
  -clicktime <wait_time> wait time after clicks in milliseconds
  -w <wait_time>	 execute a wait event in milliseconds
  -wait <wait_time>	 execute a wait event in milliseconds
  -b			 do not click on back button after execution
  -back			 do not click on back button after execution

  -c <clicks>
  -click <clicks>
	  specify the number of clicks to execute.
	  The program will click on any visible pattern <clicks> times.
	 Each click is executed until the screen is changed.
```

<font size='4'><b>How does Sikuli-fuzz know not to click on blank screen area?</b></font>

Sikuli-fuzz checks the view of the app to find any dissimilarities and if found, will attempt to click them.

<font size='4'><b>Can Sikuli-Fuzz be applied to non-Android apps?</b></font>

Sikuli-fuzz has not been tested on non-Android apps yet but theoretically the concept should be applicable to any app.