#  UNIT 9: Eyetracking example (Week 6)

**Useful operators and commands for this unit...**

logical indexing, ``nan``, ``subplot()``, ``cell`` arrays and using {:} to unpack them

Data in the file ``exFixation.mat`` are organized as follows: there are two matrices datax and datay that are of size 1000 rows (time points) by 10 columns (trials). That means: 10 very long columns. Fixation patterns refer back to the following kinds of images. In the second part of the exercise you’ll need to know the bounding box / region of interest for the eyes.

<img width="744" alt="Screenshot 2023-11-01 at 21 14 58" src="https://github.com/scholesy1982/learningMatlabFromDenis/assets/146671875/b8ca3631-0c7a-4741-a5e8-a75d8c6fa39e">

1. Clear the workspace to start with a clean sheet and then inspect the data provided in exFixation.
mat. The following gives you a way to look without loading the data in. This is useful:
```matlab
clear all, close all
whos -file exFixation.mat
```

2. Load the data into the main Matlab workspace so you can manipulate the data and get ready to write a function for plotting data in differet ways:

```matlab
load exFixation
```

3. Now, we can start working on a new function (call it plotFixations) that plots the data in a couple of different ways. The figure window should be divided into three ‘‘subplot‘‘s - the first showing the x-position as a function of time, the second the y-position as a function of time and the third a plot of y-position against x-position (the actual eye-position in 2d). You should be able to call:

```matlab
plotFixations(datax, datay, 3, 'g')
% plotFixations(<x data>, <y data>, <trialNumber>, <line specifications>)
```

