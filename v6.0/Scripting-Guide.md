<h2 align="center">ERPLAB TOOLBOX SCRIPTING GUIDE </h2>
<h5 align="center">
By Steve Luck <br><br>
</h5>

**Important note: Because this is not commercial software, bugs are inevitable. In some cases, errors will occur leading to a message that instructs you to report the error to the EEGLAB developers.  If this happens, please report the error to us at erplab@erpinfo.org and not to the EEGLAB developers. ERPLAB has primarily been tested using EEG collected with a Biosemi ActiveTwo System, along with a smaller amount of testing using EEG collected with Neuroscan and EGI systems.**

Version 4.0 is intended to be backward compatible with version 3.0 with respect to scripting (but not with version 2.0).  Many parameter names have changed, but the old parameters should still work.  If you find cases where the old parameter name no longer works, please let us know.  One exception is that the pop_averager routine now calculates the standard error rather than the standard deviation, so this parameter has been changed from 'Stdev' to 'SEM'.

You can do a lot in ERPLAB without ever writing a script.  However, scripting can save you a lot of time by automating the processing of each subject.  That way, when a reviewer asks you to reanalyze all of your data with different EEG filter settings, you won't have to manually re-do every subsequent processing step for every subject.  In addition, scripting can allow you to perform analyses that aren't built into ERPLAB (or that have never been done before).

Scripting sounds complicated, but EEGLAB includes some features that make it easy, and ERPLAB inherits and extends those features.  Specifically, when you perform a set of steps in the GUI, these steps are equivalent to a set of script commands, and EEGLAB and ERPLAB save the equivalent scripts in a history.  You can then use the history to figure out the appropriate script commands.  The next section will explain how to access the history, and then we will go through some examples.

This Scripting Guide does not assume that you know anything about programming in Matlab (or in any other language). To make the best use of ERPLAB, however, it is useful to learn a little bit about Matlab programming. We will teach you a little here, but only a little. It would be a good idea for you to have a book on Matlab programming to learn more and to consult if you run into problems. There are several available Matlab books, and any of them would probably be fine. Our lab uses Mastering Matlab by Hanselman and Littlefield.

**Very Important Note: The histories and script examples given here won't look exactly like your histories and scripts, mainly because of differences in where the files and folders are stored.  If the scripts aren't working correctly, this is likely the source of the problem.  Also, Matlab often has problems when special characters (especially spaces) are in a filename or folder name.  So, if the same data are stored in a folder named 'Sample' that is inside a folder named 'ERPLAB' that is inside a folder named 'In Progress (new)', you may need to change the name of the 'In Progress (new)' folder to 'In_Progress_new'.**

## Table of Contents
---
* [Getting Started With This Scripting Guide](./Getting-Started-With-This-Scripting-Guide)
 * [Downloading the example data](./Getting-Started-With-This-Scripting-Guide#downloading-the-example-data)
 * [Accessing the history](./Getting-Started-With-This-Scripting-Guide#accessing-the-history)
 * [Organizing your files](./Getting-Started-With-This-Scripting-Guide#organizing-your-files)
 * [Keeping the GUI synced with your scripts](./Getting-Started-With-This-Scripting-Guide#keeping-the-gui-synced-with-your-scripts)
 * [If you already know a little about scripts or programming…](./Getting-Started-With-This-Scripting-Guide#if-you-already-know-a-little-about-scripts-or-programming)
* [Example 1: The World's Simplest EEGLAB/ERPLAB Script](./Example-1:-The-World's-Simplest-EEGLAB-ERPLAB-Script)
 * [Getting started](./Example-1:-The-World's-Simplest-EEGLAB-ERPLAB-Script#getting-started)
 * [Loading a dataset with the GUI to create a history](./Example-1:-The-World's-Simplest-EEGLAB-ERPLAB-Script#loading-a-dataset-with-the-gui-to-create-a-history)
 * [Executing a command from the command line](./Example-1:-The-World's-Simplest-EEGLAB-ERPLAB-Script#executing-a-command-from-the-command-line)
 * [Using eeglab redraw to synchronize with the GUI](./Example-1:-The-World's-Simplest-EEGLAB-ERPLAB-Script#using-pop_loadset-and-eeglab-redraw-to-synchronize-with-the-gui)
 * [Creating and executing the script](./Example-1:-The-World's-Simplest-EEGLAB-ERPLAB-Script#creating-and-executing-the-script)
* [Example 2: An Even Simpler EEGLAB Script](./Example-2:-An-Even-Simpler-EEGLAB-Script)
* [Example 3: A Simple Script That Actually Does Something Useful](./Example-3:-A-Simple-Script-That-Actually-Does-Something-Useful)
 * [Getting Started](./Example-3:-A-Simple-Script-That-Actually-Does-Something-Useful#getting-started)
 * [Doing the processing steps with the GUI to create a history](./Example-3:-A-Simple-Script-That-Actually-Does-Something-Useful#doing-the-processing-steps-with-the-gui-to-create-a-history)
 * [Using the history to make a script](./Example-3:-A-Simple-Script-That-Actually-Does-Something-Useful#using-the-history-to-make-a-script)
* [Example 3b: Modifying the Script to Work for Different Subjects](./Example-3b:-Modifying-the-Script-to-Work-for-Different-Subjects)
 * [Learning a little Matlab trick](./Example-3b:-Modifying-the-Script-to-Work-for-Different-Subjects#learning-a-little-matlab-trick)
 * [Adding subject and path variables to the script](./Example-3b:-Modifying-the-Script-to-Work-for-Different-Subjects#adding-subject-and-path-variables-to-the-script)
 * Averaging from EEG instead of ALLEEG
 * [Putting the bin descriptor file in the parent folder](./Example-3b:-Modifying-the-Script-to-Work-for-Different-Subjects#putting-the-bin-descriptor-file-in-the-parent-folder)
 * [Changing the path for the electrode locations file](./Example-3b:-Modifying-the-Script-to-Work-for-Different-Subjects#changing-the-path-for-the-electrode-locations-file)
* [Example 3c: Looping Through Multiple Subjects](./Example-3c:-Looping-Through-Multiple-Subjects)
 * [Cell arrays](./Example-3c:-Looping-Through-Multiple-Subjects#cell-arrays)
 * [The fprintf() command](./Example-3c:-Looping-Through-Multiple-Subjects#the-fprintf-command)
 * [Loops](./Example-3c:-Looping-Through-Multiple-Subjects#loops)
 * [Adding a loop to the script](./Example-3c:-Looping-Through-Multiple-Subjects#adding-a-loop-to-the-script)
* [Example 4: A Complete Data Processing Script](./Example-4:-A-Complete-Data-Processing-Script)
* [Hints About Debugging Your Scripts](./Hints-About-Debugging-Your-Scripts)
=======
 * [Putting the bin descriptor file in the parent folder](./Example-3b:-Modifying-the-Script-to-Work-for-Different-Subjects#putting-the-bin-descriptor-file-in-the-parent-folder)
 * [Changing the path for the electrode locations file](./Example-3b:-Modifying-the-Script-to-Work-for-Different-Subjects#changing-the-path-for-the-electrode-locations-file)
* [Example 3c: Looping Through Multiple Subjects](./Example-3c:-Looping-Through-Multiple-Subjects)
 * [Cell arrays](./Example-3c:-Looping-Through-Multiple-Subjects#cell-arrays)
 * [The fprintf() command](./Example-3c:-Looping-Through-Multiple-Subjects#the-fprintf-command)
 * [Loops](./Example-3c:-Looping-Through-Multiple-Subjects#loops)
 * [Adding a loop to the script](./Example-3c:-Looping-Through-Multiple-Subjects#adding-a-loop-to-the-script)
* [Example 4: A Complete Data Processing Script](./Example-4:-A-Complete-Data-Processing-Script)
* [Hints About Debugging Your Scripts](./Hints-About-Debugging-Your-Scripts)