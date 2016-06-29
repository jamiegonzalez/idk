## Hints About Debugging Your Scripts
Debugging is a very important skill that develops gradually over time. You will probably spend as much (or more) time debugging your scripts than initially writing them. I can guarantee that you will hate debugging, but you need to think of it as an integral part of programming. Indeed, you will eventually learn to design your programs in a way that makes debugging easier.

Entire books have been written on debugging. Here I will describe just a few principles. Matlab includes sophisticated debugging tools, and I encourage you to learn about them once you've gotten some experience. But here I am going to describe some very simple approaches that are designed for beginners. Once you've learned these simple approaches, I encourage you to learn about Matlab's debugging tools.

The most important piece of advice is that you should think about debugging as being analogous to scientific hypothesis-testing. When an error occurs, you look at the data (your script, its output, and any error messages that were produced), generate a hypothesis about what is causing the error, and conduct experiments (make changes to the code) to test this hypothesis. Don't just flail around trying a bunch of things and hoping that they will work. Design a set of tests that provide useful data about the nature of the bug, and gradually hone in on the exact problem.

### An example
Open the script named **Bugs1.m**, which is located in **Test_Data > Script_Examples**. Make sure that EEGLAB is running, and then run the **Bugs1.m** script. This is just a version of **Script3b.m**, but with a bug. When you run it, you should see an error message in the command window that looks something like this:  

    pop_loadset(): loading file /Users/luck/Documents/Software_Development/ERPLAB_Toolbox/Test_Data/S1 /S1_EEG.set ...
    ??? Error using ==> load
    Unable to read file /Users/luck/Documents/Software_Development/ERPLAB_Toolbox/Test_Data/S1 /S1_EEG.set: No such file
    or directory.

    Error in ==> pop_loadset at 107
    TMPVAR = load(filename, '-mat');

    Error in ==> Bugs1 at 12
    EEG = pop_loadset('filename', [subject '_EEG.set'],'filepath', subject folder);  

 

The first line (pop_loadset...) is just the usual EEGLAB output when the **pop_loadset** command is invoked. This is not an error message, but it might still be useful in seeing what EEGLAB was trying to do when the error occurred.

The next line tells you that an error was encountered. The next several lines provide information about the sequence of events that happened when the error was detected. First, a Matlab function called **load** initially determined that an error occurred, and it generated a message saying that it was unable to read the file (and it gives the whole path to the file). The **load** function was called on line 107 of an EEGLAB function called **pop_loadset**, and the next part of the error message tells yout this. It also tells you what the line of the script in **pop_loadset** looked like (TMPVAR = load(filename, -=mat');). The **pop_loadset** function was called on line 12 of the **Bugs1** script, and the next part of the error message tells you that and shows what this line of **Bugs1.m** looked like.

This information is the initial set of data that you will use to generate a hypothesis about the nature of the bug.

Matlab's error message might seem to imply that the problem arises due to the **load** function, the **loadset** function, or perhaps line 12 of **Bugs1.m**. However, the error messages are really telling you when Matlab encountered a problem, and the cause of the problem is usually something that happened before the problem was detected by Matlab. By analogy, if you wake up one morning with a flu bug, the cause of the flu did not happen when you first felt sick. The cause occurred a few days earlier when the virus first entered your body, but you couldn't detect the virus until it had a chance to grow and spread. So, when you look at a Matlab error message, the problem might be on the line of your code indicated by the error message, but it is usually something that happened earlier in the script.

The information printed in the command window gives you a broad hypothesis about the cause of the error: It probably has something to do with the information that you are sending the **pop_loadset** function. This is a reasonable hypothesis, because it is the part of your script that was running when the error occurred. Of course, it's always possible that the bug is in the **pop_loadset** routine or even in Matlab's **load** function. However, you should usually start by assuming that you caused the problem and not EEGLAB or Matlab.

### Adding debugging code
You might be able to determine the nature of the bug by looking at Matlab's output or by staring at the script for a few minutes. But often you won't be able to figure it out right away. So the next step is to run some experiments that will allow you to collect additional data and refine your hypothesis about the cause of the error.

In many cases, bugs arise because a variable has an incorrect value (either because you put in the wrong value directly or because the value was computed by an inccorrect equation). The simplest thing you can do to collect more data is to look at the values of your variables. And the simplest way to do this is just to delete the semicolon at the end of the line where a variable is defined or computed. When you do this, Matlab will print the value of the variable on the command line when it reaches the relevant part of your script.

To see how this works, open **Bugs1.m** and remove the semicolons on the three lines near the top that define the **subject**, **parentfolder**, and **subjectfolder** variables. Run the script. You should see something like the following in the command window (followed by the error messages):  

    subject =

    S1


    parentfolder =

    /Users/luck/Documents/Software_Development/ERPLAB_Toolbox/Test_Data/


    subjectfolder =

    /Users/luck/Documents/Software_Development/ERPLAB_Toolbox/Test_Data/S1 /  

 

Why are we printing the values of these three variables? Because they are all defined before the error occurs on line 12, and they all have an influence on the information that is sent by the script to **pop_loadset**. Do you see the error? It's a little difficult to see.

There is a more powerful way to print the values of variables (along with other debugging text), which is to use Matlab's **fprintf** function. A brief description of **fprintf** can be found by [clicking here](https://github.com/lucklab/erplab/wiki/Example-3c:-Looping-Through-Multiple-Subjects#the-fprintf-command), and more details can be found in the Matlab documentation.

To see how this works, put the semicolons back on the lines that define the **subject**, **parentfolder**, and **subjectfolder** variables, and add the following line to the script right above the call to **pop_loadset**:  

    fprintf('subject="%s", filename="%s", subjectfolder="%s"\n', subject, [subject '_EEG.set'], subject folder);  

 

Now run the script. The first thing you will see in the command window is this:  

    subject="S1", filename="S1_EEG.set", subjectfolder="/Users/luck/Documents/Software_Development/ERPLAB_Toolbox/Test_Data/S1 /"  

 

The double-quote marks around the variable values should make it easier to see that there is an accidental space between "S1" and "/" in the **subjectfolder** variable. Take a look at the initial definition of this variable in the script. Can you see where this extra space comes from? Here's the relevant line of the script:  

    subjectfolder = [parentfolder subject ' /'];  

 

If you look closely, you will see that it contains the string **' /'** (a space followed by a slash). This is the origin of the error.

Now you have a very specific hypothesis about the source of the error. You can test this hypothesis by deleting the extra space in the line that defines the **subjectfolder** variable. Run the script after deleting the extra space, and verify that the error is now gone.

This sort of tiny, hard-to-see error is often the cause of bugs in scripts. You might spend an hour staring at the code, only to realize that one stupid little character is the problem. This is very frustrating, but you can save a lot of time and frustration by taking a careful, systematic, hypothesis-testing approach to debugging. And don't forget that debugging is an essential skill that you must learn to be a good programmer. Good luck!