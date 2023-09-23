# Basic_Buildroot_Image_for_RPi4

This is a Buildroot image generated for Raspberry Pi 4. This README file shall contain all the steps I took in order to generate it, as well as screenshots for the system's output.

Notes:

  1. This system was built on 22/9/2023. Some steps may differ/be omitted altogether. Please, bare in mind that Buildroot is a piece of software that gets updated constantly and your steps may vary depending on when you decide to build/use it.
     
  2. This system was built on an Ubuntu 22.04 system on my trusty ten-year-old PC with the following specs:

       1. i7 4790k @4.4GHz
       1. 16GB DDR3 RAM @2400MHz
       1. GTX 980ti (irrelevant to this project) 
       1. A Kingston HyperX Savage SSD.
       
       ![](README_Photos/drip.png)
     
 Note that build time may vary depending on your hardware.
 
  3. The source I followed is Chris Simmond's book "Mastering Embedded Linux Programming - Second Edition" chapter 6: Selecting a Build System. It is a fantastic book that I STRONGLY recommend. But, bear in mind that the instructions listed in the chapter are for Beaglebone Black. If you use any other single board computer, you are on your own. If you decide to use Raspberry Pi 4, you came to the right place comrade.
