CASESRC = $(shell find cases -name "*.c")
CASES = $(patsubst %.c,%,$(CASESRC))

CFLAGS ?= -g -Wall -Wextra
FLAGS = $(CFLAGS) -DSNOW_ENABLED
VGFLAGS ?= \
	--quiet --leak-check=full --show-leak-kinds=all \
	--track-origins=yes --error-exitcode=1

test-snow: test.c $(CASES) snow/snow.h
	$(CC) -I. $(FLAGS)  -o $@ $<

cases/%: cases/%.c ../snow/snow.h
	$(CC) -I.. $(FLAGS) -o $@ $<

test: test-snow
	valgrind $(VGFLAGS) ./test-snow

clean:
	rm -f test-snow $(CASES)

.PHONY: test clean
