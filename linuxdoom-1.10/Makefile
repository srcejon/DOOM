################################################################
#
# $Id:$
#
# $Log:$
#
CC=  gcc # Use -m32 for 32-bit compile

CFLAGS=-g -Wall -O2 -DNORMALUNIX -DLINUX -DSNDSERV # -DUSEASM 
LDFLAGS=-L/usr/X11R6/lib
LIBS=-lXext -lX11 -lnsl -lm

# subdirectory for objects
O=linux

# not too sophisticated dependency
OBJS=				\
		$(O)/doomdef.o		\
		$(O)/doomstat.o		\
		$(O)/dstrings.o		\
		$(O)/i_system.o		\
		$(O)/i_sound.o		\
		$(O)/i_video.o		\
		$(O)/i_net.o			\
		$(O)/tables.o			\
		$(O)/f_finale.o		\
		$(O)/f_wipe.o 		\
		$(O)/d_main.o			\
		$(O)/d_net.o			\
		$(O)/d_items.o		\
		$(O)/g_game.o			\
		$(O)/m_menu.o			\
		$(O)/m_misc.o			\
		$(O)/m_argv.o  		\
		$(O)/m_bbox.o			\
		$(O)/m_fixed.o		\
		$(O)/m_swap.o			\
		$(O)/m_cheat.o		\
		$(O)/m_random.o		\
		$(O)/am_map.o			\
		$(O)/p_ceilng.o		\
		$(O)/p_doors.o		\
		$(O)/p_enemy.o		\
		$(O)/p_floor.o		\
		$(O)/p_inter.o		\
		$(O)/p_lights.o		\
		$(O)/p_map.o			\
		$(O)/p_maputl.o		\
		$(O)/p_plats.o		\
		$(O)/p_pspr.o			\
		$(O)/p_setup.o		\
		$(O)/p_sight.o		\
		$(O)/p_spec.o			\
		$(O)/p_switch.o		\
		$(O)/p_mobj.o			\
		$(O)/p_telept.o		\
		$(O)/p_tick.o			\
		$(O)/p_saveg.o		\
		$(O)/p_user.o			\
		$(O)/r_bsp.o			\
		$(O)/r_data.o			\
		$(O)/r_draw.o			\
		$(O)/r_main.o			\
		$(O)/r_plane.o		\
		$(O)/r_segs.o			\
		$(O)/r_sky.o			\
		$(O)/r_things.o		\
		$(O)/w_wad.o			\
		$(O)/wi_stuff.o		\
		$(O)/v_video.o		\
		$(O)/st_lib.o			\
		$(O)/st_stuff.o		\
		$(O)/hu_stuff.o		\
		$(O)/hu_lib.o			\
		$(O)/s_sound.o		\
		$(O)/z_zone.o			\
		$(O)/info.o				\
		$(O)/sounds.o

all:	$(O) $(O)/doom1.wad  $(O)/linuxxdoom $(O)/sndserver

$(O):
	mkdir $(O)

$(O)/doom1.wad: ../wad/doom1.wad
	cp $< $@

$(O)/sndserver: ../sndserv/linux/sndserver
	cp $< $@

../sndserv/linux/sndserver:
	(cd ../sndserv ; mkdir -p linux ; make)

clean:
	rm -f *.o *~ *.flc
	rm -f linux/*

$(O)/linuxxdoom:	$(OBJS) $(O)/i_main.o
	$(CC) $(CFLAGS) $(LDFLAGS) $(OBJS) $(O)/i_main.o \
	-o $(O)/linuxxdoom $(LIBS)

$(O)/%.o:	%.c
	$(CC) $(CFLAGS) -c $< -o $@

# For sound you need /dev/dsp - For this, run: sudo apt-get install osspd
# See: https://bugs.launchpad.net/ubuntu/+source/osspd/+bug/1857810

# Update path, so it can find sndserver
export PATH := .:$(PATH)
	
# Run doom - use an X server to provide 8-bit colour depth
run:
	Xephyr :2 -ac -br -screen 320x200x8 -reset -terminate -title DOOM &
	sleep 1
	(cd $(O) ; DISPLAY=:2 pasuspender ./linuxxdoom )

debug:
	Xephyr :2 -ac -br -screen 320x200x8 -reset -terminate -title DOOM &
	sleep 1
	(cd $(O) ; DISPLAY=:2 gdb ./linuxxdoom )

#############################################################
#
#############################################################
