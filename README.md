# MIT_OS_6.828
Operating Systems course from MIT OS 6.828  

Steps to make and install qemu and xv6 on Fedora 32:  
  1. Packages I needed that F32 lacked  
    a. $ sudo yum install gtk2-devel  
    b. $ sudo dnf install zlib-dev  
    c. Install latest python2.7  
    
  2. QEMU  
    a. '$ git clone http://pdos.csail.mit.edu/6.828/qemu.git -b 6.828-0.15'  
    b. CD into the directory and run: '$ ./configure --disable-kvm [--prefix=PFX] [--target-list="i386-softmmu x86_64-softmmu"]'  
      i. The prefix argument specifies where to install QEMU; without it QEMU will install to /usr/local by default. The target-list argument simply slims down the architectures QEMU will build support for.  
    c. '$ sudo make && sudo make install'  
    
  3. xv6  
    a. '$ git submodule add git://github.com/mit-pdos/xv6-public.git <xv6>'  
    b. In qga/commands-posix.c, add #include <sys/sysmacros.h>  
    c. '$ make'  
    d. Recent GDB versions will not automatically load .gdbinit files anymore for security reasons. You have four choices to proceed (I chose option ii):  
      i. Add "add-auto-load-safe-path /absolute/path/to/.gdbinit" to your ~/.gdbinit to enable autoloading of only this file (good if you use GDB in untrusted codebases).  
      ii. You can completely disable the security check and tell GDB to load any .gdbinit file automatically by adding "set auto-load safe-path /" to your
 ~/.gdbinit.  
      iii. You can explicitly tell GDB to load the file by running "gdb -x .gdbinit" every time.  
      iv. You can manually run the commands in .gdbinit every time.  
    
  4. How to Run It   
    a. $ make qemu   
        i. runs with vga display; terminal echos vga display  
    b. $ make qemu-nox  
        ii. runs output in terminal only  
    c. $ make qemu-gdb    
        i. runs with gdb   
        ii. to make it work, run (c) in one terminal and then run '$ gdb' in another terminal in the same directory  
        iii. Initially, the vga display will not have a connection. This is fine. If you run 'si' repeatedly or 'c' in the second terminal where you have gdb running you will eventually load the kernel (which subsequently sets up the vga display). Really cool stuff.  
        
  Final Notes:  
    I believe these are the steps of how I got it working (it took a bit of time for me and so I do not remember the exact ordering of steps, but I think this list is a faithful representation of everything you need to do on Fedora 32). Feel free to contact me if something doesn't work.    
      
      
      
