## Example 2: An Even Simpler EEGLAB Script
_Note: A complete version of this script is available in **Test_Data > Script_Examples > Script2.m**._

I know I said that the last example was the world's simplest EEGLAB script, but that was a little fib. Now we're going to make that script even simpler to show you a little more about Matlab commands.  Remember that your previous script looked something like this:  

    EEG = pop_loadset('filename','S1_EEG.set','filepath','/Users/luck/Documents/Software_Development/ERPLAB_Toolbox/Test_Data/S1/');
    [ALLEEG, EEG, CURRENTSET] = eeg_store( ALLEEG, EEG, 0 );
    eeglab redraw

 

The first line says to run the **pop_loadset** command and save the result in the variable named **EEG**.  (You won't need to worry about the nature of the EEG structure unless you start doing advanced scripting.)

The complicated part of the **pop_loadset** command is the stuff between the parentheses.  In Matlab (like most computer languages), you send various pieces of information to a command by putting them between the parentheses.  Each piece of information is called an _argument_ (sometimes called a _parameter_), and the arguments are separated by parentheses.  For example, a simple Matlab command would be  **X = power(2, 3)**, which would compute 2 to the 3rd power (23) and assign this value to the variable **X**.  The **power()** function is sent two arguments, the base (2 in this example) and the exponent (3 in this example).  For many commands, the arguments are numbers or text strings that must occur in a particular order, and you need to remember the order to avoid computing the wrong thing (e.g., if the 2 and 3 were reversed, we would get 32 instead of 23).  Many EEGLAB and ERPLAB commands try to make things simpler by having you specify pairs of arguments, the first indicating what the argument represents and the second indicating the value.  For example, in our very simple script, the first argument sent to pop_loadset is 'filename' and the second is **'S1_EEG.set'**.  This tells the **pop_loadset** command that the filename is **S1_EEG.set**.  (Note that these are enclosed in single quote marks to indicate that they are text strings; without the quote marks, Matlab would think they are variables.)  With this approach, the arguments can be presented in any order (as long as the first in each pair begins with the name of the argument and the second is the value).

To learn about the arguments for a given command, you can type **help _commandname_** in the command window for a description of the command and its arguments.  Try typing **help pop_loadset** and see what it says about this command. 

In our simple script, we're sending both the filename and the path to **pop_loadset()**.  We can simplify the script by getting rid of the specification of the path.  To do this, edit the **myscript.m** file that you created before, deleting the **'filepath'** argument and the path that follows it.  The result should look like this:  

    EEG = pop_loadset('filename', 'S1_EEG.set');  

 

If you don't specify the path, how will EEGLAB know where to look for the **S1_EEG.set** file?  Well, it will first look in Matlab's current folder.  You may recall that, at an earlier step, you set the current folder to be the **S1** folder that contains the **S1_EEG.set** file. Consequently, EEGLAB should be able to find the file in the current folder when you run the script. 

Try running the newly modified script and make sure that it still works.  If it doesn't work, check the current folder (which is indicated near the top of the command window; you can also type **pwd** [_print working directory_] on the command line to see what the current folder is).  If necessary, change the current folder so that it is the one that contains the **S1_EEG.set** file.

If EEGLAB can't find the file in the current folder, it will look through its path for the file.  You can experiment with this by moving **S1_EEG.set** to other locations that are in (or not in) your path.

If you still had EEGLAB running after running the script described in the previous page of this documentation, you may notice that **S1_EEG** is listed twice in the **Datasets** menu. This happened because **ALLEEG** still had **S1_EEG** in it when you ran the script. When your script called the **eeg_store** function, it told it to store the current EEG in position 0 (zero) of the **ALLEEG** structure. There is no position 0, so eeg_store figured that you just wanted to append it onto the end of **ALLEEG**. If you want to make sure that it's stored in the first position in **ALLEEG**, you can specify position 1 by calling the function like this: **[ALLEEG, EEG, CURRENTSET] = eeg_store( ALLEEG, EEG, 1 );**

----
<table style="width:100%">
  <tr>
    <td><a href="./Example-1:-The-World's-Simplest-EEGLAB-ERPLAB-Script"> << Example 1: The World's Simplest EEGLAB ERPLAB Script  </a></td>
    <td><a href="./Scripting-Guide"> Scripting Guide</a></td>
    <td><a href="./Example-3:-A-Simple-Script-That-Actually-Does-Something-Useful">  Example 3: A Simple Script That Actually Does Something Useful >>  </a></td>
  </tr>
</table>
