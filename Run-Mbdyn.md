## 1. Set Installation Path

You have to set the path of the [MBDyn][1] binaries in Blendyn, to run an 
[MBDyn][1] simulation.

On Ubuntu, open up a new terminal, and type `whereis mbdyn`, which produces
an output of `mbdyn: /usr/local/mbdyn`. Here `/usr/local/mbdyn/bin` is the installation path.

Or you could also set the installation through the path navigator in the 
`Path` field above the `Set Installation Path` button.

- - - 
![blendyn panel in sidebar](images/tools_simulation_panel.png
"Simulation Panel")
- - - 

## 2. Select Input File

Select an input file by clicking on the `Select input file` button, and navigating
to the input file.

Note that [MBDyn][1] doesn't demand any specific extension for its input files, so all
kinds of files are displayed.

## 3. Set Output Directory

Select the output directory in which you want the results files to be 
generated through the `Output Directory` button.

The default directory is the directory of input file selected.

## 4. Set Output Filename

Set the results files basename through the `Output Filename` button.

- - - 
![blendyn panel in sidebar](images/overwrite.png
"Simulation Number")
- - - 

The default output filename is the name of the input file. All output filenames
are appended by the **current simulation number** to differentiate between successive simulations.

To overwrite over results of previous simulations, check the `Overwrite Previous
Files` option before proceeding with the rest of the simulation.

## 5. Set Environment Variables (Optional)

You can set environment variables to help with your [MBDyn][1] Simulation. A good
example is setting an environment variable to a parameters file, as shown below.

Set the variable in the `Variable` field, and its corresponding value in the
`Value` field, and the set the variable with the `Set Variable` button, as shown below.

- - - 
![blendyn panel in sidebar](images/environment_variable.png
"Environment Variables")
- - - 
To change the value of an environment variable, change the value in the `Value`
field, and press `Set Variable` again.
  
To remove an environment variable from the list, just select the environment
variable from the list, and press `Delete Variable` .

## 6. Final Time
If you set the final time of your simulation in your input file with a number,
go ahead an ignore this step.
```
begin: initial value;
	initial time: 0.;
	final time: 2.;
  .............
```


But if you set the final time with a variable,
```
set: const real TF = 10;

begin: initial value;
	initial time: 0.;
	final time: TF;
  .............
```

do manually set the `Final Time`
in Blendyn, right below the `Delete Variable` button. **Make sure that the value
set in Blendyn is the same as that in the input file.**

## 7. Run Simulation
Go ahead and press the `Run Simulation` button to start the [MBDyn][1] Simulation.

You can observe the progress of the simulation in the `Simulation Status` field,
right above the `Run Simulation` button.

- - - 
![blendyn panel in sidebar](images/progress_simulation.png
"Environment Variables")
- - - 

If at any point in the progress of the simulation, you want to stop the simulation,
you can press the `Stop Simulation` button.

After the completion of the simulation, the results file should be automatically
loaded into Blendyn.

If you do not have the [netCDF][3] module installed, do click on the `Always load text output`
(located just below the `Overwrite Previous Files` option). This will make sure
you always load `*.mov` files.

Go ahead and press the `Load .log file` button, and proceed with the rest of the
animation process.


  [1]: https://www.mbdyn.org/
  [2]: https://www.blender.org/
  [3]: http://www.unidata.ucar.edu/software/netcdf/
