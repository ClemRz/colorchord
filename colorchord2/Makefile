all : colorchord

RAWDRAW:=DrawFunctions.o XDriver.o
SOUND:=sound.o sound_alsa.o sound_pulse.o sound_null.o

OUTS := OutputVoronoi.o DisplayArray.o OutputLinear.o DisplayPie.o DisplayNetwork.o DisplayUSB2812.o DisplayDMX.o OutputProminent.o RecorderPlugin.o OutputCells.o

WINGCC:= i686-w64-mingw32-gcc
WINGCCFLAGS:= -g -DICACHE_FLASH_ATTR= -I../embeddedcommon -I. -O0   #-O2 -Wl,--relax -Wl,--gc-sections -ffunction-sections -fdata-sections
WINLDFLAGS:=-lwinmm -lgdi32 -lws2_32 

RAWDRAWLIBS:=-lX11 -lm -lpthread -lXinerama -lXext
LDLIBS:=-lpthread -lasound -lm -lpulse-simple -lpulse


CFLAGS:=-g -O0 -flto -Wall -ffast-math -I../embeddedcommon -I. -DICACHE_FLASH_ATTR=
EXTRALIBS:=-lusb-1.0

colorchord : os_generic.o main.o  dft.o decompose.o filter.o color.o sort.o notefinder.o util.o outdrivers.o $(RAWDRAW) $(SOUND) $(OUTS) parameters.o chash.o hook.o ../embeddedcommon/DFT32.o
	gcc -o $@ $^ $(CFLAGS) $(LDLIBS) $(EXTRALIBS) $(RAWDRAWLIBS)

colorchord.exe : os_generic.c main.c  dft.c decompose.c filter.c color.c sort.c notefinder.c util.c outdrivers.c DrawFunctions.c parameters.c chash.c WinDriver.c sound.c sound_null.c sound_win.c OutputVoronoi.c DisplayArray.c OutputLinear.c DisplayPie.c DisplayNetwork.c hook.c RecorderPlugin.c ../embeddedcommon/DFT32.c OutputCells.c
	$(WINGCC) $(WINGCCFLAGS) -o $@ $^ $(WINLDFLAGS)


clean :
	rm -rf *.o *~ colorchord colorchord.exe embeddedcc
