CC = gcc

DEBUG_FLAGS = -g -Wall
RELEASE_FLAGS = -O2

MODE ?= DEBUG

ifeq ($(MODE),DEBUG)
CFLAGS = $(DEBUG_FLAGS)
else
CFLAGS = $(RELEASE_FLAGS)
endif

SRC = $(wildcard src/*.c)

OBJ = $(patsubst src/%.c,build/%.o,$(SRC))

DEP = $(OBJ:.o=.d)

all: myls mycat mycp

build/%.o: src/%.c
	$(CC) $(CFLAGS) -MMD -Iinclude -c $< -o $@

myls: build/myls.o build/utils.o
	$(CC) $^ -o bin/myls

mycat: build/mycat.o build/utils.o
	$(CC) $^ -o bin/mycat

mycp: build/mycp.o build/utils.o
	$(CC) $^ -o bin/mycp

install:
	cp bin/* bin/installed/

uninstall:
	rm -f bin/installed/*

debug:
	make MODE=DEBUG

release:
	make MODE=RELEASE

package:
	tar -czf linux_tools.tar.gz *

clean:
	rm -rf build/*.o build/*.d bin/myls bin/mycat bin/mycp

.PHONY: all clean install uninstall debug release package

-include $(DEP)
