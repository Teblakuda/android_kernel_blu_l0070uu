#FPGA project no need build-in
ifndef CONFIG_MTK_FPGA 

# ccci_util is build after eccci or later
ifdef CONFIG_MTK_ECCCI_DRIVER

include $(srctree)/drivers/misc/mediatek/Makefile.custom
ccflags-y += -I$(srctree)/drivers/misc/mediatek/ccci_util

obj-y += ccci_util_lib.o
ccci_util_lib-y := ccci_util_lib_fo.o
ccci_util_lib-y += ccci_util_lib_load_img.o
ccci_util_lib-y += ccci_util_lib_sys.o
ccci_util_lib-y += ccci_private_log.o
ccci_util_lib-y += ccci_util_lib_time.o
ccci_util_lib-y += ccci_util_lib_main.o

endif 

ifeq ($(CONFIG_MTK_SECURITY_SW_SUPPORT), y)
ccflags-y  += -DENABLE_MD_IMG_SECURITY_FEATURE
endif
ifeq ($(CONFIG_MTK_SEC_MODEM_NVRAM_ANTI_CLONE), y)
ccflags-y  += -DMTK_SEC_MODEM_NVRAM_ANTI_CLONE
endif

# always build platform, for power off md
MTK_PLATFORM_DIR=$(srctree)/drivers/misc/mediatek/ccci_util/$(subst ",,$(CONFIG_MTK_PLATFORM))
mtkplatform_exist=$(shell if [ -d ${MTK_PLATFORM_DIR} ]; then echo "y"; else echo "n"; fi;)
ifeq ($(mtkplatform_exist), y)
obj-y += $(subst ",,$(CONFIG_MTK_PLATFORM))/
endif

# wanglj, DATE20150806, NOTE, Bug FADALTHA-127 START
WIKO_ONE := $(strip $(subst ro.subproject =,,$(shell cat $(PWD)/../build.ini |grep ^ro.subproject)))
$(warning --[wlj]--WIKO_ONE-$(WIKO_ONE))
ifeq ($(WIKO_ONE), l5460_one)
ccflags-y += -DCONFIG_PROJECT_WIKO_ONE
$(warning --[wlj]--add new macro--CONFIG_PROJECT_WIKO_ONE--)
endif
# wanglj, Bug FADALTHA-127 END

endif

obj-y += ccci_util_dummy.o # avoid build error
