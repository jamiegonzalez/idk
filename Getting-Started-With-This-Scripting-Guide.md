## Getting Started With This Scripting Guide
### Downloading the Example Data
If you haven't already done so, you need to download the ERPLAB Test_Data folder, which contains the data and other files that will be used in the examples below. You can download it from the [ERPLAB documentation area of this web site](https://github.com/lucklab/erplab/wiki).  You can put this folder anywhere on your computer's file system. 

### Accessing the History
To see the history of everything that led up to the current EEG or ERP structure, you can simply type **EEG.history** or **ERP.history**.  You will then see something like this (assuming that you've done some processing steps in the EEGLAB GUI since it was last launched):  

    EEG = pop_loadset( 'filename', 'S1_EEG.set', 'filepath', '/Users/luck/Documents/Software Development/ERPLAB Toolbox/Documentation/Tutorial/s1/');

    EEG = eeg_checkset( EEG );

    EEG = pop_editset(EEG, 'setname',  'S1_EEG');

    EEG = eeg_checkset( EEG );

    EEG = pop_loadset('filename','S1_EEG.set','filepath','/Users/luck/Documents/Software_Development/erplab toolbox/documentation/Tutorial_Data (for testing)/S1 August 2011/');

    EEG = eeg_checkset( EEG );

    EEG=pop_chanedit(EEG, 'lookup','/Users/luck/Documents/Software_Development/eeglab9_0_2_3b/plugins/dipfit2.2/standard_BESA/standard-10-5-cap385.elp');

    EEG = eeg_checkset( EEG );

    figure; pop_spectopo(EEG, 1, [0  2139038], 'EEG' , 'percent', 15, 'freq', [6 10 22], 'freqrange',[2 25],'electrodes','off');

    EEG = pop_editset(EEG, 'setname', 'S1_Chan');

    EEG = eeg_checkset( EEG );

    EEG = pop_saveset( EEG, 'savemode','resave');

    EEG = eeg_checkset( EEG );

    EEG = pop_loadset('filename','S1_Chan.set','filepath','/Users/luck/Documents/Software_Development/erplab toolbox/documentation/Tutorial_Data (for testing)/S1 August 2011/');

    EEG = eeg_checkset( EEG );

    EEG = eeg_checkset( EEG );

    EEG = pop_editeventlist(EEG, '/Users/luck/Documents/Software_Development/erplab toolbox/documentation/Tutorial_Data (for testing)/S1 August 2011/event_mapping_1.txt', 'elist.txt', {'boundary'}, {-99});

    EEG = eeg_checkset( EEG );

    pop_eegplot( EEG, 1, 1, 1);

    EEG = pop_epochbin( EEG , [-200.0  800.0],  'pre');

    EEG = eeg_checkset( EEG );

    EEG = pop_artmwppth( EEG, 'Channel', 1:16, 'Flag', 1, 'Threshold', 100, 'Twindow', [-200 798], 'Windowsize', 200, 'Windowstep', 100);  

 

This history list contains a variety of "housekeeping" steps (like the eeg_checkset() function) that you will not ordinarily include in a script.  You can instead type **eegh** or **erph** to get a version of the history that excludes most (but not all) housekeeping functions.  Note that EEG.history and ERP.history give you the history of routines that were made to create the current EEG and ERP structures, whereas the eegh and erph commands give you a history of what was done in the current session (including things that don't actually change the data, such as plotting, and things that were done to previous EEG and ERP files). In general, we recommend that you use EEG.history and ERP.history as the starting point for your scripts, but you can take a look at the output of **eegh** and **erph** to see how to run functions that don't actually change the EEG or ERP structure (like plotting).

You can also get information about how a given function works by typing **help _functionname_** (e.g., **help pop_epochbin**). This will tell you a little bit about how the function works and what the various function parameters mean.

### Organizing your files
In a typical ERP experiment, you may end up with 20-100 files for each subject (EEG and ERP files at various steps of analysis, analyzed in different ways, etc.).  It may be unwieldy to keep all of these files in a single folder.  In the examples described in this document, we have put the data for each subject in a separate folder (named S1, S2, S3, etc.).  If you use this format for your own research, you should have a "parent folder" for each experiment, and put the single-subject folders inside this parent folder.  Scripts and other files that apply to all subjects (e.g., bin descriptor files) can also be placed inside the parent folder.  You can also have a folder named "grand" inside the parent folder for your grand averages (or separate grand average folders for each group in a between-subject design, e.g., "grand_patient" and "grand_control"). ERPLAB doesn't require this particular organizational strategy, but it is a useful approach and will be used by the examples in this scripting guide.

### Keeping the GUI synced with your scripts
When you type a command on the Matlab command line or run a script, you may change the EEG or ERP structures.  If you then try to do something from the EEGLAB/ERPLAB GUI (like plotting the EEG or ERP data), you will likely run into errors.  This happens because the GUI doesn't "know about" the changes you've made to the EEG and ERP structures.  To solve this problem, type **eeglab redraw** and/or **erplab redraw** right before you go back to the GUI after executing commands from the command line or a script. We'll say more about this later.

### If you already know a little about scripts or programming…
The next few examples are designed for people who have little or no experience with scripting/programming.  If you have some basic knowledge, you can skip to [Example 3: A Simple Script That Actually Does Something Useful](https://github.com/lucklab/erplab/wiki/Example-3:-A-Simple-Script-That-Actually-Does-Something-Useful).