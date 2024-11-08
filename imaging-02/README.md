## Aim

The learning objectives for this unit are:

- become more comfortable with manipulating 3d and 4d data ("multidimensional arrays")
- solidify our understanding of what it means for something to be 3 (or 4) dimensional
- load in data from `nifti` files
- get practice writing writing ``function``s in matlab
- get comfortable with ``function``s that have 1 or more input arguments, and 1 or more output arguments

## Loading data from `nifti` files

```matlab
data = niftiread('/Volumes/practicals/ds1/2019-msc-matlab/example.nii');
```
Look at the documentation for `niftiread`!

## A function for returning a single voxel timecourse

Write a function ``returnTimecourse()`` that returns a 1D timecourse from a 4D dataset (3d space, 1d time).

Users should be able to use the function like this

```matlab
c = [24,25,10]; for example
tc = returnTimecourse(data, c);
plot(tc)
```
- What are the things that you might want to guard against when writing your code? 
- Can you anticipate some potential user errors?
- Additional: how can you find out what the `TR` is to create a vector of time in seconds (rather than units of `volumes`)?

## A function for calculating the HRF

The function ``makeHrf()`` creates the y-values for an HRF. The time runs from 0 to 30s (in steps of the ``TR`` you specify). So for ``TR=1.5`` it would be ``[0, 1.5 3, 4.5, ... 30]``

```matlab
t = 0:1.5:30; %
h = makeHrf(1.5); % creates an hrf for 30s
plot(t, h ,'ro-')
```
**Bonus:** where to find the equations that describe HRF as a function to time? Are there several available? Could you add a flag to your code that could allow you to switch between different versions?

## Also...
Toward the end of this unit, we need to construct a function ``makeDesignMatrix()`` that will help us do linear regression in due course. The idea here is to specify the on/off timing (say, for a visual stimulus in an fMRI experiment)

- 2 obligatory input arguments: ``blockOne, n``
- 2 optional input argument: ``TR, hrf``
- returns:
	+ ``d`` (1-column design matrix taking into account the HRF)
	+ ``dRaw`` (same as d, but without HRF).


## Checking results

Look at ``help makeDesignMatrix`` to get some ideas on how to plot. With some additional adjusting you can end up with something like this:

![Image of Design matrix](https://github.com/schluppeck/c84nim/blob/master/imaging-02/designMatrix.png)

## Notes

- the file ``makeDesignMatrix.p`` is the pcode/compiled version that runs (but for which you cannot see the code). The ``.m`` file here is just to provide the help text - you need to add the code to implement the function yourself!

- ``dRaw`` contains ``n`` repeats of ``blockOne`` in succession,
- ``d`` is the same as ``dRaw``, but convolved with a haemodynamic response function.
- ``d`` should be returned such that mean(d) = 0
- ninja skills: how to handle non-blocked designs?
