###############################################################################
#
# Installation DIRECTORIES
#
# Change these if you want to install somewhere else.

INSTALL_PLUGINS_DIR	=	output/lib/
INSTALL_INCLUDE_DIR	=	output/include/
INSTALL_BINARY_DIR	=	output/bin/

###############################################################################
#
# GENERAL
#

INCLUDES	=	-I.
LIBRARIES	=	-ldl -lm
CFLAGS		=	$(INCLUDES) -Wall  -O3
LOCAL_LDFLAGS   =      -L./output/lib/ -lRK_AudioProcess 
CXXFLAGS	=	$(CFLAGS)
PLUGINS		=	../plugins/Equalizer.so
CC		=	../../../buildroot/output/rockchip_rk3308_release/host/usr/bin/aarch64-rockchip-linux-gnu-gcc
CPP		=	../../../buildroot/output/rockchip_rk3308_release/host/usr/bin/aarch64-rockchip-linux-gnu-g++
LD		=	../../../buildroot/output/rockchip_rk3308_release/host/usr/bin/aarch64-rockchip-linux-gnu-ld

###############################################################################
#
# RULES TO BUILD PLUGINS FROM C OR C++ CODE
#

../plugins/%.so:	plugins/%.c ladspa.h
	$(CC) $(CFLAGS) -o plugins/$*.o -c -fPIC plugins/$*.c
	$(LD) -o ../plugins/$*.so plugins/$*.o -shared $(LOCAL_LDFLAGS)

../plugins/%.so:	plugins/%.cpp ladspa.h
	$(CPP) $(CXXFLAGS) -o plugins/$*.o -c plugins/$*.cpp
	$(CPP) -o ../plugins/$*.so plugins/$*.o -shared

###############################################################################
#
# TARGETS
#

install:	targets

targets:	$(PLUGINS) 


###############################################################################
#
# UTILITIES
#

always:	

clean:
	-rm -f `find . -name "*.o"` ../bin/* ../plugins/*
	-rm -f `find .. -name "*~"`
	-rm -f *.bak core score.srt
	-rm -f *.bb *.bbg *.da *-ann gmon.out bb.out
	-rm -f `find .. -name "*.class"`

backup:		clean
	(cd ../../;							\
	tar czf `date '+../backup/ladspa_sdk.%Y%m%d%H%M.tgz'` ladspa_sdk/)

###############################################################################
