#
# Makefile for the bcm963xx PCIe host controller drivers
#  for ARM and MIPS based platforms with 4.1 kernel onwards
#

PCIE_HCD_PATH=$(BRCMDRIVERS_DIR)/opensource/bus/pci/host/impl1
EXTRA_CFLAGS += -I$(PCIE_HCD_PATH)/common
EXTRA_CFLAGS += -I. -I$(INC_BRCMDRIVER_PUB_PATH)/$(BRCM_BOARD) -I$(INC_BRCMSHARED_PUB_PATH)/$(BRCM_BOARD) -I$(INC_BRCMBOARDPARMS_PATH)/$(BRCM_BOARD)
EXTRA_CFLAGS += -I$(INC_BRCMSHARED_PUB_PATH)/pmc

#
# ARM platforms
#
ifeq ($(filter y,$(CONFIG_ARM) $(CONFIG_ARM64)),)
else
EXTRA_CFLAGS += -I$(PCIE_HCD_PATH)/arm
obj-$(CONFIG_BCM_PCI) += arm/pcie-bcm963xx.o
ifeq ("$(CONFIG_ARM64)" ,"y")
#temporary until fill DT is implemented for arm64 platforms
obj-$(CONFIG_BCM_PCI) += ../../../../../../kernel/$(notdir $(KERNEL_DIR))/drivers/pci/setup-irq.o
endif
endif

#
# MIPS platforms
#

ifeq ("$(CONFIG_MIPS)" ,"y")
ifdef BCM_KF # defined(CONFIG_BCM_KF_PCI_FIXUP)
ifdef CONFIG_MIPS_BCM963XX
EXTRA_CFLAGS += -I$(PCIE_HCD_PATH)/mips
obj-$(CONFIG_BCM_PCI)	+= mips/pci-bcm963xx.o mips/fixup-bcm963xx.o mips/ops-bcm963xx.o
endif
endif # BCM_KF
endif

obj-$(CONFIG_BCM_PCI) += common/pcie_common.o

-include $(TOPDIR)/Rules.make

clean:
	rm -f core *.o *.a *.s

