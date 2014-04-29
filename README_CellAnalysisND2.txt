####################################
# READ_ME - CellAnalysisND2
# University of California - Davis
# Albeck Lab
#
#########################################################
#Cell Tracking and Analysis                             #
#	This software analyses an ND2 movie file and    #
#	tracks cells through time. The output contains  #
#	intensities of the tracks in different channels #
#	as well as the ratios of those channels.	#
#########################################################

Scripts
-------
1. autourun.m		This script invokes the pipeline for cell analysis.
2. bfopen2.m		This is a modified script that opens bioformat files.
3. qteND2p.m		This script identifies cells based on a set of given parameters.
4. scriptTrackgeneral.m	This modified script creates tracks of identified cells.
5. ContourTrackND2p.m	This script grabs the nuclear and cytosolic intensity values from the tracked cells.

Packages used(included)
1. bfmatlab		Contains scripts to open bioformat files.
2. u-track_2.1.0	Containts scripts to track based on cell position.


Dependencies
------------
1. Matlab R2013A or newer
2. ND2 file to analyze
3. Enough RAM to open ~16 GB of data
4. Scripts and files should be on the Matlab Path
5. Initialized parallel environment (done by typing at command line: matlabpool local)

To Invoke
---------
On the Command Prompt:
matlabpool local
autorun(file, positions, maxDiam, minDiam, circularity, c1Background, c2Background, c3Background, workers)

Replace the variables as follows:
file - file name in quotes. 'test.nd2'
positions - the number of positions in the nd2 file.
maxDiam - maximum cell diamater for identification. 
minDiam - minimum cell diameter for identification.
circularity - circularity for cell identification. 0-1. closer to 1 the more circular
c1Background - Background values for the 1st channel. This is to get rid of noise in the ouput
workers - The number of processors you want this job to take. More cores the more intensive it is on your computer, but the faster the output will come. Most computer have 4 cores. Matlab has one core for processing by default. This value adds extra workers. 3 workers = 4 cores.

sample invoke script:
autorun('test.nd2', 48, 100, 14, 0.6, 345, 200, 500, 3)

See what your program is tracking:
%Open first position
mdata = bfopen2(file,1);
slice = mdata{i,1}(:,1);
slices = [1:size(slice,1)/3];
movieInfo = qteND2(mdata,2,maxDiam,minDiam,circularity,1);

Replace the variables with your best guess and adjust according.
