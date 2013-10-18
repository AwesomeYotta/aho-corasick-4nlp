-include rules.mk
# GMAKE stupidly trims off leading "./" where least appropriate
export acism ?= .
CFLAGS = -g

#---------------- PRIVATE VARS:
# acism.pgms: test programs requiring no args

acism.c          = $(patsubst %,$(acism)/%, acism.c acism_create.c acism_dump.c acism_file.c)
acism.pgms       = $(acism)/acism_x $(acism)/acism_mmap_x

#---------------- PUBLIC VARS:
acism.lib       = $(acism)/libacism.a
acism.include   = $(acism)/acism.h

#---------------- PUBLIC TARGETS (see rules.mk):
all             : $(acism.lib)
test            : $(acism)/acism_t.pass

# Activate default actions for (clean,install):
acism.clean 	= $(acism)/*.tmp
install .PHONY  : acism.install

#---------------- PRIVATE RULES:
$(acism.lib)	: $(acism.c:c=o)

$(acism)/acism_t.pass : $(acism.pgms) $(acism)/words

$(acism.pgms)   : CPPFLAGS := -I$(acism) $(CPPFLAGS)
$(acism.pgms)   : $(acism.lib) $(acism)/msutil.o $(acism)/tap.o

# Include auto-generated depfiles (gcc -MMD):
-include $(acism)/*.d

%.i : CPPFLAGS += -I$(acism)

# vim: set nowrap :
