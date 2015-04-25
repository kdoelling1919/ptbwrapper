* Testing

To use the toolbox, you have to first run SetupPsychtoolbox on your computer from inside the Psychtoolbox/toolbox folder.

Then, remember to restart matlab

Then, make sure that PTB is in the path, because the Setup function will delete it.

Finally, you have to restart matlab.

If you get a Java error, try 'PsychJavaTrouble'.
	[You should really make sure the classpath.txt file is writable, then run setup again, and restart matlab]

You can check to see if sound is working by trying to run BasicSoundOutputDemo
	* If a library fails to load, try copying it to the directories specified and then making sure they have loose enough permissions (i.e. in a terminal type: 'sudo chmod -R 777 directory')

Some random notes, for now:

•	Try ‘help PTB____’ to see how a function works.
•	If you get a Sync error before the program starts, try restarting
o	If that doesn’t work, add Screen(‘Preference’,’SkipSyncTests’,1) to your code.
•	Using absolute timing seems to be better than relative (i.e. get the start of the experiment or block and time everything from that (See Sample_Video)
•	Always use the PTBSetDebugging function until you’re pretty sure your program won’t crash. This will allow you to switch back to matlab easily. 
•	If the program has crashed and the screen is still up, try PTBCleanupExperiment
•	There is an option to set an arbitrary escape key. The will allow you to exit the program whenever you want and any response point.
•	Use PTBSetLogAppend to write conditions, item numbers, etc. to the log file.


 Check the comments for PTBSetupExperiment for relevant global variables to use.

Basic structure of PTB:

* The main idea is to do all the setup while a display is being shown. 


Top-level functions are PTBDisplay_______
	- These take arguments specific to the type of object being displayed
	- They they use Screen Draw commands to write the appropriate objects to the scree buffer
	- Also, they take a duration argument
	- After the buffer has been draw, they all call PTBDisplayScreen

PTBDisplayScreen
	- This function actually displays the new screen through the Screen Flip command
	- This will wait until PTBNextDisplayTime is reached or, if PTBWaitForKey is set, will wait for a key press
	- It will then return PTBLastDisplayTime as the estimate of when the screen was displayed
	- The duration is then set through PTBSetDuration

PTBSetDuration
	- Can take a key name, 'any' [for all keys], an absolute time stamp or a relative time stamp
	- Will set either the PTBWaitingForKey flag or PTBNextDisplayTime, or both

