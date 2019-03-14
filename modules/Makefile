TOP = ..
include $(TOP)/configure/CONFIG

# Submodules
SUBMODULES += motorOms

# Allow sites to add extra submodules
-include Makefile.local

# Add only checked-out submodules to DIRS
DIRS += $(subst /Makefile,,$(wildcard $(addsuffix /Makefile, $(SUBMODULES))))

include $(TOP)/configure/RULES_DIRS

INSTALL_LOCATION_ABS := $(abspath $(INSTALL_LOCATION))
RELEASE_LOCAL := RELEASE.$(EPICS_HOST_ARCH).local

# Ensure that RELEASE.<host>.local exists before doing anything else
all host $(DIRS) $(ARCHS) $(ACTIONS) $(dirActionTargets) $(dirArchTargets) \
    $(dirActionArchTargets) $(actionArchTargets): | $(RELEASE_LOCAL)

$(RELEASE_LOCAL):
	$(ECHO) Creating $@, EPICS_BASE = $(INSTALL_LOCATION_ABS)
	@echo EPICS_BASE = $(INSTALL_LOCATION_ABS)> $@
	$(ECHO) Creating $@, ASYN = $(ASYN)
	@echo ASYN = $(ASYN)>> $@
	$(ECHO) Creating $@, SNCSEQ = $(SNCSEQ)
	@echo SNCSEQ = $(SNCSEQ)>> $@
	$(ECHO) Creating $@, BUSY = $(BUSY)
	@echo BUSY = $(BUSY)>> $@
	$(ECHO) Creating $@, IPAC = $(IPAC)
	@echo IPAC = $(IPAC)>> $@

realclean:
	$(RM) $(RELEASE_LOCAL)
