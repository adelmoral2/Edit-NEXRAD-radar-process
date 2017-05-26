# Editing Procedure of NEXRAD radar data
## Prerequisite
Prior to working, make sure that the following packages are installed:
- [Latest Radx Package](https://github.com/NCAR/lrose-core/releases/tag/radx-20170315)

Radx is a package for handling radar and lidar data in radial/polar coordinates
([Instructions from NCAR](https://www.eol.ucar.edu/software/radx))
```terminal
cd Downloads/radx-20160327.macosx_x64 
sudo ./install_bin_release
```
- [Xquartz](https://www.xquartz.org/)
- [Soloii Binary file]()
([Overview of Soloii](http://radarmet.atmos.colostate.edu/software/soloii/index.html))

Before you run it, put the following command in a Terminal so that it can recognize the display:
```terminal
export DISPLAY=:0
```

## Convert data format
We have to convert the format of raw data (ar2v file) to sweep files by performing the command of RadxConvert before running soloii.
```terminal
RadxConvert -dorade -f name.ar2v
```

To show all the commands that we can use inside the Radx package, we can run:
```terminal
RadxConvert -h |more
```

## Quality Control of the wind field
Before unfolding the wind field, make sure that xquartz is running. 
Type "soloii" in the terminal, so the variables fields can be displyed in your xquartz. 
```terminal
soloii
```
A window will pop out just like the following image:
![Soloii Display](https://github.com/tingyucha/Edit-NEXRAD-radar-process/blob/master/Soloii_Display.png)

Some algorithms perform pretty well in quality control. To start with, right click "Editor". 

![Editor Commands](https://github.com/tingyucha/Edit-NEXRAD-radar-process/blob/master/Editor_Commands.png)
The commands of left panel work pretty well in general conditions. Make sure that the commands are in order. It will influence the QC processing if you don't follow the above order. On the other hand, the commands of right panel need  Note that the following three commands are referring to the location of radar, which means that it should calculate according to the local winds near the radar.
```terminal
BB-use-local-wind
ew-wind is [approximate a value near the radar]
ns-wind is [approximate a value near the radar]
```

## Convert all the sweep files to be gridded
After completing editing all wind fields, the data should be converted into cartesian coordinate and be gridded in this step.
1. Run createVolumes.sh in the terminal under the same directory of sweep files[createVolumes.sh](https://github.com/tingyucha/Edit-NEXRAD-radar-process/blob/master/createVolumes.sh)

```terminal
sh createVolumes.sh /DirectoryWhereYouWantPutTheVolumes/
```
Or you can use one command to convert sweep files to cfrad files:


```terminal
sh createVolumes.sh /DirectoryWhereYouWantPutTheVolumes/
```
2. 
