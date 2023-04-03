---
layout: page
title: "PC-SIG Library Disk #54"
permalink: /software/pcx86/sw/misc/pcsig/0001-0999/DISK0054/
machines:
  - id: ibm5150
    type: pcx86
    config: /machines/pcx86/ibm/5150/cga/256kb/machine.xml
    diskettes: /machines/pcx86/diskettes.json,/disks/pcsigdisks/pcx86/diskettes.json
    autoGen: true
    autoMount:
      B: "PC-SIG Library Disk 0054"
    autoType: $date\r$time\rB:\rDIR\r
---

{% include machine.html id="ibm5150" %}

{% comment %}info_begin{% endcomment %}

## Information about "XMODEM"

    XMODEM is a communications program that imposes no restrictions on
    the contents of the data being transmitted.  Any kind of data may be
    sent-- binary, ASCII, etc.
    
    This IBM Asynchronous Communication Support Program provides software
    needed to allow the personal computer to communicate with a wide variety
    of computer systems including several IBM mainframe computers.  It
    emphasizes great flexibility in communications and provides a protocol
    for file transfer between personal computers.
    
    The user must be technically competent in communications protocol to be
    able to properly set selectable  parameters provided through various
    menus.  A user-friendly design has been substantially ignored.
    
    Features:
    ~ A 64K version named SHORTERM.BAS, and a 96K version
    named LONGTERM.BAS
    ~ Automatic selection of screen width and an option to
    bypass all intermediate menus
    ~ Preselected parameters for Display Selection and Dialing
    Option for the Hayes Smartmodem
    ~ Download capability, including error trapping, file
    directory printout, On/Off switching of data recording
    for open files, and status indicator
    ~ Upload capability, including error trapping, file directory
    printout, On/Off switching, status indication
    ~ Time/Date/Status line
    ~ Telephone/LOG-ON menu and function
    ~ Automatic enabling of error messages upon terminal startup
    ~ Error trapping routines supported in many areas for printer
    applications
    ~ Changes to preset terminal parameters, facilitating program
    initialization in full duplex mode and bypassing of menus.
    
    System Requirements:  Some programs require BASIC; two disk drives,
    modem
    
    How to Start:  From DOS, enter TYPE TUTORIAL to access a tutorial on
    IBM ASYNC COM PROGRAM.  To read the documentation on XMODEM, enter
    TYPE MODEM.DOC. To run it, type XMODEM and press <ENTER>.
    
    File Descriptions:
    
    TUTORIAL      Tutorial for IBM ASYNC COM PROGRAM
    DESCRIPT ION  Description for IBM ASYNC COM PROGRAM modifications
    PROGRAMN OTE  Programming notes for IBM ASYNC COM PROGRAM modifications
    LONGTERM BAS  96K version - see PROGRAMN.OTE
    SHORTERM BAS  64K version - see PROGRAMN.OTE
    XMODEM   DOC  Documentation for XMODEM.COM
    XMODEM   ASM  Source code  (52K)
    -------- ---  XMODEM
    PROFEEL       Sony Profeel monitor modifications (Text file)
    XMODEM   COM  Modem communication program  (DOS 1.1)
{% comment %}info_end{% endcomment %}

{% comment %}samples_begin{% endcomment %}

## LONGTERM.BAS

```bas
1 'LONGTERM.BAS ....Enhancements to IBM Async. Comm.   V1.02   (96KB)  4/24/82
2 'By Robert C. Rice, Upload/Download based on a program by Morris E. Thompson
115 DEF SEG=&H1700
200 CLEAR
210 IDSEG=&H1700
223 IF LEFT$(TIME$,4)="00:0" THEN NTME=TRUE ELSE NTME=FALSE
330 DIM ERM$(21) 'error msg array
400 DIM TRMNL$(ICN+1)
410 TRMNL$(1)="IBM VM/370"
420 TRMNL$(2)="IBM MVS TSO"
430 TRMNL$(3)="Half Duplex"
440 TRMNL$(4)="Full Duplex"
450 TRMNL$(5)="PC Computer"
460 TRMNL$(6)="User Defined"
605 DATA 1,1,0,0,0,0,1,0,0,0,0,0,0,0,0,1,1,0,0,0
615 DATA 1,1,0,0,0,0,1,0,0,0,0,0,0,0,0,1,1,0,0,0
625 DATA 1,1,1,0,0,0,1,1,0,1,1,1,0,0,1,1,1,0,0,0
635 DATA 1,1,1,0,0,1,1,0,1,1,1,1,0,0,1,1,1,0,0,0
645 DATA 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,0,0,0
745 DATA 4,4,1,0,1,0,1,2,0,3,6,1,0,1,1,0,1,0,0,0
755 DATA 4,4,1,0,2,2,1,0,1,2,5,6,0,2,5,0,1,0,0,0
765 DATA 4,4,1,0,1,0,1,2,0,3,6,1,0,0,1,0,1,0,0,0
775 DATA 4,3,1,0,2,1,1,0,2,2,3,7,0,0,1,0,1,0,0,0
781 DATA 4,3,1,0,2,1,1,0,1,1,1,1,0,3,1,0,1,0,0,0
866 NA$(16)="Select Display"
867 NA$(17)="Select Modem Dial Option"
937 VDO=40:DEF SEG=0:IF(PEEK(&H410)AND &H30)=&H30 THEN IWT=80 ELSE IWT=VDO
938 WIDTH IWT:LOCATE 10,1,0:IF IWT=80 THEN S1PC=INT(IWT/4)+2 ELSE S1PC=1
939 PRINT SPC(S1PC):PRINT"       The IBM Personal Computer"
940 PRINT SPC(S1PC):PRINT"  Asynchronous Communications Support"
941 PRINT SPC(S1PC):PRINT"This 96KB Version Modified and Enhanced"
942 PRINT SPC(S1PC):PRINT"           by Robert C. Rice"
943 PRINT SPC(S1PC):PRINT"   Upload/Download based on a program"
944 PRINT SPC(S1PC):PRINT"         by Morris E. Thompson"
945 PRINT:PRINT
949 IF IWT=80 THEN S2PC=INT(IWT/4)+6 ELSE S2PC=5
950 COLOR 15,0:LOCATE ,S2PC
960 PRINT "Bypass intermediate menus (y/n)?";:COLOR 7,0
961 K$=INKEY$:IF K$="" THEN 961
965 IF K$="y" OR K$="Y" THEN OP1T=1:GOTO 970
966 IF K$="n" OR K$="N" THEN OP1T=0 ELSE GOSUB 20400:GOTO 961
1050 IF OP1T=0 THEN GOSUB 20200 ELSE IMEN=4:GOTO 1065
1066 TMSL$=TRMNL$(IMEN)
1170 TITLE$=TMSL$+" Terminal Feature"
1185 IF OP1T=0 THEN GOSUB 20200 ELSE IMEN=IMAX-2:GOTO 1500
1520 ON IP GOSUB 6000,6200,6400,9000,6800,7000,7200,7400,7500,7600,7625,7660,9000,9000,7800,7900,8000,9000,9000,9000
1800 GOSUB 35000 'Init. Term. Operation
1811 BKS$=CHR$(8):ENDD$=CHR$(79):HMNU$=CHR$(35):SMART=TRUE
1812 SNRC$=CHR$(31):HELP$=CHR$(63):IDSW$=CHR$(64):PRSW$=CHR$(65):LGSW$=CHR$(68)
1813 PLMX$=CHR$(25):UPSW$=CHR$(67):DIAL$=CHR$(66):HOME$=CHR$(71):BCSR$=CHR$(75)
1820 IDPR=FALSE:IPRR=FALSE:IPY=FALSE:LON=FALSE:ULON=FALSE:INIT=TRUE
2005 D%=512+ASC(BKS$):CALL SS(C%,T%,D%,E%)
2024 ISS=5:DTA%=1:T%=7:GOSUB 15000:GOSUB 2788
2025 PRINT"Starting up as a "+TMSL$+" Terminal"
2027 X=FRE("x"):PRINT:GOSUB 31000:GOSUB 31130
2480 LOCATE 25,IWT-17,0:PRINT"F5=HELP RECEIVING";:LOCATE 24,1,1
2531 IF LG THEN GOSUB 17310
2551 IF K$=PLMX$ OR K$=DIAL$ OR K$=LGSW$ OR K$=UPSW$ GOTO 2552 ELSE GOTO 2553
2552 E%=0:ERM$(0)="Must be SENDING to use that key":GOSUB 3600:GOTO 2500
2553 IF K$<>PRSW$ GOTO 2555
2554 IF IPRR THEN IPRR=FALSE:PTR$=" " ELSE IPRR=TRUE:PTR$="P"
2555 IF K$=GOMEN$ GOTO 2800
2556 IF K$=HELP$ THEN GOSUB 31000 ELSE IF K$=HMNU$ GOTO 2552
2602 ITEM=POS(X):LOCATE 25,IWT-17,0
2603 PRINT "F5=HELP   SENDING";
2710 CALL BR(C%,E%):PRINT "Break Sent"
2712 ON ERROR GOTO 3440:IF IPRR THEN LPRINT "Break Sent"
2713 ON ERROR GOTO 0
2751 IF K$=HOME$ THEN INIT=TRUE:LGGR=0:RETURN
2752 IF K$=BCSR$ THEN IF LGGR>0 THEN LGGR=LGGR-1:RETURN ELSE RETURN
2753 IF K$=ENDD$ THEN INIT=FALSE:LGGR=4:RETURN
2754 IF K$=HMNU$ THEN GOSUB 32580:RETURN
2755 IF K$=PLMX$ THEN PRINT "Max. Receive Buffer Space Used = ";LM:LM=0:RETURN
2756 IF K$<>LGSW$ THEN 2760
2757 E%=0:IF NOT LG THEN ERM$(0)="Logging File Not Open":GOSUB 3600:RETURN
2758 DNTSY=7:IF LON THEN LON=FALSE ELSE LON=TRUE:DNTSY=31
2759 GOSUB 33010:RETURN
2761 IF K$<>UPSW$ THEN 2765
2762 IF NOT IU THEN GOSUB 17520:RETURN
2763 UNTSY=7:IF ULON THEN ULON=FALSE ELSE ULON=TRUE:UNTSY=31
2764 GOSUB 33010:RETURN
2766 IF K$=HELP$ THEN GOSUB 31000:RETURN
2768 IF K$=DIAL$ AND INIT THEN GOSUB 32000:RETURN
2769 IF K$=DIAL$ AND NOT INIT THEN GOSUB 32420:RETURN
2775 IF IDPR THEN IDPR=FALSE :HXL$=" " ELSE IDPR=TRUE:HXL$="H"
2776 GOSUB 33010:RETURN
2783 IF IPRR THEN IPRR=FALSE ELSE IPRR=TRUE
2784 PTR$=" ":IF IPRR THEN PTR$="P"
2785 GOSUB 33010:RETURN
2803 IMAX=12:IT=MPARM(14)
2808 C$(3)="Return to BASIC (pause)"
2809 IF LG THEN C$(4)="Close log file: "+LG$ ELSE C$(4)="Open log file"
2810 IF IU THEN C$(5)="Close upload file: "+UP$ ELSE C$(5)="Open upload file"
2811 C$(6)="Terminate Comm. go to BASIC"
2812 C$(7)="Terminate Comm. go to DOS"
2813 IF IT=0 THEN IMAX=7:GOTO 2835
2814 C$(8)="Upload   (VM/370,TSO)"
2815 C$(9)="Download (VM/370,TSO)"
2820 C$(10)="Compare  (VM/370,TSO)"
2822 IF IT<3 THEN IMAX=10:GOTO 2835
2825 C$(11)="Transmit a Personal Computer File"
2830 C$(12)="Receive  a Personal Computer File"
2843 IF IMEN>7 AND IMEN<11 AND IT=3 THEN PRINT "Not Used between Personal Computers":GOTO 13370
2844 IF IMEN=2 THEN OP1T=0
2845 ON IMEN GOTO 3400,970,3430,17200,17410,34000,34010,14000,13000,13050,16200,16500
3100 ON ERROR GOTO 3440:IF IPRR THEN LPRINT B$;
3101 ON ERROR GOTO 0
3400 GOSUB 13030:IF JO THEN CALL SN(C%,XON$,E%)
3405 PRINT "Back as a "+TMSL$+" Terminal":IF MPARM(5)=1 GOTO 2601 ELSE GOTO 5000
3430 CLS:PRINT "You are back in BASIC."
3432 PRINT "Use F5 to return to Terminal Operation":KEY 5,"CONT"+CHR$(13):STOP
3435 KEY 5,"":GOTO 2800
3440 IF ERR=24 OR ERR=27 THEN 3445 ELSE 3450
3445 PTR$=" ":IPRR=FALSE:GOSUB 3540:E%=20:GOSUB 3600:GOSUB 33010:RESUME
3450 ON ERROR GOTO 0
3540 ERM$(20)="ERROR ="+STR$(ERR)+" ** Printer off"
3544 RETURN
3815 PRINT STRING$(40," ");
3825 PRINT STRING$(40," ");:LOCATE ,2:PRINT MSTK$(ICMP);
3955 IF (D% AND 4)>0 THEN E%=16:RETURN
5002 TERM$=LE$:TME=61
5106 IF RIGHT$(B$,1)<>BKS$ THEN 5110
5107 IF LEN(B$)>1 THEN B$=LEFT$(B$,LEN(B$)-2) ELSE GOSUB 2720:GOTO 5200
5110 IF LL<>IWT OR B$<>CR$ THEN PRINT B$;ELSE 5200
5113 ON ERROR GOTO 3440
5115 IF IPRR THEN LPRINT B$;
5116 ON ERROR GOTO 0
5200 GOSUB 33000:GOSUB 2590
5201 IF NOT IU GOTO 5205
5202 IF ULON THEN IF ISF THEN GOSUB 17510
5215 GOSUB 2750:IF K$=GOMEN$ GOTO 5290 ELSE GOTO 5030
5265 ON ERROR GOTO 3440:IF IPRR THEN LPRINT K$;
5266 ON ERROR GOTO 0
5290 IF JO THEN CALL SN(C%,XOFF$,E%)
5300 GOTO 2800
7900 'Menu for Display selection
7910 TITLE$="Display"
7920 C$(1)="Monochrome Display"
7930 C$(2)="Color Video Monitor"
7940 IMAX=2
7950 GOSUB 20200
7960 GOSUB 20100
7970 RETURN
8000 'Menu for Modem dial Option
8010 TITLE$="Type of Modem Dialing"
8020 C$(1)="Touch Tone"
8030 C$(2)="Pulse Dialing"
8040 IMAX=2
8050 GOSUB 20200
8060 GOSUB 20100
8070 RETURN
17200 IF LG THEN CLOSE#3:LG$="":LG=FALSE:DLN$=" ":GOTO 2800
17210 CLS:GOSUB 17660:PRINT "What is the name of the local file "
17220 PRINT "to which you wish to log?":PRINT "(ENTER alone returns to Menu)"
17230 INPUT X$:IF X$="" THEN 2800
17240 GOSUB 20300:LG$=Y$:ON ERROR GOTO 17260
17250 OPEN LG$ FOR APPEND AS 3:M$="":GOTO 17290
17260 IF ERR=67 THEN M$="Too many files open":GOTO 17280
17270 M$="FILE ACCESS FAILED. BASIC ERROR "+STR$(ERR)
17280 RESUME 17290
17290 ON ERROR GOTO 0:IF M$ <> "" THEN GOSUB 14032:GOTO 17230
17300 DLN$="L":DNTSY=31:LG=TRUE:LON=TRUE:GOTO 2800
17310 ON ERROR GOTO 17370
17320 IF NOT LON GOTO 17400 ELSE IF (LEN(LL$)+LEN(B$))<=255 GOTO 17350
17330 LLN=LEN(LL$):LL$=LL$+LEFT$(B$,255-LLN):PRINT#3,LL$
17340 LL$="":B$=RIGHT$(B$,LEN(B$)-255-LLN))
17350 LL$=LL$+B$:IF R$<>CR$ AND R$<>LE$ GOTO 17400
17360 PRINT#3,LEFT$(LL$,LEN(LL$)-1):LL$="":GOTO 17400
17370 IF ERR=61 THEN ERM$(0)="Disk full, Log file closed":GOTO 17390
17380 ERM$(0)="Disk Error, BASIC Err= "+STR$(ERR)
17390 E%=0:GOSUB 3600:LG=FALSE:LON=FALSE:DLN$=" ":GOSUB 33010:RESUME NEXT
17400 ON ERROR GOTO 0:RETURN
17405 'Upload
17410 IF IU THEN CLOSE#1:UP$="":IU=FALSE:ULON=FALSE:ULN$=" ":GOTO 2800
17420 CLS:GOSUB 17660:PRINT "What is the name of the local file "
17430 PRINT "which you wish to upload?":PRINT "(ENTER alone returns to Menu)"
17440 INPUT X$:IF X$="" THEN 2800 ELSE GOSUB 20300:LET UP$=Y$
17450 ON ERROR GOTO 17460:OPEN "I",1,UP$:M$="":GOTO 17490
17460 IF ERR=53 THEN M$="File "+UP$+" not found":GOTO 17480
17470 M$="File access failed. BASIC error "+STR$(ERR)
17480 RESUME 17490
17490 ON ERROR GOTO 0:IF M$<>"" THEN GOSUB 14032:GOTO 17440
17500 IU=TRUE:UNTSY=7:ULN$="U":ULON=FALSE:GOTO 2800
17510 T%=1:CALL BF(C%,T%,D%,E%):IF D%<>0 THEN RETURN
17520 IF NOT IU THEN ERM$(0)="Upload not active":E%=0:GOSUB 3600:RETURN
17530 IF EOF(1) THEN CLOSE#1:ERM$(0)="Upload complete, file closed" ELSE 17550
17540 E%=0:GOSUB 3600:IU=FALSE:ULON=FALSE:ULN$=" ":GOSUB 33010:UP$="":RETURN
17550 ON ERROR GOTO 17620:IF UL$="" THEN LINE INPUT#1,UL$:ON ERROR GOTO 0
17560 IF ILE THEN PRINT UL$
17570 ON ERROR GOTO 3440:IF IPRR THEN LPRINT UL$
17580 ON ERROR GOTO 0
17590 CALL SN(C%,UL$,E%):IF E%>-1 THEN GOSUB 3600
17600 CALL SN(C%,TSEND$,E%):IF E%>-1 THEN GOSUB 3600
17610 UL$="":RETURN
17620 CLOSE#1:UP$="":IU=FALSE:ULON=FALSE:ULN$=" ":GOSUB 33010:E%=0
17630 ERM$(0)="Disk Error, BASIC Err= "+STR$(ERR):GOSUB 3600:RESUME 17640
17640 ON ERROR GOTO 0:RETURN
17650 'Print files
17660 PRINT"If you wish a list of files,":PRINT"enter the drive designator(s),"
17670 PRINT "NO colons, or separators":PRINT "(ENTER alone to bypass)"
17680 INPUT "",DRV$:LDRV=LEN(DRV$):IF LDRV>2 THEN GOSUB 20400:GOTO 17660
17690 IF LDRV=0 GOTO 17740
17700 IF LDRV=1 THEN DR1$=DRV$ ELSE DR1$=LEFT$(DRV$,1):DR2$=RIGHT$(DRV$,1)
17710 ON ERROR GOTO 17750:FL1CK$=DR1$+":*.*":FL2CK$=DR2$+":*.*"
17720 CLS:PRINT "Drive ";DR1$:FILES FL1CK$:PRINT :PRINT
17730 IF LDRV=2 THEN PRINT "Drive ";DR2$:FILES FL2CK$:PRINT:PRINT
17740 ON ERROR GOTO 0:RETURN
17750 IF (ERL=17720)AND(ERR=53) THEN BEEP ELSE 17770
17760 CLS:PRINT"No files found":RESUME 17660
17770 IF (ERL=17720)AND(ERR=71) THEN BEEP ELSE 17790
17780 PRINT"Drive "+DR1$+" not ready":PRINT:RESUME 17660
17790 IF ERL=17720 THEN BEEP:PRINT "BASIC Error "+STR$(ERR):PRINT:RESUME 17730
17800 IF ERR=53 THEN BEEP ELSE 17820
17810 PRINT"No files found":PRINT:RESUME 17660
17820 IF ERR=71 THEN BEEP:PRINT"Drive "+DR2$+" not ready":RESUME 17660
17830 BEEP:PRINT "BASIC Error "+STR$(ERR):RESUME NEXT
30640 'Function key Help Menu
31000 COLOR 15:PRINT "F1 ";:COLOR 7:PRINT "- Send Break to Host"
31010 COLOR 15:PRINT "F2 ";:COLOR 7:PRINT "- Function Selection Menu"
31020 COLOR 15:PRINT "F3 ";:COLOR 7:PRINT "- Display Next Error Msg."
31030 COLOR 15:PRINT "F4 ";:COLOR 7:PRINT "- Error ON/OFF Switch"
31040 COLOR 15:PRINT "F5 ";:COLOR 7:PRINT "- Display Function Key Menu"
31050 COLOR 15:PRINT "F6 ";:COLOR 7:PRINT "- Hex Listing ON/OFF Switch"
31060 COLOR 15:PRINT "F7 ";:COLOR 7:PRINT "- Printer ON/OFF Switch"
31070 COLOR 15:PRINT "F8 ";:COLOR 7:PRINT "- Telephone/LOG-ON Menu"
31080 COLOR 15:PRINT "F9 ";:COLOR 7:PRINT "- Upload ON/OFF Switch"
31090 COLOR 15:PRINT "F10";:COLOR 7:PRINT "- Log File ON/OFF Switch"
31100 COLOR 15:PRINT "ALT H ";:COLOR 7:PRINT "- Telephone/LOG-ON Help Menu"
31110 COLOR 15:PRINT "ALT P ";:COLOR 7:PRINT "- Print Max.Rec.Buf.Used"
31115 COLOR 15:PRINT "ALT S ";:COLOR 7:PRINT "- Force to Send (Half Duplex)"
31116 IF MPARM(5)=2 GOTO 31120 ELSE PRINT"Depress ";:COLOR 15:PRINT"ALT S";
31117 COLOR 7:PRINT" before using ";:COLOR 15:PRINT"F6, F8-F10":COLOR 7
31120 PRINT:RETURN
31130 IF NOT SMART GOTO 31150
31140 PRINT "Insure ";:COLOR 15 :PRINT "CAPS LOCK ";:COLOR 7:PRINT"is on"
31150 PRINT "Depress ";:COLOR 15:PRINT "F2 ";:COLOR 7:PRINT "to open ";
31160 COLOR 15:PRINT "Log/Upload ";:COLOR 7:PRINT "files"
31170 PRINT "Use ";:COLOR 15:PRINT "F7 ";:COLOR 7:PRINT "if printout desired"
31180 PRINT "Depress ";:COLOR 15,0:PRINT "F8 ";:COLOR 7:PRINT "for ";
31190 COLOR 15:PRINT"Telephone/LOG-ON ";:COLOR 7:PRINT "menu":PRINT:RETURN
32000 LOCATE 24,1:FOR CLEER=0 TO 24:PRINT:NEXT CLEER:LGGR=0:TLN=9 'Max. 9
32010 X=FRE("x"):IF TLN=1 THEN TELE=1:GOTO 32160
32020 COLOR 15,0:PRINT "Enter ";:COLOR 7,0:PRINT "phone # ";:COLOR 15,0
32030 PRINT "selection ";:COLOR 7,0:PRINT "Depress ":COLOR 15
32040 PRINT "ESC";:COLOR 7:PRINT "ape to ";
32050 COLOR 15:PRINT "return ";:COLOR 7:PRINT "as a Terminal"
32060 PRINT:RESTORE 32320:FOR SELEC=1 TO TLN
32070 READ CPNY$,UL$,CTY$,TELCO$,GO,LOGIN$,IDPSW$:GOSUB 32090
32080 NEXT:PRINT:GOTO 32120
32090 COLOR 15,0:PRINT RIGHT$(STR$(SELEC),1);" ";:COLOR 7,0:GOSUB 32100:RETURN
32100 PRINT USING "\      \";CPNY$+" ";:PRINT UL$;" ";
32110 PRINT USING "\           \";CTY$+" ";TELCO$:RETURN
32120 DL$=INKEY$:TELE=VAL(DL$)
32130 IF DL$="" THEN GOSUB 33000:GOTO 32120
32140 IF DL$=CHR$(27) THEN GOSUB 32200:GOTO 3405
32150 IF (TELE<1) OR (TELE>TLN) THEN GOSUB 20400:GOTO 32120
32160 RESTORE 32320:FOR SELECT=1 TO TELE
32170 READ CPNY$,UL$,CTY$,TELCO$,GO,LOGIN$,IDPSW$:NEXT:IF NOT SMART GOTO 32270
32180 IF MPARM(17)=1 THEN UL$="ATDT"+UL$ ELSE UL$="ATDP"+UL$
32190 GOSUB 17590:GOSUB 32200:GOTO 32220
32200 LOCATE 24-(TLN+1),1,0:FOR CLEER=0 TO 24:PRINT STRING$(79," ")
32210 NEXT CLEER:LOCATE ,,1:RETURN
32220 COLOR 15,0:PRINT CPNY$;:COLOR 7,0
32230 PRINT " is being called via ";:COLOR 15,0:PRINT TELCO$:COLOR 7,0
32240 PRINT "To redial, Depress ";:COLOR 15,0:PRINT "HOME ";
32250 COLOR 7,0:PRINT "and ";:COLOR 15,0:PRINT "F8 ";
32260 COLOR 7,0:PRINT "and Redo":PRINT:GOTO 32280
32270 GOSUB 32200:PRINT"Place Call to "+CPNY$+" via "+TELCO$:PRINT"Ph. # "+UL$
32280 PRINT "Operating as "+TMSL$+" Terminal":PRINT"After CONNECT, use ";:COLOR 15
32290 PRINT"F8 ";:COLOR 7:PRINT "to ";:COLOR 15:PRINT "LOG-ON.":COLOR 7:PRINT
32300 ON ERROR GOTO 3440:IF IPRR THEN LPRINT CPNY$+" being called via ";TELCO$
32310 ON ERROR GOTO 0:INIT=FALSE:UL$="":RETURN
32320 DATA SOURCE,986-9503,Van Nuys,TYMNET,1,SOURCE11;PRIM;,ID TCA123 PASWRD
32330 DATA SOURCE,986-9803,Van Nuys,TYMNET,1,SOURCE11;PRIM;,ID TCA123 PASWRD
32340 DATA SOURCE,365-9277,Mission Hls,TYMNET,1,SOURCE11;PRIM;,ID TCA123 PASWRD
32350 DATA SOURCE,998-3331,Northridge,TYMNET,1,SOURCE13;PRIM;,ID TCA123 PASWRD -ON SYS11
32360 DATA SOURCE,992-0144,Woodland Hls,TELENET,2,C 30138,ID TCA123 PASWRD
32370 DATA SOURCE,822-9287,Canoga Park,TELENET,2,C 30138,ID TCA123 PASWRD
32380 DATA CSERVE,892-7211,Van Nuys,CSERVE,3,"77000,1100",PASS/WORD
32390 DATA CSERVE,781-8439,San Fernando,CSERVE,3,"77000,1100",PASS/WORD
32400 DATA CSERVE,365-2013,Mission Hls,TYMNET,4,"77000,1100",PASS/WORD
32410 DATA CSERVE,998-4872,Northridge,TYMNET,4,"77000,1100",PASS/WORD
32420 IF LGGR<>0 GOTO 32510 ELSE ON GO GOTO 32430,32440,32450,32460,32470,32500
32430 UUL$="A":GOSUB 32570:LGGR=1:RETURN
32440 UUL$=CHR$(13):GOSUB 32570:FOR D2LY=0 TO 500:NEXT:GOSUB 32570:GO=6:RETURN
32450 UUL$=CHR$(3):GOSUB 32570:LGGR=1:RETURN
32460 UUL$="A":GOSUB 32570:GO=GO+1:RETURN
32470 PRINT "Type CIS02 and ENTER for non-prime time"
32480 PRINT "Type CPS01 and ENTER for prime time use":PRINT
32490 PRINT "Use F8 key for rest of LOG-ON":LGGR=1:RETURN
32500 UL$="D1":GOSUB 17590:LGGR=1:RETURN
32510 ON LGGR GOTO 32520,32530,32540,32550
32520 UL$=LOGIN$:GOSUB 17590:LGGR=LGGR+1:RETURN
32530 UL$=IDPSW$:GOSUB 17590:LGGR=LGGR+1:RETURN
32540 E%=0:ERM$(0)="ERROR * Use ALT H for F8 Help Menu":GOSUB 3600:RETURN
32550 PRINT "DISCONNECTING":UUL$="+++":GOSUB 32570:FOR D2LY=0 TO 3000:NEXT
32560 UL$="ATH":GOSUB 17590:LGGR=0:INIT=TRUE:RETURN
32570 CALL SN(C%,UUL$,E%):IF E%>-1 THEN GOSUB 3600 ELSE RETURN
32580 PRINT :PRINT :COLOR 15:PRINT"  Telephone/LOG-ON Help Menu":COLOR 7:PRINT
32590 COLOR 15:PRINT "HOME ";:COLOR 7:PRINT "- Enables F8 from the beginning"
32600 PRINT "       telephone dialup menu.":PRINT
32610 COLOR 15:PRINT "F8   ";:COLOR 7:PRINT "- After dialup, Depress F8 "
32620 PRINT "       in response to LOG-ON requests.":PRINT
32630 COLOR 15:PRINT CHR$(27)+"--  ";:COLOR 7:PRINT "- Cursor left  (Numeric 4)
32640 PRINT "       Return to previous entry,"
32650 PRINT "       using Function Key F8.":PRINT
32660 COLOR 15:PRINT "END  ";:COLOR 7:PRINT "- Enables last entry using F8"
32670 PRINT "       (Hang up the phone)":PRINT :PRINT :RETURN
33000 IF VAL(MID$(TIME$,4,2))=TME THEN RETURN
33010 IF MPARM(5)<>2 THEN RETURN
33020 ITEM=POS(X):ICSR=CSRLIN:CLMN=IWT-(LEN(TIME$)+LEN(DATE$)+17)
33030 TMME$=LEFT$(TIME$,5):TME=VAL(RIGHT$(TMME$,2))
33040 HOUR=VAL(LEFT$(TMME$,2)):IF HOUR=0 THEN HOUR=12:APM$="AM ":GOTO 33070
33050 IF HOUR>12 THEN HOUR=HOUR-12:APM$="PM ":GOTO 33070
33060 IF HOUR=12 THEN APM$="PM " ELSE APM$="AM "
33070 HR$=STR$(HOUR):TMME$=HR$+RIGHT$(TMME$,3)+APM$
33080 LOCATE 25,CLMN,0:COLOR 15,0:PRINT USING "\\";HXL$;:PRINT USING "\\";PTR$;
33090 COLOR UNTSY:PRINT USING "\\";ULN$;:COLOR DNTSY:PRINT USING "\\";DLN$;
33100 COLOR 7,0:PRINT "F5=HELP ";:IF NOT NTME THEN PRINT TMME$;
33110 IF LEFT$(DATE$,2)<>"00" THEN PRINT DATE$;
33120 LOCATE ICSR,ITEM,1:RETURN
34000 GOSUB 34050:GOSUB 34040:CLS:NEW
34010 GOSUB 34050:PRINT "Insert DOS diskette in default drive"
34020 PRINT "Depress any key when ready"
34030 K$=INKEY$:IF K$="" THEN 34030 ELSE GOSUB 34040:SYSTEM
34040 CLOSE:OPEN "COM1:" AS 1:RETURN
34050 CLS:PRINT "TERMINATING COMM. PROGRAM"
34060 PRINT "ARE YOU SURE(Y/N)?"
34070 K$=INKEY$:IF K$="" THEN 34070
34080 IF K$="Y" OR K$="y" THEN RETURN
34090 IF K$="N" OR K$="n" THEN 2800
34100 GOSUB 20400:GOTO 34070
35000 IQ=MPARM(16):IF IQ=0 THEN RETURN
35010 ON IQ GOTO 35020,35040
35020 WIDTH 40:LOCATE ,,0:CLS:DEF SEG=0:A=PEEK(&H410):POKE &H410, A OR &H30
35030 WIDTH 80:IWT=80:LOCATE 1,1,0,12,13:RETURN
35040 LOCATE ,,0:CLS:DEF SEG=0:A=PEEK(&H410):POKE &H410,(A AND &HCF) OR &H20
35050 SCREEN 1:SCREEN 0:WIDTH VDO:IWT=VDO:LOCATE ,,0,6,7:RETURN
```

## SHORTERM.BAS

```bas
1 'SHORTERM.BAS ....Enhancements to IBM Async. Comm.   V1.04   (64KB)  4/24/82
2 'By Robert .C Rice, Upload/Download based on a program by Morris E. Thompson
223 IF LEFT$(TIME$,4)="00:0" THEN NTME=TRUE ELSE NTME=FALSE
225 IZF = 17 'max no. of features
235 ICN = 2 'set no. of terminals to be configured
330 DIM ERM$(21) 'error msg array
400 DIM TRMNL$(ICN+1)
410 TRMNL$(1)="Full Duplex"
420 TRMNL$(2)="PC Computer"
430 TRMNL$(3)="User Defined"
635 DATA 1,1,1,0,0,1,1,0,1,1,1,1,0,0,1,1,1
645 DATA 1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1
775 DATA 4,3,1,0,2,1,1,0,2,2,3,7,0,0,1,0,1
781 DATA 4,3,1,0,2,1,1,0,1,1,1,1,0,3,1,0,1
866 NA$(16)="Select Display"
867 NA$(17)="Select Modem Dial Option"
937 VDO=40:DEF SEG=0:IF(PEEK(&H410)AND &H30)=&H30 THEN IWT=80 ELSE IWT=VDO
938 WIDTH IWT:LOCATE 10,1,0:IF IWT=80 THEN S1PC=INT(IWT/4)+2 ELSE S1PC=1
939 PRINT SPC(S1PC):PRINT"       The IBM Personal Computer"
940 PRINT SPC(S1PC):PRINT"  Asynchronous Communications Support"
941 PRINT SPC(S1PC):PRINT"This 64KB Version Modified and Enhanced"
942 PRINT SPC(S1PC):PRINT"           by Robert C. Rice"
943 PRINT SPC(S1PC):PRINT"   Upload/Download based on a program"
944 PRINT SPC(S1PC):PRINT"         by Morris E. Thompson"
945 PRINT:PRINT
949 IF IWT=80 THEN S2PC=INT(IWT/4)+6 ELSE S2PC=5
950 COLOR 15,0:LOCATE ,S2PC
960 PRINT "Bypass intermediate menus (y/n)?";:COLOR 7,0
961 K$=INKEY$:IF K$="" THEN 961
965 IF K$="y" OR K$="Y" THEN OP1T=1:GOTO 970
966 IF K$="n" OR K$="N" THEN OP1T=0 ELSE GOSUB 20400:GOTO 961
1004 C$(1) = "User Specified Full Duplex Term."
1005 C$(2) = "Personal Computer Communications"
1050 IF OP1T=0 THEN GOSUB 20200 ELSE IMEN=1:GOTO 1065
1066 TMSL$=TRMNL$(IMEN)
1170 TITLE$=TMSL$+" Terminal Feature"
1185 IF OP1T=0 THEN GOSUB 20200 ELSE IMEN=IMAX-2:GOTO 1500
1520 ON IP GOSUB 6000,6200,6400,9000,6800,7000,7200,7400,7500,7600,7625,7660,9000,9000,7800,7900,8000,9000,9000,9000
1800 GOSUB 35000 'Init. Term. Operation
1811 BKS$=CHR$(8):ENDD$=CHR$(79):HMNU$=CHR$(35):SMART=TRUE
1812 SNRC$=CHR$(31):HELP$=CHR$(63):IDSW$=CHR$(64):PRSW$=CHR$(65):LGSW$=CHR$(68)
1813 PLMX$=CHR$(25):UPSW$=CHR$(67):DIAL$=CHR$(66):HOME$=CHR$(71):BCSR$=CHR$(75)
1820 IDPR=FALSE:IPRR=FALSE:IPY=FALSE:LON=FALSE:ULON=FALSE:INIT=TRUE
2005 D%=512+ASC(BKS$):CALL SS(C%,T%,D%,E%)
2024 ISS=5:DTA%=1:T%=7:GOSUB 15000:GOSUB 2788
2025 PRINT"Starting up as a "+TMSL$+" Terminal"
2027 X=FRE("x"):PRINT:GOSUB 31000:GOSUB 31130
2531 IF LG THEN GOSUB 17310
2710 CALL BR(C%,E%):PRINT "Break Sent"
2712 ON ERROR GOTO 3440:IF IPRR THEN LPRINT "Break Sent"
2713 ON ERROR GOTO 0
2751 IF K$=HOME$ THEN INIT=TRUE:LGGR=0:RETURN
2752 IF K$=BCSR$ THEN IF LGGR>0 THEN LGGR=LGGR-1:RETURN ELSE RETURN
2753 IF K$=ENDD$ THEN INIT=FALSE:LGGR=4:RETURN
2754 IF K$=HMNU$ THEN GOSUB 32580:RETURN
2755 IF K$=PLMX$ THEN PRINT "Max. Receive Buffer Space Used = ";LM:LM=0:RETURN
2756 IF K$<>LGSW$ THEN 2760
2757 E%=0:IF NOT LG THEN ERM$(0)="Logging File Not Open":GOSUB 3600:RETURN
2758 DNTSY=7:IF LON THEN LON=FALSE ELSE LON=TRUE:DNTSY=31
2759 GOSUB 33010:RETURN
2761 IF K$<>UPSW$ THEN 2765
2762 IF NOT IU THEN GOSUB 17520:RETURN
2763 UNTSY=7:IF ULON THEN ULON=FALSE ELSE ULON=TRUE:UNTSY=31
2764 GOSUB 33010:RETURN
2766 IF K$=HELP$ THEN GOSUB 31000:RETURN
2768 IF K$=DIAL$ AND INIT THEN GOSUB 32000:RETURN
2769 IF K$=DIAL$ AND NOT INIT THEN GOSUB 32420:RETURN
2775 IF IDPR THEN IDPR=FALSE :HXL$=" " ELSE IDPR=TRUE:HXL$="H"
2776 GOSUB 33010:RETURN
2783 IF IPRR THEN IPRR=FALSE ELSE IPRR=TRUE
2784 PTR$=" ":IF IPRR THEN PTR$="P"
2785 GOSUB 33010:RETURN
2803 IMAX=9:IT=MPARM(14)
2808 C$(3)="Return to BASIC (pause)"
2809 IF LG THEN C$(4)="Close log file: "+LG$ ELSE C$(4)="Open log file"
2810 IF IU THEN C$(5)="Close upload file: "+UP$ ELSE C$(5)="Open upload file"
2811 C$(6)="Terminate Comm. go to BASIC"
2812 C$(7)="Terminate Comm. go to DOS"
2813 IF IT=0 THEN IMAX=7:GOTO 2835
2825 C$(8)="Transmit a Personal Computer File"
2830 C$(9)="Receive a Personal Computer File"
2844 IF IMEN=2 THEN OP1T=0
2845 ON IMEN GOTO 3400,970,3430,17200,17410,34000,34010,16200,16500
3100 ON ERROR GOTO 3440:IF IPRR THEN LPRINT B$;
3101 ON ERROR GOTO 0
3400 GOSUB 13030:IF JO THEN CALL SN(C%,XON$,E%)
3405 PRINT "Back as a "+TMSL$+" Terminal":IF MPARM(5)=1 GOTO 2601 ELSE GOTO 5000
3430 CLS:PRINT "You are back in BASIC."
3432 PRINT "Use F5 to return to Terminal Operation":KEY 5,"CONT"+CHR$(13):STOP
3435 KEY 5,"":GOTO 2800
3440 IF ERR=24 OR ERR=27 THEN 3445 ELSE 3450
3445 PTR$=" ":IPRR=FALSE:GOSUB 3540:E%=20:GOSUB 3600:GOSUB 33010:RESUME
3450 ON ERROR GOTO 0
3540 ERM$(20)="ERROR ="+STR$(ERR)+" ** Printer off"
3544 RETURN
3815 PRINT STRING$(40," ");
3825 PRINT STRING$(40," ");:LOCATE ,2:PRINT MSTK$(ICMP);
3955 IF (D% AND 4)>0 THEN E%=16:RETURN
5002 TERM$=LE$:TME=61
5106 IF RIGHT$(B$,1)<>BKS$ THEN 5110
5107 IF LEN(B$)>1 THEN B$=LEFT$(B$,LEN(B$)-2) ELSE GOSUB 2720:GOTO 5200
5110 IF LL<>IWT OR B$<>CR$ THEN PRINT B$;ELSE 5200
5113 ON ERROR GOTO 3440
5115 IF IPRR THEN LPRINT B$;
5116 ON ERROR GOTO 0
5200 GOSUB 33000:GOSUB 2590
5201 IF NOT IU GOTO 5205
5202 IF ULON THEN IF ISF THEN GOSUB 17510
5215 GOSUB 2750:IF K$=GOMEN$ GOTO 5290 ELSE GOTO 5030
5265 ON ERROR GOTO 3440:IF IPRR THEN LPRINT K$;
5266 ON ERROR GOTO 0
5290 IF JO THEN CALL SN(C%,XOFF$,E%)
5300 GOTO 2800
7900 'Menu for Display selection
7910 TITLE$="Display"
7920 C$(1)="Monochrome Display"
7930 C$(2)="Color Video Monitor"
7940 IMAX=2
7950 GOSUB 20200
7960 GOSUB 20100
7970 RETURN
8000 'Menu for Modem dial Option
8010 TITLE$="Type of Modem Dialing"
8020 C$(1)="Touch Tone"
8030 C$(2)="Pulse Dialing"
8040 IMAX=2
8050 GOSUB 20200
8060 GOSUB 20100
8070 RETURN
17200 IF LG THEN CLOSE#3:LG$="":LG=FALSE:DLN$=" ":GOTO 2800
17210 CLS:GOSUB 17660:PRINT "What is the name of the local file "
17220 PRINT "to which you wish to log?":PRINT "(ENTER alone returns to Menu)"
17230 INPUT X$:IF X$="" THEN 2800
17240 GOSUB 20300:LG$=Y$:ON ERROR GOTO 17260
17250 OPEN LG$ FOR APPEND AS 3:M$="":GOTO 17290
17260 IF ERR=67 THEN M$="Too many files open":GOTO 17280
17270 M$="FILE ACCESS FAILED. BASIC ERROR "+STR$(ERR)
17280 RESUME 17290
17290 ON ERROR GOTO 0:IF M$ <> "" THEN GOSUB 14032:GOTO 17230
17300 DLN$="L":DNTSY=31:LG=TRUE:LON=TRUE:GOTO 2800
17310 ON ERROR GOTO 17370
17320 IF NOT LON GOTO 17400 ELSE IF (LEN(LL$)+LEN(B$))<=255 GOTO 17350
17330 LLN=LEN(LL$):LL$=LL$+LEFT$(B$,255-LLN):PRINT#3,LL$
17340 LL$="":B$=RIGHT$(B$,LEN(B$)-255-LLN))
17350 LL$=LL$+B$:IF R$<>CR$ AND R$<>LE$ GOTO 17400
17360 PRINT#3,LEFT$(LL$,LEN(LL$)-1):LL$="":GOTO 17400
17370 IF ERR=61 THEN ERM$(0)="Disk full, Log file closed":GOTO 17390
17380 ERM$(0)="Disk Error, BASIC Err= "+STR$(ERR)
17390 E%=0:GOSUB 3600:LG=FALSE:LON=FALSE:DLN$=" ":GOSUB 33010:RESUME NEXT
17400 ON ERROR GOTO 0:RETURN
17405 'Upload
17410 IF IU THEN CLOSE#1:UP$="":IU=FALSE:ULON=FALSE:ULN$=" ":GOTO 2800
17420 CLS:GOSUB 17660:PRINT "What is the name of the local file "
17430 PRINT "which you wish to upload?":PRINT "(ENTER alone returns to Menu)"
17440 INPUT X$:IF X$="" THEN 2800 ELSE GOSUB 20300:LET UP$=Y$
17450 ON ERROR GOTO 17460:OPEN "I",1,UP$:M$="":GOTO 17490
17460 IF ERR=53 THEN M$="File "+UP$+" not found":GOTO 17480
17470 M$="File access failed. BASIC error "+STR$(ERR)
17480 RESUME 17490
17490 ON ERROR GOTO 0:IF M$<>"" THEN GOSUB 14032:GOTO 17440
17500 IU=TRUE:UNTSY=7:ULN$="U":ULON=FALSE:GOTO 2800
17510 T%=1:CALL BF(C%,T%,D%,E%):IF D%<>0 THEN RETURN
17520 IF NOT IU THEN ERM$(0)="Upload not active":E%=0:GOSUB 3600:RETURN
17530 IF EOF(1) THEN CLOSE#1:ERM$(0)="Upload complete, file closed" ELSE 17550
17540 E%=0:GOSUB 3600:IU=FALSE:ULON=FALSE:ULN$=" ":GOSUB 33010:UP$="":RETURN
17550 ON ERROR GOTO 17620:IF UL$="" THEN LINE INPUT#1,UL$:ON ERROR GOTO 0
17560 IF ILE THEN PRINT UL$
17570 ON ERROR GOTO 3440:IF IPRR THEN LPRINT UL$
17580 ON ERROR GOTO 0
17590 CALL SN(C%,UL$,E%):IF E%>-1 THEN GOSUB 3600
17600 CALL SN(C%,TSEND$,E%):IF E%>-1 THEN GOSUB 3600
17610 UL$="":RETURN
17620 CLOSE#1:UP$="":IU=FALSE:ULON=FALSE:ULN$=" ":GOSUB 33010:E%=0
17630 ERM$(0)="Disk Error, BASIC Err= "+STR$(ERR):GOSUB 3600:RESUME 17640
17640 ON ERROR GOTO 0:RETURN
17650 'Print files
17660 PRINT"If you wish a list of files,":PRINT"enter the drive designator(s),"
17670 PRINT "NO colons, or separators":PRINT "(ENTER alone to bypass)"
17680 INPUT "",DRV$:LDRV=LEN(DRV$):IF LDRV>2 THEN GOSUB 20400:GOTO 17660
17690 IF LDRV=0 GOTO 17740
17700 IF LDRV=1 THEN DR1$=DRV$ ELSE DR1$=LEFT$(DRV$,1):DR2$=RIGHT$(DRV$,1)
17710 ON ERROR GOTO 17750:FL1CK$=DR1$+":*.*":FL2CK$=DR2$+":*.*"
17720 CLS:PRINT "Drive ";DR1$:FILES FL1CK$:PRINT :PRINT
17730 IF LDRV=2 THEN PRINT "Drive ";DR2$:FILES FL2CK$:PRINT:PRINT
17740 ON ERROR GOTO 0:RETURN
17750 IF (ERL=17720)AND(ERR=53) THEN BEEP ELSE 17770
17760 CLS:PRINT"No files found":RESUME 17660
17770 IF (ERL=17720)AND(ERR=71) THEN BEEP ELSE 17790
17780 PRINT"Drive "+DR1$+" not ready":PRINT:RESUME 17660
17790 IF ERL=17720 THEN BEEP:PRINT "BASIC Error "+STR$(ERR):PRINT:RESUME 17730
17800 IF ERR=53 THEN BEEP ELSE 17820
17810 PRINT"No files found":PRINT:RESUME 17660
17820 IF ERR=71 THEN BEEP:PRINT"Drive "+DR2$+" not ready":RESUME 17660
17830 BEEP:PRINT "BASIC Error "+STR$(ERR):RESUME NEXT
31000 COLOR 15:PRINT "F1 ";:COLOR 7:PRINT "- Send Break to Host"
31010 COLOR 15:PRINT "F2 ";:COLOR 7:PRINT "- Function Selection Menu"
31020 COLOR 15:PRINT "F3 ";:COLOR 7:PRINT "- Display Next Error Msg."
31030 COLOR 15:PRINT "F4 ";:COLOR 7:PRINT "- Error ON/OFF Switch"
31040 COLOR 15:PRINT "F5 ";:COLOR 7:PRINT "- Display Function Key Menu"
31050 COLOR 15:PRINT "F6 ";:COLOR 7:PRINT "- Hex Listing ON/OFF Switch"
31060 COLOR 15:PRINT "F7 ";:COLOR 7:PRINT "- Printer ON/OFF Switch"
31070 COLOR 15:PRINT "F8 ";:COLOR 7:PRINT "- Telephone/LOG-ON Menu"
31080 COLOR 15:PRINT "F9 ";:COLOR 7:PRINT "- Upload ON/OFF Switch"
31090 COLOR 15:PRINT "F10";:COLOR 7:PRINT "- Log File ON/OFF Switch"
31100 COLOR 15:PRINT "ALT H ";:COLOR 7:PRINT "- Telephone/LOG-ON Help Menu"
31110 COLOR 15:PRINT "ALT P ";:COLOR 7:PRINT "- Print Max.Rec.Buf.Used"
31120 PRINT:RETURN
31130 IF NOT SMART GOTO 31150
31140 PRINT "Insure ";:COLOR 15 :PRINT "CAPS LOCK ";:COLOR 7:PRINT"is on"
31150 PRINT "Depress ";:COLOR 15:PRINT "F2 ";:COLOR 7:PRINT "to open ";
31160 COLOR 15:PRINT "Log/Upload ";:COLOR 7:PRINT "files"
31170 PRINT "Use ";:COLOR 15:PRINT "F7 ";:COLOR 7:PRINT "if printout desired"
31180 PRINT "Depress ";:COLOR 15,0:PRINT "F8 ";:COLOR 7:PRINT "for ";
31190 COLOR 15:PRINT"Telephone/LOG-ON ";:COLOR 7:PRINT "menu":PRINT:RETURN
32000 LOCATE 24,1:FOR CLEER=0 TO 24:PRINT:NEXT CLEER:LGGR=0:TLN=9 'Max. 9
32010 X=FRE("x"):IF TLN=1 THEN TELE=1:GOTO 32160
32020 COLOR 15,0:PRINT "Enter ";:COLOR 7,0:PRINT "phone # ";:COLOR 15,0
32030 PRINT "selection ";:COLOR 7,0:PRINT "Depress ":COLOR 15
32040 PRINT "ESC";:COLOR 7:PRINT "ape to ";
32050 COLOR 15:PRINT "return ";:COLOR 7:PRINT "as a Terminal"
32060 PRINT:RESTORE 32320:FOR SELEC=1 TO TLN
32070 READ CPNY$,UL$,CTY$,TELCO$,GO,LOGIN$,IDPSW$:GOSUB 32090
32080 NEXT:PRINT:GOTO 32120
32090 COLOR 15,0:PRINT RIGHT$(STR$(SELEC),1);" ";:COLOR 7,0:GOSUB 32100:RETURN
32100 PRINT USING "\      \";CPNY$+" ";:PRINT UL$;" ";
32110 PRINT USING "\           \";CTY$+" ";TELCO$:RETURN
32120 DL$=INKEY$:TELE=VAL(DL$)
32130 IF DL$="" THEN GOSUB 33000:GOTO 32120
32140 IF DL$=CHR$(27) THEN GOSUB 32200:GOTO 3405
32150 IF (TELE<1) OR (TELE>TLN) THEN GOSUB 20400:GOTO 32120
32160 RESTORE 32320:FOR SELECT=1 TO TELE
32170 READ CPNY$,UL$,CTY$,TELCO$,GO,LOGIN$,IDPSW$:NEXT:IF NOT SMART GOTO 32270
32180 IF MPARM(17)=1 THEN UL$="ATDT"+UL$ ELSE UL$="ATDP"+UL$
32190 GOSUB 17590:GOSUB 32200:GOTO 32220
32200 LOCATE 24-(TLN+1),1,0:FOR CLEER=0 TO 24:PRINT STRING$(79," ")
32210 NEXT CLEER:LOCATE ,,1:RETURN
32220 COLOR 15,0:PRINT CPNY$;:COLOR 7,0
32230 PRINT " is being called via ";:COLOR 15,0:PRINT TELCO$:COLOR 7,0
32240 PRINT "To redial, Depress ";:COLOR 15,0:PRINT "HOME ";
32250 COLOR 7,0:PRINT "and ";:COLOR 15,0:PRINT "F8 ";
32260 COLOR 7,0:PRINT "and Redo":PRINT:GOTO 32280
32270 GOSUB 32200:PRINT"Place Call to "+CPNY$+" via "+TELCO$:PRINT"Ph. # "+UL$
32280 PRINT "Operating as "+TMSL$+" Terminal":PRINT"After CONNECT, use ";:COLOR 15
32290 PRINT"F8 ";:COLOR 7:PRINT "to ";:COLOR 15:PRINT "LOG-ON.":COLOR 7:PRINT
32300 ON ERROR GOTO 3440:IF IPRR THEN LPRINT CPNY$+" being called via ";TELCO$
32310 ON ERROR GOTO 0:INIT=FALSE:UL$="":RETURN
32320 DATA SOURCE,986-9503,Van Nuys,TYMNET,1,SOURCE11;PRIM;,ID TCA123 PASWRD
32330 DATA SOURCE,986-9803,Van Nuys,TYMNET,1,SOURCE11;PRIM;,ID TCA123 PASWRD
32340 DATA SOURCE,365-9277,Mission Hls,TYMNET,1,SOURCE11;PRIM;,ID TCA123 PASWRD
32350 DATA SOURCE,998-3331,Northridge,TYMNET,1,SOURCE13;PRIM;,ID TCA123 PASWRD -ON SYS11
32360 DATA SOURCE,992-0144,Woodland Hls,TELENET,2,C 30138,ID TCA123 PASWRD
32370 DATA SOURCE,822-9287,Canoga Park,TELENET,2,C 30138,ID TCA123 PASWRD
32380 DATA CSERVE,892-7211,Van Nuys,CSERVE,3,"77000,1100",PASS/WORD
32390 DATA CSERVE,781-8439,San Fernando,CSERVE,3,"77000,1100",PASS/WORD
32400 DATA CSERVE,365-2013,Mission Hls,TYMNET,4,"77000,1100",PASS/WORD
32410 DATA CSERVE,998-4872,Northridge,TYMNET,4,"77000,1100",PASS/WORD
32420 IF LGGR<>0 GOTO 32510 ELSE ON GO GOTO 32430,32440,32450,32460,32470,32500
32430 UUL$="A":GOSUB 32570:LGGR=1:RETURN
32440 UUL$=CHR$(13):GOSUB 32570:FOR D2LY=0 TO 500:NEXT:GOSUB 32570:GO=6:RETURN
32450 UUL$=CHR$(3):GOSUB 32570:LGGR=1:RETURN
32460 UUL$="A":GOSUB 32570:GO=GO+1:RETURN
32470 PRINT "Type CIS02 and ENTER for non-prime time"
32480 PRINT "Type CPS01 and ENTER for prime time use":PRINT
32490 PRINT "Use F8 key for rest of LOG-ON":LGGR=1:RETURN
32500 UL$="D1":GOSUB 17590:LGGR=1:RETURN
32510 ON LGGR GOTO 32520,32530,32540,32550
32520 UL$=LOGIN$:GOSUB 17590:LGGR=LGGR+1:RETURN
32530 UL$=IDPSW$:GOSUB 17590:LGGR=LGGR+1:RETURN
32540 E%=0:ERM$(0)="ERROR * Use ALT H for F8 Help Menu":GOSUB 3600:RETURN
32550 PRINT "DISCONNECTING":UUL$="+++":GOSUB 32570:FOR D2LY=0 TO 3000:NEXT
32560 UL$="ATH":GOSUB 17590:LGGR=0:INIT=TRUE:RETURN
32570 CALL SN(C%,UUL$,E%):IF E%>-1 THEN GOSUB 3600 ELSE RETURN
32580 PRINT :PRINT :COLOR 15:PRINT"  Telephone/LOG-ON Help Menu":COLOR 7:PRINT
32590 COLOR 15:PRINT "HOME ";:COLOR 7:PRINT "- Enables F8 from the beginning"
32600 PRINT "       telephone dialup menu.":PRINT
32610 COLOR 15:PRINT "F8   ";:COLOR 7:PRINT "- After dialup, Depress F8 "
32620 PRINT "       in response to LOG-ON requests.":PRINT
32630 COLOR 15:PRINT CHR$(27)+"--  ";:COLOR 7:PRINT "- Cursor left  (Numeric 4)
32640 PRINT "       Return to previous entry,"
32650 PRINT "       using Function Key F8.":PRINT
32660 COLOR 15:PRINT "END  ";:COLOR 7:PRINT "- Enables last entry using F8"
32670 PRINT "       (Hang up the phone)":PRINT :PRINT :RETURN
33000 IF VAL(MID$(TIME$,4,2))=TME THEN RETURN
33010 IF MPARM(5)<>2 THEN RETURN
33020 ITEM=POS(X):ICSR=CSRLIN:CLMN=IWT-(LEN(TIME$)+LEN(DATE$)+17)
33030 TMME$=LEFT$(TIME$,5):TME=VAL(RIGHT$(TMME$,2))
33040 HOUR=VAL(LEFT$(TMME$,2)):IF HOUR=0 THEN HOUR=12:APM$="AM ":GOTO 33070
33050 IF HOUR>12 THEN HOUR=HOUR-12:APM$="PM ":GOTO 33070
33060 IF HOUR=12 THEN APM$="PM " ELSE APM$="AM "
33070 HR$=STR$(HOUR):TMME$=HR$+RIGHT$(TMME$,3)+APM$
33080 LOCATE 25,CLMN,0:COLOR 15,0:PRINT USING "\\";HXL$;:PRINT USING "\\";PTR$;
33090 COLOR UNTSY:PRINT USING "\\";ULN$;:COLOR DNTSY:PRINT USING "\\";DLN$;
33100 COLOR 7,0:PRINT "F5=HELP ";:IF NOT NTME THEN PRINT TMME$;
33110 IF LEFT$(DATE$,2)<>"00" THEN PRINT DATE$;
33120 LOCATE ICSR,ITEM,1:RETURN
34000 GOSUB 34050:GOSUB 34040:CLS:NEW
34010 GOSUB 34050:PRINT "Insert DOS diskette in default drive"
34020 PRINT "Depress any key when ready"
34030 K$=INKEY$:IF K$="" THEN 34030 ELSE GOSUB 34040:SYSTEM
34040 CLOSE:OPEN "COM1:" AS 1:RETURN
34050 CLS:PRINT "TERMINATING COMM. PROGRAM"
34060 PRINT "ARE YOU SURE(Y/N)?"
34070 K$=INKEY$:IF K$="" THEN 34070
34080 IF K$="Y" OR K$="y" THEN RETURN
34090 IF K$="N" OR K$="n" THEN 2800
34100 GOSUB 20400:GOTO 34070
35000 IQ=MPARM(16):IF IQ=0 THEN RETURN
35010 ON IQ GOTO 35020,35040
35020 WIDTH 40:LOCATE ,,0:CLS:DEF SEG=0:A=PEEK(&H410):POKE &H410, A OR &H30
35030 WIDTH 80:IWT=80:LOCATE 1,1,0,12,13:RETURN
35040 LOCATE ,,0:CLS:DEF SEG=0:A=PEEK(&H410):POKE &H410,(A AND &HCF) OR &H20
35050 SCREEN 1:SCREEN 0:WIDTH VDO:IWT=VDO:LOCATE ,,0,6,7:RETURN
```

{% comment %}samples_end{% endcomment %}

### Directory of PC-SIG Library Disk 0054

     Volume in drive A has no label
     Directory of A:\

    CRC      TXT       983  11-09-84  10:55a
    CRCK4    COM      1536  10-21-82   7:54p
    DESCRIPT ION     27426   5-16-82
    LONGTERM BAS     17611   7-27-84  10:08a
    PROFEEL           2499   5-16-82
    PROGRAMN OTE     27934   5-16-82
    SHORTERM BAS     16342   7-27-84  10:05a
    TUTORIAL         15293   5-16-82
    XMODEM   ASM     52521   4-02-83   7:36a
    XMODEM   COM      9728   3-29-83   9:16p
    XMODEM   DOC      7621   3-29-83   6:35p
           11 file(s)     179494 bytes
                          138240 bytes free