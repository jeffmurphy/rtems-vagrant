# Hello World Source

```
/*
 *  Simple test program -- simplified version of sample test hello.
 *
 *  $Id$
 */

#include <bsp.h>

#include <stdlib.h>
#include <stdio.h>

rtems_task Init(
  rtems_task_argument ignored
)
{
  printf( "\n\n*** HELLO WORLD TEST ***\n" );
  printf( "Hello Syn-tax Collectors!\n" );
  printf( "*** END OF HELLO WORLD TEST ***\n" );
  exit( 0 );
}

/* configuration information */

/* NOTICE: the clock driver is explicitly disabled */
#define CONFIGURE_APPLICATION_DOES_NOT_NEED_CLOCK_DRIVER
#define CONFIGURE_APPLICATION_NEEDS_CONSOLE_DRIVER

#define CONFIGURE_RTEMS_INIT_TASKS_TABLE
#define CONFIGURE_MAXIMUM_TASKS 1

#define CONFIGURE_INIT

#include <rtems/confdefs.h>

/* end of file */
```

# Build (sis)

We can build hello world using:

```
sparc-rtems4.10-gcc --pipe -B/home/vagrant/development/rtems/4.10/sparc-rtems4.10/erc32/lib/ -specs bsp_specs -qrtems   -g -Wall  -O2 -g -g    -mcpu=cypress       -mcpu=cypress   -o o-optimize/hello.exe  o-optimize/test.o        
sparc-rtems4.10-nm -g -n o-optimize/hello.exe > o-optimize/hello.num
sparc-rtems4.10-size o-optimize/hello.exe
   text	   data	    bss	    dec	    hex	filename
 117984	   1796	   4112	 123892	  1e3f4	o-optimize/hello.exe
cp o-optimize/hello.exe o-optimize/hello.ralf
```

We can test using 

```
sparc-rtems4.10-gdb ./hello/hello_world_c/o-optimize/hello.exe
(gdb) tar sim
(gdb) load ./hello/hello_world_c/o-optimize/hello.exe
(gdb) run
```

# Build (leon3)

We can build hello world using:

```
sparc-rtems4.10-gcc --pipe -B/home/vagrant/development/rtems/4.10/sparc-rtems4.10/leon3/lib/ -specs bsp_specs -qrtems   -g -Wall  -O2 -g -g    -mcpu=cypress -msoft-float       -mcpu=cypress -msoft-float   -o o-optimize/hello.exe  o-optimize/test.o        
sparc-rtems4.10-nm -g -n o-optimize/hello.exe > o-optimize/hello.num
sparc-rtems4.10-size o-optimize/hello.exe
   text	   data	    bss	    dec	    hex	filename
 128016	   1620	   4192	 133828	  20ac4	o-optimize/hello.exe
cp o-optimize/hello.exe o-optimize/hello.ralf
```
  
We can test using the TSIM LEON3 simulator (demo) from Aeroflex Gaisler:

```
$ ~/tsim-eval/tsim/linux-x64/tsim-leon3 `find . -name hello.exe`

 This TSIM evaluation version will expire 2015-06-15


 TSIM/LEON3 SPARC simulator, version 2.0.36 (evaluation version)

 Copyright (C) 2014, Aeroflex Gaisler - all rights reserved.
 This software may only be used with a valid license.
 For latest updates, go to http://www.gaisler.com/
 Comments or bug-reports to support@gaisler.com

serial port A on stdin/stdout
allocated 4096 K SRAM memory, in 1 bank
allocated 32 M SDRAM memory, in 1 bank
allocated 2048 K ROM memory
icache: 1 * 4 kbytes, 16 bytes/line (4 kbytes total)
dcache: 1 * 4 kbytes, 16 bytes/line (4 kbytes total)
section: .text, addr: 0x40000000, size 128016 bytes
section: .data, addr: 0x4001f410, size 1616 bytes
section: .jcr, addr: 0x4001fa60, size 4 bytes
read 1312 symbols
tsim> run
starting at 0x40000000


*** HELLO WORLD TEST ***
Hello Syn-tax Collectors!
*** END OF HELLO WORLD TEST ***


Program exited normally.
```



