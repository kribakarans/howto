```make
# GNU Makefile

ELFNAME  :=  hello
TARGET   :=  $(ELFNAME).out

SRCDIR   :=  src
OBJDIR   :=  obj
GCOVDIR  := __coverage

CC       ?=  gcc
CFLAGS   := -g -O0
LDFLAGS  :=
LDLIBS   :=

# Source files
SRCS += $(SRCDIR)/hello.c

# Build object files
OBJS = $(SRCS:%.c=$(OBJDIR)/%.o)

# Build dependencies
DEPS = $(OBJS:%.o=%.d)

all: info $(TARGET)

info:
	@echo "TARGET   =  $(TARGET)"
	@echo "COMPILER =  $(CC)"
	@echo "CFLAGS   = $(CFLAGS)"
	@echo "LDFLAGS  = $(LDFLAGS)"
	@echo "LDLIBS   = $(LDLIBS)"

$(TARGET): $(OBJS)
	@echo  "\nLinking   ... object-files"
	@$(CC) -o $(TARGET) $(OBJS) $(LDFLAGS) $(LDLIBS)
	@echo "\nBuild completed [$(TARGET)]"

# Build object file for each .c file
$(OBJDIR)/%.o : %.c
	@mkdir -p $(@D)
	@printf "\nCompiling ... $<"
	@$(CC) $(CFLAGS) -c $< -o $@
	@printf "\33[2K\rCompiled  ... $<"

-include $(DEPS)

clean:
	rm -rf $(TARGET) $(OBJDIR) $(GCOVDIR)

#--------------------------------------------------
# Gcovr code coverage build rule procedure:
# 1. Append --coverage flag to CFLAGS and LDFLAGS
# 2. Compile the program with 'clean' && 'all'
# 3. Run target program with 'gcov_run_target'
# 4. Generate Gcovr report with 'gcov_exec'
#--------------------------------------------------

# Append gcov flags
coverage: CFLAGS  += --coverage
coverage: LDFLAGS += --coverage # or Add -lgcov to LDLIBS
coverage: clean all gcov_run_target gcov_exec

gcov_init: gcov_debug
	@mkdir -p $(GCOVDIR)

# Run target to generate .gda files
gcov_run_target:
	@echo "\nRunning target to generate '.gda' files ..."
	eval ./$(TARGET)

# Generate coverage reports in HTML format
gcov_exec: gcov_init
	@echo "\nGenerating coverage report ..."
	gcovr --html-details $(GCOVDIR)/coverage.html

gcov_debug: GCDA_FILES := $(SRCS:%.c=$(OBJDIR)/%.gcda)
gcov_debug: GCOV_FILES := $(GCDA_FILES:%.gcda=%.c.gcov)
gcov_debug:
	@echo "\nGCDA_FILES: $(GCDA_FILES)"
	@echo "GCOV_FILES: $(GCOV_FILES)"

.PHONY: all clean coverage

#EOF
```
