#  UNIT 9: Eyetracking example (Week 6)

**Useful operators and commands for this unit...**

logical indexing, ``nan``, ``subplot()``, ``cell`` arrays and using {:} to unpack them

Data in the file ``exFixation.mat`` are organized as follows: there are two arrays ``datax`` and ``datay`` that are of size 1000 rows (time points) by 10 columns (trials). That means: 10 very long columns. Fixation patterns refer back to the following kinds of images. In the second part of the exercise you’ll need to know the bounding box / region of interest for the eyes.

<img width="744" alt="Screenshot 2023-11-01 at 21 14 58" src="https://github.com/scholesy1982/learningMatlabFromDenis/assets/146671875/b8ca3631-0c7a-4741-a5e8-a75d8c6fa39e">

1. Clear the workspace to start with a clean sheet and then inspect the data provided in exFixation.
mat. The following gives you a way to look without loading the data in. This is useful:
```matlab
clear all, close all
whos -file exFixation.mat
```

2. Load the data into the main Matlab workspace so you can manipulate the data:

```matlab
load exFixation
```

3. Now, we can start working on a script (call it ``plotFixations``) that plots the data in a couple of different ways. The figure window should be divided into three ``subplot``s - the first showing the x-position as a function of time (or sample number), the second the y-position as a function of time (or sample number) and the third a plot of y-position against x-position (the actual eye-position in 2d). Create a variable trialNumber to control which trial is being plotted ``trialNumber = 3;`` and a variable called lineSpec to control the appearance of the plot ``lineSpec = 'g';``.

Your figure should look something like this:

![fixationFig](https://github.com/scholesy1982/learningMatlabFromDenis/assets/146671875/21f305e6-76e7-4357-b62e-34f78c4abcdf)

Can you work out how to arrange the panels as shown in the example figure using subplot?

4. **Bonus.** A more advanced way to specify linestyles for the plots. Can you see how to do this? Hint: check out what happens when you expand a cell array using the colon operator - as indicated just below:

```matlab
lineSpec = {'linewidth',2, 'color',[0 1 1]};
lineSpec{:}
```

5. Now it’s time to break out the bit of code that plots y against x. For the next steps we are not so interested in how x and y evolve over time, but more about which parts of space are being viewed at a particular time. And we wish to loop over all trials to create a figure for each trial. We're going to do the *same* thing repeatedly (but for different trial numbers) so this time you should write a **function** ``plotFixationsInWindow()``. In this function, the input arguments are: ``x, y, trialNum, fixationWindow``. The variable ``fixationWindow`` specifies the dimensions of a box for which you want to estimate the proportion of viewing time.
* ``fixationWindow`` should be a 4 element vector ``[x0 y0 x1 y1]``
* use a logical test to make an index that selects part of the data within the limits (see Unit6: loopsAndControls)
* ``plot`` the data and use ``hold on`` and plot the selected points on top in a different color.
* the finished product may look something like the following:

<img width="727" alt="Screenshot 2023-11-01 at 21 33 45" src="https://github.com/scholesy1982/learningMatlabFromDenis/assets/146671875/d87491b8-db3e-4ed8-88d3-912f043c2567">

6. Once you have created your function, write a script which loops through each trial and calls the function you created in step 5. As there are 10 trials, you should end up with 10 figures. Add a line into your function which puts a ``title`` on to each figure, specifying which trial is being shown.
