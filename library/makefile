CC ?= gcc
CFLAGS ?= -O3
LDFLAGS ?= -O3
LIB_NAME = libjpeg
STAT_LIB_NAME = $(LIB_NAME).a
DYN_LIB_EXT = .so
DYN_LIB_NAME = $(LIB_NAME)$(DYN_LIB_EXT)
BIN_DIR = bin
OBJ_DIR = obj
SOURCES = $(wildcard *.c)
OBJS = $(patsubst %.c,$(OBJ_DIR)/%.o,$(SOURCES))

# There should be different obj folders for static and dynamic libs
# Dynamic lib should be compilied with gcc and -fPIC option (also for linker)

all: create_dirs $(BIN_DIR)/$(STAT_LIB_NAME) # $(BIN_DIR)/$(DYN_LIB_NAME)

create_dirs:
	mkdir -p $(BIN_DIR)
	mkdir -p $(OBJ_DIR)

$(BIN_DIR)/$(STAT_LIB_NAME): $(OBJS)
	ar rcs $@ $^

-include $(OBJS:.o=.d)

$(OBJ_DIR)/%.o: %.c
	$(CC) -c $(CFLAGS) $< -o $@
	$(CC) -MM -MP -MT $@ -MF $(OBJ_DIR)/$*.d $(CFLAGS) $<

.PHONY : clean create_dirs

clean:
	rm -rf $(OBJ_DIR)/*.o $(OBJ_DIR)/*.d $(BIN_DIR)/$(STAT_LIB_NAME)
