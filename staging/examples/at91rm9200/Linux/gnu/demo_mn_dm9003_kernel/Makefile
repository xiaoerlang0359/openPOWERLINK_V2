
INSTALLDIR  = /tftpboot/

MODULENAME = epl



# ------------------------- Secondary Call ----------------------------------
ifneq ($(KERNELRELEASE),)

MAINPATH	:= ../../../../..
MAINDIR	:= $(src)/$(MAINPATH)
INCLUDES	:= -I$(MAINDIR)/Include \
			  -I$(src) \
			  -I$(MAINDIR)/Target/PLCcore-CF54/Linux/gnu/generic \
			  -I$(MAINDIR)/SharedBuff \
			  -I$(MAINDIR)/EplStack \			  
			  -I$(MAINDIR)/ObjDicts/Api_CN

MODULEOBJS	= demo_main.o \
			  $(MAINPATH)/Edrv/Edrv9003.o $(MAINPATH)/Edrv/EdrvCyclic.o \
			  $(MAINPATH)/EplStack/EplDllk.o $(MAINPATH)/EplStack/kernel/dll/dllkcal.o \
			  $(MAINPATH)/EplStack/user/dll/dllucal.o \
			  $(MAINPATH)/EplStack/common/dll/dllcal-shb.o \
			  $(MAINPATH)/EplStack/EplLedu.o \
			  $(MAINPATH)/EplStack/kernel/event/eventk.o $(MAINPATH)/EplStack/user/event/eventu.o \
			  ${MAINPATH}/EplStack/kernel/event/eventkcal.c ${MAINPATH}/EplStack/user/event/eventucal.c \
			  ${MAINPATH}/EplStack/common/event/eventcal-shb.c \
			  ${MAINPATH}/EplStack/user/event/eventucal-shb.c \
			  ${MAINPATH}/EplStack/kernel/event/eventkcal-shb.c \
			  ${MAINPATH}/EplStack/common/event/event.c \
			  $(MAINPATH)/EplStack/EplNmtk.o $(MAINPATH)/EplStack/EplNmtkCal.o \
			  $(MAINPATH)/EplStack/EplNmtu.o $(MAINPATH)/EplStack/EplNmtuCal.o $(MAINPATH)/EplStack/EplNmtCnu.o \
			  $(MAINPATH)/EplStack/EplNmtMnu.o $(MAINPATH)/EplStack/EplIdentu.o $(MAINPATH)/EplStack/EplStatusu.o \
			  $(MAINPATH)/EplStack/kernel/pdo/pdok.o $(MAINPATH)/EplStack/kernel/pdo/pdokcal.o \
			  $(MAINPATH)/EplStack/user/pdo/pdou.o $(MAINPATH)/EplStack/user/pdo/pdoucal.o \
			  $(MAINPATH)/EplStack/EplObd.o \
			  $(MAINPATH)/EplStack/EplSdoUdpu.o $(MAINPATH)/EplStack/EplSdoComu.o $(MAINPATH)/EplStack/EplSdoAsySequ.o $(MAINPATH)/EplStack/EplSdoAsndu.o \
			  $(MAINPATH)/EplStack/EplTimeruLinuxKernel.o \
			  $(MAINPATH)/EplStack/kernel/errhnd/errhndk.o \
			  $(MAINPATH)/EplStack/user/errhnd/errhndu.o \
			  $(MAINPATH)/EplStack/kernel/errhnd/errhndkcal-local.o \
			  $(MAINPATH)/EplStack/user/errhnd/errhnducal-local.o \			  
			  $(MAINPATH)/EplStack/EplApiGeneric.o \
			  $(MAINPATH)/ObjDicts/Api_CN/Objdict.o \
			  $(MAINPATH)/EplStack/amiarm.o \
			  $(MAINPATH)/EplStack/VirtualEthernetLinux.o \
			  $(MAINPATH)/SharedBuff/SharedBuff.o $(MAINPATH)/SharedBuff/ShbIpc-LinuxKernel.o \
			  $(MAINPATH)/EplStack/SocketLinuxKernel.o \
			  $(MAINPATH)/Target/PLCcore-CF54/Linux/gnu/generic/proc_fs.o \
			  $(MAINPATH)/Target/at91/Linux/gnu/generic/TimerHighReskAT91.o

#           Select here between debug and release settings
#DBG_MODE = NDEBUG
DBG_MODE = _DEBUG

#MODFLAGS =	-D$(DBG_MODE)
#MODFLAGS =	-D$(DBG_MODE) -D_DBG_TRACE_POINTS_ -DDEF_DEBUG_LVL=0xEC000040L
MODFLAGS =	-D$(DBG_MODE) -D_DBG_TRACE_POINTS_ -DDEF_DEBUG_LVL=0xEC000000L

EXTRA_CFLAGS = $(INCLUDES) $(MODFLAGS)
#EXTRA_CFLAGS = -Wa,-alhs $(INCLUDES) $(MODFLAGS)

obj-m := $(MODULENAME).o

$(MODULENAME)-y := $(MODULEOBJS)


# add the object files of the stack to the variable clean-files,
# because the object files in upper directories were not deleted otherwise.
clean-files := $(MODULEOBJS) \
		$(foreach f,$(MODULEOBJS),$(dir $(f)).$(notdir $(f)).cmd)


# ------------------------- Primary Call ------------------------------------
else

.EXPORT_ALL_VARIABLES:
KDIR			:= $(ELINOS_PROJECT)/linux

MAINPATH	= ../../../../..

.PHONY:     call_driver_build
call_driver_build:
			$(MAKE)	-C $(KDIR)	SUBDIRS=$(PWD) modules

.PHONY:     install
install:    call_driver_build
#			cp $(MODULENAME).ko $(INSTALLDIR)
			${ELINOS_BIN_PREFIX}-strip --strip-unneeded -o $(INSTALLDIR)/$(MODULENAME).ko $(MODULENAME).ko

.PHONY:     clean
clean:
			$(MAKE)	-C $(KDIR)	SUBDIRS=$(PWD) clean

endif



