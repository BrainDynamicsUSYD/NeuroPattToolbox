# NeuroPattToolbox
Neuropatt is a MATLAB toolbox to automatically detect, analyze and visualize spatiotemporal patterns in neural population activity. Data recorded by multi-electrode arrays, EEG, MEG, fMRI and other imaging methods such as VSD can optionally be filtered to extract the phase or amplitude of oscillations within a specified frequency range. Propagating activity is then extracted adapting methods from the fields of turbulence fluid and computer vision. Spatiotemporal patterns can be tracked across space and time using order parameter and critical point analysis, and dominant spatiotemporal dynamics are extracted using vector field decompositions.

NeuroPatt comes with a collection of user-friendly Matlab functions that allow for (1) automatic detection of all spatiotemporal patterns in an input recording based on user parameters, (2) output and visualization (plots and videos) of pattern statistics, (3) and analysis and visualization of pattern dynamics.

# Citation
If you use our code in your research, please cite us as follows: 
Rory G. Townsend and Pulin Gong (2018). Detection and analysis of spatiotemporal patterns in brain activity, Under Review, PLOS Computational Biology.

# Usage
All primary functions can be accessed through the NeuroPattGUI M-file. The toolbox includes a sample dataset of LFPs recorded from marmoset visual area MT (see references 1 and 2, 10x10 recording array, 5 repetitions of moving-dot stimulus presentations with stimulus turned on at 1s and sampling frequency 1017 Hz, MA026-14 Dir 1 Rep 40-44). This test data can be processed with the following:

	# Add all subfolders to path
	addpath(genpath('.'))
	# Load test data
	load('sampleData_marmosetLFP.mat')
	# Run toolbox GUI
	results = NeuroPattGUI(sampleLFP, sampleFs);

Using default parameters, NeuroPattGUI will find all patterns at 4 Hz in the recording and output vector decompositions, patterns detected and pattern transitions. At the results screen, pattern statistics and locations can be visualised in more detail, and analysis can be repeated with surrogate, noise-driven data to verify results.

The saveVelocityFieldVideo function can then be used to show all computed amplitude/phase maps with their corresponding velocity fields:

	# Set parameters
	vidName = 'testVideo';
	vidFps = 20;
	resizeScale = 2;
	# Make video
	saveVelocityFieldVideo(results.filteredSignal, results.velocityFields, vidName, vidFps, results.Fs, resizeScale)

As an alternative to using the GUI, all main functionality can instead be run through the command line. Desired parameters should first be specified within the setNeuroPattParams M-file, then processing can be run through:
	
	# Set parameters
	params = setNeuroPattParams;
	# Process data to find all patterns
	results = mainProcessingWithOutput(sampleLFP, sampleFs, params);


# License
This project is licensed under the GNU General Public License Version 3 - see the LICENSE.md file for details.

# References
1. Townsend RG, Gong P. Detection and analysis of spatiotemporal patterns in brain activity, Under Review, PLOS Computational Biology 2018.
2. McDonald JS, Clifford CWG, Solomon SS, Chen SC, Solomon SG. Integration and segregation of multiple motion signals by neurons in area MT of primate. J Neurophysiol. 2014;111: 369–378. doi:10.1152/jn.00254.2013
