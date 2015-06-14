# Requirement #
JRuby 1.6 and above

# Hello World example #
```
require 'sikuli'

# Open the main page of Google Code in the default web browser
browse "http://code.google.com/"

# Create a screen region representing the default monitor in full screen
s = ScreenRegion.new

# Wait for the target to become visible on the screen for at most 5 seconds
# Once the target is visible, it returns a screen region object corresponding
# to the region occupied by this target.
r = s.wait "http://code.google.com/images/code_logo.gif", 5000

# Display "Hello World" next to the found target for 3 seconds 
r.label "Hello World", 3000

#  Click the center of the found target
Mouse.click r.center
```

1. Use a text editor to create `HelloWorld.rb` with the code above.

2. Download `sikuli-api.jar` and `sikuli.rb` from the Downloads tab

3. Put the two files in the same directory as `HelloWorld.rb`

4. Run
```
$ jruby HelloWorld.rb
```