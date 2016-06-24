## Getting Info about an ERP from MATLAB Command Line
Even if you do not know anything about Matlab programming and only use ERPLAB from the GUI, you can use the Matlab command line to obtain useful information about the current EEG and ERP structures.  You can simply type the name of a variable on the command line to see a summary of its contents.  For example, here is an example of what you will see if you type "ERP" on the command line (when an ERPset is active in the ERPsets menu).

>> ERP

 

ERP =

erpname: 'CNS Demo ERPs filtered difference wave'

filename: []

filepath: []

workfiles: {''}

subject: ''

nchan: 14

nbin: 3

pnts: 250

srate: 250

xmin: -0.2000

xmax: 0.7960

times: [1x250 double]

bindata: [14x250x3 double]

binerror: []

ntrials: [1x1 struct]

isfilt: 1

chanlocs: [1x14 struct]

ref: 'common'

bindescr: {'Standard (correct)'  'Target (correct)'  'DIFF WAVE'}

saved: 'no'

history: [4x826 char]

version: '1.2.0'

splinefile: ''

EVENTLIST: [1x1 struct]

 

Each line shows a field in the ERP structure.  When a given field contains relatively simple data, the values are shown for that field.  In the current example, the values from the fields show that the currently active ERPset has 14 channels (nchans), 3 bins (nbins), 250 sample points per epoch (pnts), a sampling rate of 250 Hz (srate), a starting point of -0.2 seconds (200 ms; xmin), an ending point of 0.796 seconds (796 ms; xmax), has been filtered (isfilt), and has not been saved to disk (saved).  When a field contains complex data, a summary of the matrix for that field is shown (e.g., "[4x826 char]" means a 2-dimensional character array with 4 rows and 826 columns).  If you want to see the contents of one of these complex fields, you can type the name of the structure, a dot, and the name of the field.  For example, to see the number of trials in each bin (in the ntrials field), you would type "ERP.ntrials".  The result would look like this:

>> ERP.ntrials

 

ans =

 

    accepted: [246 63 309]

    rejected: [6 0 6]

     invalid: [0 0 0]

     arflags: [3 x 8 double]

 

This means that there were 246 trials included in the average for bin 1, 63 for bin 2, and 309 for bin 3.  The number of trials rejected because of artifacts was 6, 0, and 6, respectively.  The "invalid" field is the count of trials that were rejected because of some kind of problem (e.g., the EEG epoch contained a boundary event code).  Note that bin 3 in this example is a difference wave created by subtracting bin 1 from bin 2; the number of trials in such cases is the total number of trials contributing to the average (i.e., the sum of the trials in the individual averages that were combined to create the new bins).

You can use this same approach to see the contents of the current EEG structure.  To see the EVENTLIST that was created for the current EEG structure, you can simply type "EEG.EVENTLIST".  The result would look something like this:

>> EEG.EVENTLIST

 

ans =

setname: 'CNT file_elist'

report: ''

bdfname: 'CNS Demo BDF.txt'

nbin: 2

version: '1.2.0'

account: 'luck'

username: ''

trialsperbin: [252 63]

elname: 'ERPLAB Demo 3-09.txt'

bdf: [1x2 struct]

eldate: '16-Jul-2009 09:22:37'

eventinfo: [1x315 struct]

 

Note that the setname field stores the name of the dataset that was active when the EVENTLIST structure was created, not the name of the currently active dataset.  Also note that information from the bin descriptor file is present if BINLISTER has been run.  That is, if you type "EEG.EVENTLIST.bdf", you can see the bin description that was used to define each bin.  This is helpful if you create the file one day and go back to it a year later, by which time you've forgotten exactly what you did to create the EVENTLIST.  You can even re-create the bin descriptor file using ERPLAB>Utilities>Recover bin descriptor file.