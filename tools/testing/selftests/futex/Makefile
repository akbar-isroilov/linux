# SPDX-License-Identifier: GPL-2.0
SUBDIRS := functional

TEST_PROGS := run.sh

include ../lib.mk

all:
	@for DIR in $(SUBDIRS); do		\
		BUILD_TARGET=$(OUTPUT)/$$DIR;	\
		mkdir $$BUILD_TARGET  -p;	\
		$(MAKE) OUTPUT=$$BUILD_TARGET -C $$DIR $@;\
		if [ -e $$DIR/$(TEST_PROGS) ]; then \
			rsync -a $$DIR/$(TEST_PROGS) $$BUILD_TARGET/; \
		fi \
	done

override define INSTALL_RULE
	mkdir -p $(INSTALL_PATH)
	install -t $(INSTALL_PATH) $(TEST_PROGS) $(TEST_PROGS_EXTENDED) $(TEST_FILES)

	@for SUBDIR in $(SUBDIRS); do \
		BUILD_TARGET=$(OUTPUT)/$$SUBDIR;	\
		mkdir $$BUILD_TARGET  -p;	\
		$(MAKE) OUTPUT=$$BUILD_TARGET -C $$SUBDIR INSTALL_PATH=$(INSTALL_PATH)/$$SUBDIR install; \
	done;
endef

override define CLEAN
	@for DIR in $(SUBDIRS); do		\
		BUILD_TARGET=$(OUTPUT)/$$DIR;	\
		mkdir $$BUILD_TARGET  -p;	\
		$(MAKE) OUTPUT=$$BUILD_TARGET -C $$DIR $@;\
	done
endef
