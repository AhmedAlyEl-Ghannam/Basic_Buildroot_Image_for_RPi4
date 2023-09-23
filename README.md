# Basic_Buildroot_Image_for_RPi4

This is a Buildroot image generated for Raspberry Pi 4. This README file shall contain all the steps I took in order to generate it, as well as screenshots for the system's output.

Notes:

  1. This system was built on 22/9/2023. Some steps may differ/be omitted altogether. Please, bare in mind that Buildroot is a piece of software that gets updated constantly and your steps may vary depending on when you decide to build/use it.
     
  2. This system was built on an Ubuntu 22.04---dual boot with Windows 10 not a virtual machine to squeeze every bit of performance out of my hardware---system on my trusty ten-year-old PC with the following specs:

       1. i7 4790k @4.4GHz
       1. 16GB DDR3 RAM @2400MHz
       1. GTX 980ti (irrelevant to this project) 
       1. A Kingston HyperX Savage SSD.
       
       ![](README_Photos/drip.png)
     
 Note that build time may vary depending on your hardware.
 
  3. The source I followed is Chris Simmond's book "Mastering Embedded Linux Programming - Second Edition" chapter 6: Selecting a Build System. It is a fantastic book that I STRONGLY recommend. But, bear in mind that the instructions listed in the chapter are for Beaglebone Black. If you use any other single board computer, you are on your own. If you decide to use Raspberry Pi 4, you came to the right place comrade.

  4. Another **GREAT** source is Shawn Hymel's YT playlist: [Introduction to Embedded Linux](https://youtube.com/playlist?list=PLEBQazB0HUyTpoJoZecRK6PpDG31Y7RPB&si=eVCmHkRdOECZorKh). The first video in the playlist was my first piece of info I consumed regarding Embedded Linux as a field. It is extremely well-made and I highly recommend binging the whole playlist.

Without further ado, let us begin.


## Cloning Buildroot

1. Clone Buildroot's repository. Make sure to clone it where you want to use it.

   ```
   git clone git://git.buildroot.net/buildroot
   ```


2. Open the cloned repository folder and make sure you are operating on the latest branch. `2023.08.x` is the latest branch as of the time of writing this README file.

   ```
   cd buildroot
   git checkout remotes/origin/2023.08.x
   ```


## Configuring Buildroot

1. Select the 64-bit configuration file for Raspberry Pi 4: `raspberrypi4_64_defconfig`.

   ```
   make raspberrypi4_64_defconfig
   ```


2. Next, open the TUI configuration menu for more options. For a minimal installation, you can leave it as it is. **NOTE THAT** I made an additional section where I explored lots of the options available and tested them later. For now, just leave it as it is.

   ```
   make menuconfig
   ```

3. Start compiling. My Image was compiled and built in 36 minutes but your time may vary depending on your PC's specs.

   ```
   make
   ```


The output files can be found in `buildroot/output/images` as follows:

![](README_Photos/18.png)

Our main concern is the sdcard.img file. Its size should be around 150MB.


## Burning The System on an SD Card

1. To burn your image on the SD card, simply use the following command---assuming your sd card is mounted in /dev as sdc:

   ```
   sudo dd if=sdcard.img of=/dev/sdc bs=1M
   ```


2. It can take some time but after it is done, unmount the card and then mount it again and you will see it divided into two partitions: boot and root.


## Testing the System

1. Insert your SD card into the Pi, connect your USB to TTL to both the Pi and your PC, then open your serial terminal of choice. I used `gtkterm` here.

   ```
   gtkterm -p /dev/ttyUSB0 -s 115200
   ```

2. You should see it boot and then get greeted with a login prompt from buildroot. Enter the username as `root` and it will get you into the shell.

   ![](README_Photos/21.png)



## **BONUS**: Exploring Features Available in `menuconfig`, Adding Them to the Final Image, and Testing them One by One

1. I opened the TUI configuration menu and turned on the following features:
   1. gdb
   2. valgrind
   3. git
   4. make
   5. ascii_invaders (apparently, there is a BUILT-IN option in Buildroot to add games to your final image for some reason!)
   6. Python3
   7. `file` shell command
   8. htop
   9. nano

       ![](README_Photos/1.png)
       ![](README_Photos/2.png)
       ![](README_Photos/3.png)
       ![](README_Photos/4.png)
       ![](README_Photos/5.png)
       ![](README_Photos/6.png)
       ![](README_Photos/7.png)
       ![](README_Photos/8.png)
       ![](README_Photos/9.png)
       ![](README_Photos/10.png)
       ![](README_Photos/11.png)
       ![](README_Photos/12.png)
       ![](README_Photos/13.png)
       ![](README_Photos/14.png)
       ![](README_Photos/15.png)
       ![](README_Photos/16.png)



**VERY IMPORTANT:** Before adding more functionality, make sure you expand the root's size (default is 150MB, I believe). I made mine 8GB just because I use a 64GB SD card. But, as a result, the final image has become 8GB which is not ideal at all! You definitely do not need to make it 8GB but you still has to make it larger than the default size.

  ![](README_Photos/19.png)
  ![](README_Photos/20.png)

       
2. The compilation/build process took about 38 minutes. I made sure to use `time` command before `make` to see how long it took.

   ```
   time make
   ```

   ![](README_Photos/17.png)


3. Now, burn the generated `sdcard.img` on your SD card. This time, I recommend using a `bs` option larger than 1M to speed things up. I used `bs=100M` for my 8GB image and it took 700 seconds---or roughly 11.5 minutes---to complete.

   ```
   sudo dd if=sdcard.img of=/dev/sdc bs=100M
   ```


4. Finally, we can boot it. Down below are screenshots showcasing most of the features I added to the final image.
       ![](README_Photos/23.png)
       ![](README_Photos/24.png)
       ![](README_Photos/25.png)
       ![](README_Photos/26.png)
       ![](README_Photos/27.png)
       ![](README_Photos/28.png)
       ![](README_Photos/29.png)
       ![](README_Photos/30.png)
       ![](README_Photos/31.png)

