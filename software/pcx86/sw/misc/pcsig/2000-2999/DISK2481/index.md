---
layout: page
title: "PC-SIG Library Disk #2481"
permalink: /software/pcx86/sw/misc/pcsig/2000-2999/DISK2481/
machines:
  - id: ibm5170
    type: pcx86
    config: /machines/pcx86/ibm/5170/cga/1024kb/rev3/machine.xml
    diskettes: /machines/pcx86/diskettes.json,/disks/pcsigdisks/pcx86/diskettes.json
    autoGen: true
    autoMount:
      B: "PC-SIG Library Disk #2481"
    autoType: $date\r$time\rB:\rDIR\r
---

{% include machine.html id="ibm5170" %}

{% comment %}info_begin{% endcomment %}

## Information about "PRINTGL & SOFT87"

    PRINTGL prints an HP-GL (Hewlett-Packard Graphics Language - HP 7475
    subset) plotfile on a matrix printer. HP-GL is widely supported by
    graphics programs including AutoCAD, Generic CADD, MathCAD, SAS,
    MICROCADAM, Schema, and many more. PRINTGL has native mode drivers for
    Epson and NEC compatible 9 and 24 pin dot matrix printers, HP Laserjet,
    Deskjet, and PaintJet, and IBM 9 and 24 pin Proprinters, Quietwriter 2
    and 3, and LaserPrinter. It will also display plots with a CGA, EGA,
    VGA, enhanced VGA, or HGC and output a bit map or GEM .IMG file.
    
    Even if your graphics program supports your printer, you may find that
    PRINTGL gives better print quality. PRINTGL uses the best graphics
    modes available for each printer that it supports. If you need printed
    graphics output from personal software, you can output HP-GL and use
    PRINTGL to do the printing. This gives immediate support to a wide range
    of printers.
    
    PRINTGL Menu Interface (PMI), included with PRINTGL, gives you easy
    access to PRINTGL's many options, and lets you select a list of
    plotfiles to print.
    
    SOFT87 is a memory resident math coprocessor emulator that emulates
    floating point calculations(80287, 802387) on your 286, or 386
    computers.  It is one of the cheapest ways to acquire math coprocessing
    capabilities.
    
    SOFT87 is designed for those who do not have an 80x87 (8087,
    80287,80387) installed on their computers, but want to use programs
    that require an 80x87, or write programs with 80x87 instructions.
    
    This program will work with MS-DOS, PC-DOS, MS Windows or DESQview
    SOFT87 is a Once loaded into memory, SOFT87 stays there until you turn
    off the computer. After loading SOFT87, the 80x87 instructions can be
    executed directly even without an 80287 or 80387 installed in the
    computer. Then you can run programs that require an 80287 or 80387, such
    as AutoCAD R9, AutoCAD R10, PSpice, PC-MATLAB, ASYST, Auto sketch and
    PC-SIMNON.
    
    The registered version of SOFT87 provides 57 extended instructions that
    cannot be found in other coprocessors. These extended instructions will
    simplify program design and shorten programming time.
    
    With typical co-processors costs between $200(80287-10) to
    $500(80387-33), you can't afford not to try SOFT87, since it will save
    you money even after you register it.
{% comment %}info_end{% endcomment %}


### Directory of PC-SIG Library Disk #2481

     Volume in drive A has no label
     Directory of A:\

    GO       BAT        40   1-01-80   6:00a
    GO       TXT      2003  11-19-90   7:00a
    FILE2481 TXT      4959  11-01-90   5:07p
    SOFT87   COM     14562   5-05-90
    SOFT87   DOC      4853  10-05-90   2:26p
    README   BAT        85   9-01-90   1:12a
    README   1        1185   9-01-90   1:12a
    README   2        1024   9-01-90   1:12a
    README   3        1122   9-01-90   1:12a
    PRINTGL  EXE     65216  10-19-90   1:12a
    PMI      EXE     34688   9-01-90   1:12a
    PRINTGL  DOC     85448   9-01-90   1:12a
    CHARSET  PLT      7609   9-01-90   1:12a
    SAMPLE   PLT      1525   9-01-90   1:12a
           14 file(s)     224319 bytes
                           91136 bytes free