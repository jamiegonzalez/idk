## Example 3c: Looping Through Multiple Subjects
_Note: A complete version of this script is available in **Test_Data > Script_Examples > Script3c.m**._

The script you made in the previous step can process the data for one subject at a time.  To process the next subject, you need to open the script, change the value of the **subject** variable, and then run the script again.  There must be an easier way!

Of course, there is an easier way.  You can create a list of all the subject folder names in your script and loop through them.  To understand how to do this, we first need to explain two Matlab concepts, _cell arrays_ and _looping_.  We also need to go over a useful function, **fprintf()**, that provides a convenient way to print information to the command window so that you can monitor the operation of a script.  If you already understand these concepts, feel free to skip ahead to the part where we talk about the actual script.

### Cell arrays
An array is simply a variable that holds a list of other variables.  Ordinarily, all of the variables in an array must be the same type and size (e.g., all numbers, or all 3-character strings).  However, a _cell array_ can hold a list of miscellaneous variables without any real constraints.  This makes it quite flexible.

To see how a cell array works, go to the Matlab command line and type the following:  

    x = {7, 'hi', 'dude', 1.1};  

 

You have now created a cell array named **x**, which contains a list of 4 items: the number 7, the string 'hi', the string 'dude', and the number 1.1.  To access the 4th element in this list, you would refer to **x{4}**.  For example, type **x{4} + 1** into the command line (not followed by a semicolon).  The result should look like this:  

    >> x{4} + 1

    ans =

        2.1000  

 

This is telling you that the answer to the equation **x{4} + 1** is 2.1000 (because **x{4}** is equal to 1.1).

Now type the following into the command window:  

    subject_list = {'S1', 'S2', 'S3', 'S4', 'S5', 'S6'};

    numsubjects = length(subject_list);  

 

You have now created a cell array named **subject_list** that contains the names of all the subject folders for our example experiment.  You have also created a variable named **numsubjects** that is equal to the number of elements in the cell array (which is 6 in this example).  You already knew there were 6 subjects in the experiment, so why compute it with the **length** function?  The answer is that if you add another subject to the **subject_list** variable, the **numsubjects** variable will automatically reflect the new number of subjects, which might prevent you from making an error later.

Here's a very very **VERY** important programming hint: You should not ordinarily have "raw" numbers embedded in your scripts (unless they are things like 0's or 1's that tell a command whether a given option should be off or on).  Whenever possible, values should be assigned to variables (with informative names, like "numsubjects") at the top of the script or computed from other variables.  This is a little bit of extra work initially, but it dramatically reduces the likelihood of bugs (especially as a script evolves over a period of weeks or months), and it can save you hours and hours of mindnumbing debugging later.

Now that you have created the **subject_list** cell array, practice accessing various items from this list (e.g., by typing things like **subject_list{3}** on the command line).

### The fprintf() command
As you have seen, it is possible to print the output of a command or the value of a variable in the command window by just giving the command or variable name without a semicolon at the end.  But sometimes it's useful to print something a little more complex.  You can use the **fprintf()** function for this.  You can look up the details in a Matlab book, but the basic idea is that you send this function a _formatting string_ and then a bunch of variables, and it then prints the variables to the command window (or to a file) in a manner that is specified by the formatting string.  To see how this works, try typing the following into the command window:  

    fprintf('%s\n', subject_list{1});  

 

Matlab should then print **S1** in the command window (because **S1** is the first element in the **subject_list** cell array).  In this example, the **%s** tells **fprintf** that the variable is a string. You can also use **%f** to print a number like 2.4.387[the **f** stands for "floating point number"] or **%d** to print a whole number like 34 [the **d** stands for "decimal number'].  The **\n** tells **fprintf** to print a newline (return) at the end (the other common special character is **\t**, which means TAB).  Here's a slightly more complex example:  

    fprintf('subject %d is named "%s"\n', 1, subject_list{1});  

 

This will print **subject 1 is named "S1"** in the command window.  This shows that you can use either values or variables.  But if you want to use a string, make sure to enclose it in single quote marks.

### Loops
Loops are a very important programming element that are present in almost every programming language.  A loop is basically an element of a script that causes a part of the script to repeat multiple times until some condition is met.  Here, we will use a very common type of loop called a **For** loop.  A **For** loop involves a variable that increments each time through the loop, and the loop ends when this variable reaches a specific value.  The easiest way to see this is with an example.  Make sure that you still have **subject_list** and **numsubjects** defined from the previous step.  Now type the following in the command window:  

    for s=1:numsubjects

    fprintf('subject %d: %s\n', s, subject_list{s});

    end;  

 

This tells Matlab to start by creating a variable named **s** and setting its value to 1.  Then Matlab iterates through the **fprintf** command, incrementing the value of **s** by 1 at the end of each iteration, until **s** is greater than **numsubjects**.  We only have one command here, but you could have many lines of commands between the for line and the **end** line.

Once you finish typing **end**; and press RETURN or ENTER, you should see the following in the command window:  

    subject 1: S1

    subject 2: S2

    subject 3: S3

    subject 4: S4

    subject 5: S5

    subject 6: S6  

 

The value of **s** was 1 the first time through the loop, so Matlab prints out this value along with the value of **subject_list{1}**, which is **S1**.  Then it increments **s** so that it now equals 2 and compares it against the value of numsubjects.  Since **numsubjects** has a value of 6, and 2 is less than 6, the loop keeps going.  Now when Matlab executes the **fprintf()** command, **s** has a value of 2, so it prints out the value of **subject_list{2}**, which is **S2**.  It keeps looping until incrementing **s** leads to a value that exceeds the value of **numsubjects**, at which point the loop ends.  (Note: This is only an approximate description of how a **for** loop works; for the precise definition, see a Matlab book or manual).

### Adding a loop to the script
Now we're ready to update the script so that it loops through the subjects.  This is really very easy.  The first step is to put the **subject_list** cell array and **numsubjects** variable at the top of the script.  You should just be able to copy them from the command window (where you defined them before) and paste them into your script.  These should be followed by the definition of the parent folder.  The first three lines of your script should look like this (except with a parentfolder path that is appropriate for your computer):  

    subject_list = {'S1', 'S2', 'S3', 'S4', 'S5', 'S6'};

    numsubjects  = length(subject_list); % number of subjects

    parentfolder = '/Users/luck/Documents/Software_Development/ERPLAB_Toolbox/Test_Data/';  

 

Now, put the following after these three lines:  

    for s=1:numsubjects

 

        subject = subject_list{s};

        subjectfolder = [parentfolder subject '/'];

        fprintf('\n\n\n*** Processing subject %d (%s) ***\n\n\n', s, subject);  

 

The first line is the start of the for loop.  It defines a variable called **s** (short for "subject_number"), which will go from 1 on the first iteration to 6 on the last iteration (because numsubjects should have a value of 6).

The next line sets the **subject** variable equal to the current member of the **subject_list** cell array.  On the first iteration, **s** will be equal to 1, so **subject_list{s}** will be the first subject, **S1**.  Thus, the first time through, **subject** will have a value of **S1**.

The next line sets the **subjectfolder** variable equal to the parentfolder plus the **subject** plus a slash.  This will result in a value of something like **/Users/luck/Documents/Software_Development/ERPLAB_Toolbox/Test_Data/S1**.  Notice that this needs to go inside the loop, rather than before the **for** statement, because it will be updated on each iteration of the loop.

The last line will print a message to the command line near the beginning of each iteration, letting you know which subject is currently being processed.  On the 6th iteration, for example, it will print the following to the command window:  

    *** Processing subject 6 (S6) ***  

 

The next step is to place an **end**; statement near the end of the script, after the line with the **ALLERP=ERP** command and before the line with the **eeglab redraw** command.  It needs to go before the **eeglab redraw** command, because you only want to update the EEGLAB GUI after you've finished looping through all the subjects. The whole script should look something like this:  

    subject_list = {'S1', 'S2', 'S3', 'S4', 'S5', 'S6'};

    numsubjects = length(subject_list);

    parentfolder = '/Users/luck/Documents/Software_Development/ERPLAB_Toolbox/Test_Data/';

 

    ALLERP = buildERPstruct([]);

    CURRENTERP = 0;

 

    for s=1:numsubjects

 

    subject = subject_list{s};

    subjectfolder = [parentfolder subject '/'];

    fprintf('\n\n\n*** Processing subject %d (%s) ***\n\n\n', s, subject);

 

        EEG = pop_loadset('filename',[subject '_EEG.set'],'filepath',subjectfolder);

        EEG = pop_chanedit(EEG, 'lookup','standard-10-5-cap385.elp');

        EEG = pop_editset(EEG, 'setname', [subject '_Chan']);

        EEG = pop_saveset( EEG, 'filename', [subject '_Chan.set'],'filepath', subjectfolder);

        EEG = pop_creabasiceventlist( EEG , 'AlphanumericCleaning', 'on', 'BoundaryNumeric', { -99 }, 'BoundaryString', { 'boundary' } );

        EEG = pop_binlister( EEG , 'BDF', [parentfolder 'binlister_demo_1.txt'], 'IndexEL', 1, 'SendEL2', 'EEG', 'Voutput', 'EEG' );

        EEG = pop_epochbin( EEG , [-200.0 800.0], 'pre');

        EEG = pop_artmwppth( EEG , 'Channel', 1:16, 'Flag', 1, 'Threshold', 100, 'Twindow', [ -200 798], 'Windowsize', 200, 'Windowstep', 50 );

        [ALLEEG EEG CURRENTSET] = eeg_store( ALLEEG, EEG, 0 );

        ERP = pop_averager( EEG , 'Criterion', 'good', 'DSindex', 6, 'ExcludeBoundary', 'on', 'SEM', 'on' );

        ERP = pop_savemyerp(ERP, 'erpname', [subject '_ERP'], 'filename', [subject '_ERP.erp'], 'filepath', subjectfolder, 'warning', 'off');

        CURRENTERP = CURRENTERP + 1;

        ALLERP(CURRENTERP) = ERP;

 

 

    end;

 

    eeglab redraw;

    erplab redraw;  

 

Notice that all of the lines between **for** and **end** have been indented.  This is standard practice, and it makes it easier to see which commands are inside a given loop.

Try running the script.  If you watch the command window, you should see it do the processing for each subject.

In the version of the script shown above, only the final dataset (created by the artifact detection function) is saved into the ALLEEG structure with the **eeg_store** command.  If your script does this, then you should be able to look in the **Datasets** menu after running the script and see this dataset for each subject.

However, only the final **ERP** is saved in the **ALLERP** variable and is visible in the **ERPsets** menu. To fix this, you can replace the **ALLERP = ERP**; line with the following:  

    CURRENTERP = CURRENTERP + 1;
    ALLERP(CURRENTERP) = ERP;  

 

And you'll also need to put the following at the beginning of the script (somewhere before the **for** statement):  

    ALLERP = buildERPstruct([]);
    CURRENTERP = 0;  

 

Let's unpack this a little bit. First, the line that says **ALLERP = buildERPstruct([])**; at the beginning of your script builds an empty **ERP** structure and assigns it to the **ALLERP** variable. **CURRENTERP** is an ERPLAB variable that keeps track of the current **ERPset** in the **ERPsets** menu, and you set this to 0 at the beginning of the script with **CURRENTERP = 0**. Together, these two lines clear out any previous ERPs from **ALLERP** and get the script ready for you to add a new set of ERPs to **ALLERP**.

At the end of each iteration of your loop, you will store the **ERP** you've created in **ALLERP**. First, you increment CURRENTERP by 1 (with **CURRENTERP = CURRENTERP + 1**) and then use this to indicate which element in ALLERP you are creating (by typing **ALLERP(CURRENTERP) = ERP**). On the first time through the loop, **CURRENTERP** will initially be set to 0, and the **CURRENTERP = CURRENTERP + 1** line will set it to 1. Then, the **ALLERP(CURRENTERP) = ERP** line will set the first item in **ALLERP** to be equal to the current **ERP**. Similarly, if you've already processed the first 3 subjects and are working on the fourth subject, CURRENTERP should be 3 (from the previous round of the loop). When Matlab reaches the line that says **CURRENTERP = CURRENTERP + 1**, it will set **CURRENTERP** to 4 (because the old value of **CURRENTERP** was 3, and 3 + 1 = 4). The next line will use the new value of **CURRENTERP** to select the right element of the **ALLERP** variable. This line will be equivalent to **ALLERP(4) = ERP** (because **CURRENTERP** now equals 4). This will set the fourth element of the **ALLERP** array to equal the contents of the current **ERP** structure. Whew!

You might want to take a look at the file Script3c.m to see how all of this is supposed to look.

Once you have this new stuff inserted into your script, try running the script again. You should now see all of the ERPs in your **ERPsets** menu. With this stuff in your script, you no longer need to quit and relaunch EEGLAB before running your script.