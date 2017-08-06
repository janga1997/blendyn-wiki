# Live Animation

Live Animation in Blendyn works in sync with your MBDyn simulation, and updates the Blender scene on every step of the simulation.

This is done with the help of stream file drivers and stream output elements in MBDyn. Follow the below steps to get started:

## 1. Setting up your input file

Live animation in Blendyn works with a stream output element sending coordinates to Blendyn, and Blendyn progressing the MBDyn simulation by one step by sending data to a dedicated stream file driver.

* Add the below lines to your MBDyn input file.

### Stream Driver (in between nodes and elements blocks)

**INET**
```
begin: drivers;
   file: 1, stream,
        stream drive name, "INPUT",
        create, yes,
        port, 9012,

        timeout, 200,
        1;
end: drivers;
```

**`OR`**

**UNIX**
```
begin: drivers;
   file: 1, stream,
        stream drive name, "INPUT",
        create, yes,
        path, "./mbdyn.input.sock",

        timeout, 200,
        1;
end: drivers;
```


### Stream output element (in elements block)

**INET**
```
stream output: 1,
    stream name, "OUTPUT",
    create, yes,
        port, 9014,
    no signal,
    motion,
    output flags, position, orientation matrix, 
    all;
```

**`OR`**

**UNIX**
```
stream output: 1,
    stream name, "OUTPUT",
    create, yes,
        path, "./mbdyn.output.sock",
    no signal,
    motion,
    output flags, position, orientation matrix, 
    all;
```

## 2. Running the Simulation

* Open up Blender, select the Input file using the `Select Input File` button
* Start the Simulation by pressing the button `Run Simulation`.
* Load the .log file, and add the nodes and elements to the scene using the `Standard Import` button.
* Connect to the sockets launched by MBDyn through the button `Start Sockets`.

## 3. Controlling the Live Animation
* After completing the above steps, you can start the live animation by pressing the `P` key.
* During the course of the simulation, the `P` key serves to pause/play the simulation.
* You can speed up the simulation by pressing on the key `K`, and slow it down by pressing on the key `J`. This happens by increasing/decreasing the load frequency by 1.

* You can see the progress of the simulation as a percentage, in the `Simulation Status Field`.

* You can stop the sockets, and the MBDyn simulation at any point by just pressing the `ESC` key.
* You can store keyframes of the simulation at the beginning, or at any point in the simulation by checking the `Set Keyframes` checkbox.



  [1]: http://www.pygal.org/en/latest/
  [2]: https://www.mbdyn.org
  [3]: http://www.unidata.ucar.edu/software/netcdf/
  [4]: https://github.com/zanoni-mbdyn/blendyn/wiki/Installation
  [5]: https://www.blender.org/
