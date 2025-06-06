#*************************************************************************
# Copyright (c) 2002 The University of Chicago, as Operator of Argonne
#     National Laboratory.
# Copyright (c) 2002 The Regents of the University of California, as
#     Operator of Los Alamos National Laboratory.
# EPICS BASE Versions 3.13.7
# and higher are distributed subject to a Software License Agreement found
# in file LICENSE that is included with this distribution. 
#*************************************************************************
TOP = ..
include $(TOP)/configure/CONFIG

ASYN = $(TOP)/asyn
#USR_CFLAGS += -DDEBUG
USR_CFLAGS += -DUSE_TYPED_RSET -DUSE_TYPED_DSET -DUSE_TYPED_DRVET
USR_CPPFLAGS += -DUSE_TYPED_RSET -DUSE_TYPED_DSET -DUSE_TYPED_DRVET

USR_INCLUDES_cygwin32 += -I/usr/include/tirpc

# The following gets rid of the -fno-implicit-templates flag on vxWorks, 
# so we get automatic template instantiation.
# This is what we want for miscellaneous/asynPortDriver.cpp
ifeq (vxWorks,$(findstring vxWorks, $(T_A)))
  CODE_CXXFLAGS=
endif
USR_CXXFLAGS_solaris-sparc=-instances=global

LIBRARY_IOC += asyn

asyn_SYS_LIBS_WIN32 = ws2_32 winmm
asyn_SYS_LIBS_cygwin32 = $(CYGWIN_RPC_LIB)

# Some linux systems moved RPC related symbols to libtirpc
# Define TIRPC in configure/CONFIG_SITE in this case
ifeq ($(TIRPC),YES)
  USR_INCLUDES_Linux += -I/usr/include/tirpc
  asyn_SYS_LIBS_Linux += tirpc
endif

SRC_DIRS += $(ASYN)/asynDriver
INC += asynAPI.h
INC += asynDriver.h
INC += epicsInterruptibleSyscall.h
asyn_SRCS += asynManager.c
asyn_SRCS += epicsInterruptibleSyscall.c

SRC_DIRS += $(ASYN)/asynGpib
INC += asynGpibDriver.h
asyn_SRCS += asynGpib.c

SRC_DIRS += $(ASYN)/drvAsynSerial
INC += drvAsynSerialPort.h
ifeq ($(OS_CLASS), WIN32)
  asyn_SRCS += drvAsynSerialPortWin32.c
else
  asyn_SRCS += drvAsynSerialPort.c
endif
DBD += drvAsynSerialPort.dbd
INC += drvAsynIPPort.h
asyn_SRCS += drvAsynIPPort.c
asyn_SRCS += drvAsynIPServerPort.c
DBD += drvAsynIPPort.dbd
INC += drvAsynIPServerPort.h

SRC_DIRS += $(ASYN)/interfaces
INC += asynInt32.h          asynInt32SyncIO.h
INC += asynInt64.h          asynInt64SyncIO.h
INC += asynUInt32Digital.h  asynUInt32DigitalSyncIO.h
INC += asynFloat64.h        asynFloat64SyncIO.h
INC += asynInt8Array.h      asynInt8ArraySyncIO.h
INC += asynInt16Array.h     asynInt16ArraySyncIO.h
INC += asynInt32Array.h     asynInt32ArraySyncIO.h
INC += asynInt64Array.h     asynInt64ArraySyncIO.h
INC += asynFloat32Array.h   asynFloat32ArraySyncIO.h
INC += asynFloat64Array.h   asynFloat64ArraySyncIO.h
INC += asynOctet.h          asynOctetSyncIO.h
INC += asynGenericPointer.h asynGenericPointerSyncIO.h
INC += asynEnum.h           asynEnumSyncIO.h
INC += asynCommonSyncIO.h
INC += asynOption.h         asynOptionSyncIO.h
INC += asynDrvUser.h
INC += asynStandardInterfaces.h
asyn_SRCS += asynInt32Base.c         asynInt32SyncIO.c
asyn_SRCS += asynInt64Base.c         asynInt64SyncIO.c
asyn_SRCS += asynInt8ArrayBase.c     asynInt8ArraySyncIO.c
asyn_SRCS += asynInt16ArrayBase.c    asynInt16ArraySyncIO.c
asyn_SRCS += asynInt32ArrayBase.c    asynInt32ArraySyncIO.c
asyn_SRCS += asynInt64ArrayBase.c    asynInt64ArraySyncIO.c
asyn_SRCS += asynUInt32DigitalBase.c asynUInt32DigitalSyncIO.c
asyn_SRCS += asynFloat64Base.c       asynFloat64SyncIO.c
asyn_SRCS += asynFloat32ArrayBase.c  asynFloat32ArraySyncIO.c
asyn_SRCS += asynFloat64ArrayBase.c  asynFloat64ArraySyncIO.c
asyn_SRCS += asynOctetBase.c         asynOctetSyncIO.c
asyn_SRCS += asynGenericPointerBase.c  asynGenericPointerSyncIO.c
asyn_SRCS += asynEnumBase.c          asynEnumSyncIO.c
asyn_SRCS += asynCommonSyncIO.c
asyn_SRCS += asynOptionSyncIO.c
asyn_SRCS += asynStandardInterfacesBase.c

SRC_DIRS += $(ASYN)/miscellaneous
DBD += asyn.dbd
INC += asynShellCommands.h
INC += asynInterposeCom.h
INC += asynInterposeEos.h
INC += asynInterposeFlush.h
ifneq ($(EPICS_LIBCOM_ONLY),YES)
  asyn_SRCS += asynShellCommands.c
endif
asyn_SRCS += asynInterposeCom.c
asyn_SRCS += asynInterposeEos.c
asyn_SRCS += asynInterposeFlush.c
asyn_SRCS += asynInterposeDelay.c
asyn_SRCS += asynInterposeEcho.c

SRC_DIRS += $(ASYN)/asynPortDriver/exceptions
INC += ParamListInvalidIndex.h
INC += ParamListParamNotFound.h
INC += ParamValNotDefined.h
INC += ParamValStringSizeRequestTooBig.h
INC += ParamValWrongType.h
INC += ParamValValueNotChanged.h
asyn_SRCS += ParamListInvalidIndex.cpp
asyn_SRCS += ParamListParamNotFound.cpp
asyn_SRCS += ParamValNotDefined.cpp
asyn_SRCS += ParamValStringSizeRequestTooBig.cpp
asyn_SRCS += ParamValWrongType.cpp
asyn_SRCS += ParamValValueNotChanged.cpp

SRC_DIRS += $(ASYN)/asynPortDriver
ifeq ($(EPICS_LIBCOM_ONLY),YES)
   USR_CXXFLAGS += -DEPICS_LIBCOM_ONLY
   USR_CFLAGS   += -DEPICS_LIBCOM_ONLY
endif
INC += asynParamType.h
INC += paramErrors.h
INC += asynParamSet.h
INC += asynPortDriver.h
asyn_SRCS += paramVal.cpp
asyn_SRCS += asynPortDriver.cpp

SRC_DIRS += $(ASYN)/asynPortClient
INC += asynPortClient.h
asyn_SRCS += asynPortClient.cpp

ifneq ($(EPICS_LIBCOM_ONLY),YES)
  ifdef CAT 
    DBDCAT += devEpics.dbd
  else
    INSTALL_DBDS += $(INSTALL_DBD)/devEpics.dbd
  endif
  SRC_DIRS += $(ASYN)/devEpics
  devEpics_DBD += devAsynOctet.dbd
  devEpics_DBD += devAsynInt32.dbd
  devEpics_DBD += devAsynXXXArray.dbd
  devEpics_DBD += devAsynInt32TimeSeries.dbd
  devEpics_DBD += devAsynUInt32Digital.dbd
  devEpics_DBD += devAsynFloat64.dbd
  devEpics_DBD += devAsynFloat64TimeSeries.dbd
  devEpics_DBD += devAsynRecord.dbd
  DB  += asynInt32TimeSeries.db
  DB  += asynFloat64TimeSeries.db
  INC += asynEpicsUtils.h
  asyn_SRCS += devAsynOctet.c
  asyn_SRCS += asynEpicsUtils.c
  asyn_SRCS += devAsynInt32.c
  asyn_SRCS += devAsynInt32TimeSeries.c
  asyn_SRCS += devAsynUInt32Digital.c
  asyn_SRCS += devAsynFloat64.c
  asyn_SRCS += devAsynXXXArray.cpp
  asyn_SRCS += devAsynFloat64TimeSeries.c
  asyn_SRCS += devEpicsPvt.c

  # These require 64-bit support
  ifdef BASE_7_0
    HAVE_DEVINT64=YES
  endif
  ifdef BASE_3_16
    ifneq ($(EPICS_MODIFICATION),0)
      HAVE_DEVINT64=YES
    endif
  endif

  # 3.15 and above support lsi, lso and printf records
  ifdef BASE_3_15
    USR_CFLAGS += -DHAVE_LSREC
    devEpics_DBD += devAsynOctetLs.dbd
  endif

  # do we have EPICS calc module (scalcout etc.)
  # applications should include asynCalc.dbd as well as asyn.dbd if support is needed
  ifdef CALC
    USR_CFLAGS += -DHAVE_CALCMOD
    ASYN_LIBS += calc
    DBD += asynCalc.dbd
  endif

  ifdef HAVE_DEVINT64
    USR_CFLAGS += -DHAVE_DEVINT64
    USR_CXXFLAGS += -DHAVE_DEVINT64
    devEpics_DBD += devAsynInt64.dbd
    devEpics_DBD += devAsynInt64Array.dbd
    devEpics_DBD += devAsynInt64TimeSeries.dbd
    asyn_SRCS += devAsynInt64TimeSeries.c
  endif
  devEpics_DBD += devAsynInt64Misc.dbd
  asyn_SRCS += devAsynInt64.c

  DBD += $(devEpics_DBD)

  SRC_DIRS += $(ASYN)/asynRecord
  DBDINC += asynRecord
  DBD += devAsynRecord.dbd
  asyn_SRCS += asynRecord.c
  asyn_SRCS += drvAsyn.c
  DB += asynRecord.db
endif

ifeq ($(DRV_VXI11),YES)
SRC_DIRS += $(ASYN)/vxi11
ifeq ($(OS_CLASS), WIN32)
  asyn_SRCS += drvVxi11Win32.c
else
  asyn_SRCS += vxi11core_xdr.c
  asyn_SRCS += drvVxi11.c
endif
asyn_SRCS += E5810Reboot.c
asyn_SRCS += E2050Reboot.c
asyn_SRCS += TDS3000Reboot.c
DBD += drvVxi11.dbd
endif

SRC_DIRS += $(ASYN)/drvPrologixGPIB
asyn_SRCS += drvPrologixGPIB.c
DBD += drvPrologixGPIB.dbd

ifdef IPAC
  SRC_DIRS += $(ASYN)/gsIP488
  asyn_SRCS_vxWorks += drvGsIP488.c
  asyn_SRCS_RTEMS += drvGsIP488.c
  DBD += drvGsIP488.dbd
  asyn_LIBS_vxWorks += Ipac
  asyn_LIBS_RTEMS += Ipac
endif

ifneq (, $(findstring RTEMS, $(T_A)))
  DRV_USBTMC = NO
  DRV_VXI11 = NO
endif
ifneq (, $(findstring vxWorks, $(T_A)))
  DRV_USBTMC = NO
  DRV_VXI11 = NO
endif
ifeq ($(DRV_USBTMC),YES)
  SRC_DIRS += $(ASYN)/drvAsynUSBTMC
  asyn_SRCS += drvAsynUSBTMC.c
  asyn_SYS_LIBS += usb-1.0
  DBD += drvAsynUSBTMC.dbd
endif

ifeq ($(DRV_FTDI),YES)
  SRC_DIRS += $(ASYN)/drvAsynFTDI
  asyn_SRCS += ftdiDriver.cpp drvAsynFTDIPort.cpp
  asyn_SYS_LIBS += usb-1.0
  INC += drvAsynFTDIPort.h
  ifeq ($(DRV_FTDI_USE_LIBFTDI1),YES)
    USR_CXXFLAGS += -DHAVE_LIBFTDI1
    ifeq ($(FTDI_LIB),)
      asyn_SYS_LIBS += ftdi1
    else
      asyn_LIBS += ftdi1
      ftdi1_DIR = $(FTDI_LIB)
    endif
  else
    ifeq ($(FTDI_LIB),)
      asyn_SYS_LIBS += ftdi
    else
      asyn_LIBS += ftdi
      ftdi_DIR = $(FTDI_LIB)
    endif
  endif

  ifdef FTDI_INCLUDE
    USR_INCLUDES += $(addprefix -I, $(FTDI_INCLUDE))
  endif

  DBD += drvAsynFTDIPort.dbd
endif

SRC_DIRS += $(ASYN)/ni1014
asyn_SRCS_vxWorks += drvNi1014.c
asyn_SRCS_RTEMS += drvNi1014.c
DBD += drvNi1014.dbd

ifeq ($(LINUX_GPIB),YES)
  SRC_DIRS += $(ASYN)/linuxGpib
  asyn_SRCS_Linux += drvLinuxGpib.c
  DBD += drvLinuxGpib.dbd
  asyn_SYS_LIBS += gpib
endif

SRC_DIRS += $(ASYN)/devGpib
INC += devGpib.h
INC += devSupportGpib.h
INC += devCommonGpib.h
DBD += devGpib.dbd
ifneq ($(EPICS_LIBCOM_ONLY),YES)
  asyn_SRCS += devCommonGpib.c
  asyn_SRCS += devSupportGpib.c
endif
asyn_SRCS += boSRQonOff.c

ifeq ($(EPICS_LIBCOM_ONLY),YES)
  asyn_LIBS += Com
else
  asyn_LIBS += $(EPICS_BASE_IOC_LIBS)
endif

include $(TOP)/configure/RULES

# For 3.14
drvVxi11$(OBJ): vxi11intr.h
# For 3.15
drvVxi11$(DEP): vxi11intr.h vxi11core.h
vxi11core_xdr.c$(DEP): vxi11core.h

ifdef T_A
 ifneq ($(findstring $(OS_CLASS),vxWorks RTEMS),)

vxi11core.h vxi11core_xdr.c vxi11intr.h vxi11intr_xdr.c : \
% : ../vxi11/rpc/%
	cp $< $@
vxi11core_xdr.o: vxi11core.h
vxi11intr_xrd.o: vxi11intr.h

 else

.SECONDARY: vxi11core_xdr.c vxi11intr_xdr.c

RPCGEN_FLAGS_darwin = -C
RPCGEN_FLAGS_solaris = -M
%.h %_xdr.c: ../vxi11/%.rpcl
	cp $< .
	rpcgen $(RPCGEN_FLAGS_$(OS_CLASS)) $*.rpcl

 endif  # OS_CLASS = vxWorks, RTEMS

# Parallel build sometimes fails.
# Make dependences on new records explicit.
asynRecord$(OBJ): $(COMMON_DIR)/asynRecord.h

devEpics.dbd$(DEP): $(TOP)/asyn/Makefile
	@$(RM) $@
	@echo "$(COMMON_DIR)/devEpics.dbd:" > $@

$(COMMON_DIR)/devEpics.dbd: $(TOP)/asyn/Makefile

 ifdef DBDCAT_COMMAND
  # Override the default command when generating devEpics.dbd
  $(COMMON_DIR)/devEpics.dbd: DBDCAT_COMMAND = \
      $(PERL) $(TOOLS)/makeIncludeDbd.pl $(devEpics_DBD) $(notdir $@)
 else
  # 3.14 didn't have the DBDCAT rule:
  build: $(COMMON_DIR)/devEpics.dbd
  $(COMMON_DIR)/devEpics.dbd: $(devEpics_DBD)
	$(ECHO) "Creating dbd file $(notdir $@)"
	@$(RM) $(notdir $@)
	$(PERL) $(TOOLS)/makeIncludeDbd.pl $(devEpics_DBD) $(notdir $@)
	@$(MV) $(notdir $@) $@
 endif  # DBDCAT_COMMAND
endif  # T_A
USR_CPPFLAGS += -DBUILDING_asyn_API
