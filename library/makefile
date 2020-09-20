CC ?= gcc
CCFLAGS_STC ?= -O3
CCFLAGS_DYM ?= -O3 -fPIC
LDFLAGS_DYN ?= -O3 -fPIC
LIB_NAME = libjpeg
LIB_EXT_STC ?= .a
LIB_EXT_DYN ?= .so
BIN_DIR = bin
OBJ_DIR_STC = obj_stc
OBJ_DIR_DYN = obj_dyn
SOURCES := $(wildcard *.c)
OBJS_STC := $(patsubst %.c,$(OBJ_DIR_STC)/%.o,$(SOURCES))
OBJS_DYN := $(patsubst %.c,$(OBJ_DIR_DYN)/%.o,$(SOURCES))

all: create_dirs static_lib dynamic_lib

create_dirs:
	mkdir -p $(BIN_DIR)
	mkdir -p $(OBJ_DIR_STC)
	mkdir -p $(OBJ_DIR_DYN)

static_lib: $(OBJS_STC)
	ar rcs $(BIN_DIR)/$(LIB_NAME)$(LIB_EXT_STC) $^

dynamic_lib: $(OBJS_DYN)
	$(CC) -shared $^ -o $(BIN_DIR)/$(LIB_NAME)$(LIB_EXT_DYN) $(LDFLAGS_DYN)

# Include target dependencies
-include $(OBJS_STC:.o=.d)
-include $(OBJS_DYN:.o=.d)

# Compile .c file(for static library) and generate its dependencies in .d file
$(OBJ_DIR_STC)/%.o: %.c
	$(CC) -c $< $(CCFLAGS_STC) -o $@
	$(CC) -MM -MP -MT $@ -MF $(OBJ_DIR_STC)/$*.d $(CCFLAGS_STC) $<

# Compile .c file(for dynamic library) and generate its dependencies in .d file
$(OBJ_DIR_DYN)/%.o: %.c
	$(CC) -c $< $(CCFLAGS_DYM) -o $@
	$(CC) -MM -MP -MT $@ -MF $(OBJ_DIR_DYN)/$*.d $(CCFLAGS_DYM) $<

.PHONY : clean create_dirs static_lib dynamic_lib

clean:
	rm -rf $(OBJ_DIR_STC) $(OBJ_DIR_DYN) $(BIN_DIR)
