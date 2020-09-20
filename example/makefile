CC ?= gcc
CCFLAGS ?= -O3 -I ../library
LDFLAGS ?= -O3 -L ../library/bin -l jpeg -Wl,-rpath,\$$ORIGIN/../../library/bin
BIN_DIR = bin
OBJ_DIR = obj
CJPEG_SOURCES = cjpeg.c cdjpeg.c
DJPEG_SOURCES = djpeg.c cdjpeg.c
CJPEG_OBJS = $(patsubst %.c,$(OBJ_DIR)/%.o,$(CJPEG_SOURCES))
DJPEG_OBJS = $(patsubst %.c,$(OBJ_DIR)/%.o,$(DJPEG_SOURCES))

all: create_dirs cjpeg djpeg

create_dirs:
	mkdir -p $(BIN_DIR)
	mkdir -p $(OBJ_DIR)

cjpeg: $(CJPEG_OBJS)
	$(CC) $^ -o $(BIN_DIR)/$@ $(LDFLAGS)

djpeg: $(DJPEG_OBJS)
	$(CC) $^ -o $(BIN_DIR)/$@ $(LDFLAGS)

# Include target dependencies
-include $(CJPEG_OBJS:.o=.d)
-include $(DJPEG_OBJS:.o=.d)

# Compile .c file and generate its dependencies in .d file
$(OBJ_DIR)/%.o: %.c
	$(CC) -c $< $(CCFLAGS) -o $@
	$(CC) -MM -MP -MT $@ -MF $(OBJ_DIR)/$*.d $(CCFLAGS) $<

.PHONY : clean create_dirs cjpeg djpeg

clean:
	rm -rf $(OBJ_DIR)
