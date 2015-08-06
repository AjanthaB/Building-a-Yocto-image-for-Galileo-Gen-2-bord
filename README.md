# Building-a-Yocto-image-for-Galileo-Gen-2-bord
#####This tutorial will show you how to Building a Yocto image for Galileo Gen 2  bord using linux. And installing other packeges like OpenCV etc.
### Tested with Ubuntu 14.04
First of all you should install following packages

1. git
2. diffstat
3. textinfo
4. gawk
5. chrpath
6. file

If you are connecting through `proxy`, git requires proxy configuration.If any command fail, it may be proxy settings.You can find proxy settings here https://wiki.yoctoproject.org/wiki/Working_Behind_a_Network_Proxy.

Download the file `FBoard_Support_Package_Sources_for_Intel_Quark_v1.1.0.7z` from here https://downloadcenter.intel.com/download/23197/Intel-Quark-BSP. And extract the file. you can see few .tar.gz  files, To build  this image extract the meta-clanton_v1.1.0-dirty.tar.gz file to new directory.
cd to meta-clanton_v1.1.0-dirty and run following command.
###### # ./setup.sh

When this scripts runs successfully, it will add additional folders such as bitbake,
meta-yocto, repo-ext, etc.

Next, `source the iot-devkit-init-build-env` command to initialize the Yocto
Project build environment. This command takes the build directory name as its
parameter:
###### # `source ./iot-devkit-init-build-env yocto_build`
yocto_build is the directoty name. use whatever you want.

After this command runs, the current directory will now be the directory specified in
the parameter (yocto_build in this case). From this directory, run `bitbake <target>` to build the root file system and kernel.

The SoC-specific `<target>` commands described below will determine whether the
resulting components are built for SPI flash or for SD/USB. The output is slightly
different for each target.

Note: It is not possible to perform both (SD/USB and SPI) build methods from the same
directory. If you want both builds, you must perform them on two completely
different and isolated directories.

###Build a Full-featured Linux for SD card or USB Stick

######Note:
A complete Yocto Project build can take several hours to complete, depending on your
internet connection speed and your machine’s specifications.

To build out an image suitable for running on SD card or USB stick, the bitbake target
is image-full:
###### # `bitbake image-full`

When this process complete, the required output files are found in
./tmp/deploy/images/quark/ and include many components.

for image you should rename this files

1. `image-full-quark-some_number.rootfs.ext3` to `image-full-quark.ext3`
2. `core-image-minimal-initramfs-quark-some_number.rootfs.cpio.gz`  to  `core-image-minimal-initramfs-quark.cpio.gz`
3. `bzImage--3.8-r0-quark-some_number.bin` to `bzImage`

`some_number` means, after building this image some_number is equal to date this image was build  


copy this files to your SD card

1. image-full-quark.ext3
2. core-image-minimal-initramfs-quark.cpio.gz
3. bzImage
4. grub.efi
5. boot (directory)


Now you can boot image. This does not contained OpenCV packge.


### install OpenCV on build yocto_image using Intel Gelileo Gen 2

connect the Gelileo bord to your computer(with build os) and connect to ethernet.type following command ti install `OpenCV`
###### Galileo configuration instructions:

 To configure your Galileo to fetch packages from this repo, do the following:
 
1. login to os on the bord using `ssh` or `srial` (use the password as "root").

2. type this command  `vi /etc/opkg/base-feeds.conf`  with the following (other opkg config files don't need any changes):

3. add this links and save it

- `src/gz all http://repo.opkg.net/edison/repo/all`
- `src/gz edison http://repo.opkg.net/edison/repo/edison`
- `src/gz core2-32 http://repo.opkg.net/edison/repo/core2-32`

4. run this command `opkg update' (`don't use "opkg upgrade"`)

5. now you can install packages using this comand `opkb install <package name>`

to install OpenCV `opkg install opencv2` and also can see the packeges already installed `opkg list-packages`

now your task is ok.yiu can check OpenCV sucessfully installed or not inmporting the opencv2 to python
`import opencv2` 


####You can download prebuild image here['https://drive.google.com/folderview?id=0Bw5tihzaggSCfnRYZGg5XzRzT2kwT3BNQXNSbllDemR1ZGdRMC0tUW03ZFFnZ0NERENGUDA&usp=sharing']








