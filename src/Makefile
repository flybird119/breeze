CC = gcc
CFLAGS ?= -g -rdynamic -Wall -I. -I./json
LDFLAGS ?= -g -rdynamic -lcrypt -lm

objects = common.o log.o ioloop.o buffer.o iostream.o http.o stacktrace.o http_connection.o http_server.o site.o json.o mod_static.o mod.o breeze.o
testobjs = test_common.o test_log.o test_buffer.o test_ioloop.o test_iostream.o test_http.o test_http_server.o test_site.o
executables = test_common test_log test_buffer test_ioloop test_iostream test_http test_http_server test_site breeze

vpath %.c tests json

.PHONY: all
all: $(executables)

%.o: %.c %.h
	$(CC) $(CFLAGS) -c $< -o $@

test_%: test_%.o %.o common.o json.o stacktrace.o log.o
	$(CC) $(LDFLAGS) $^ -o $@

test_iostream: ioloop.o buffer.o
test_site: http.o ioloop.o iostream.o buffer.o http_connection.o mod.o mod_static.o
test_http: stacktrace.o iostream.o ioloop.o buffer.o http_connection.o
test_http_server: http_connection.o iostream.o ioloop.o buffer.o http.o site.o mod.o mod_static.o

breeze: $(objects)
	$(CC) $(LDFLAGS) $^ -o $@

.PHONY: clean
clean:
	-rm -f $(objects) $(executables) $(tests) $(testobjs)
	@echo Project cleaned

