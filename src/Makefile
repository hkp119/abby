#!/bin/bash

CC=gcc
CFLAGS=-Wall -W -g -c
INCLUDE=-I../inc
TARGET=libhello.so
NEW_TARGET=libhello.so.0.0
SRCS=read.c write.c main.c
OBJS=$(SRCS:.c=.o)
CWD=$(PWD)

.SUFFIXES:.c.o
.c.o:
	$(CC) -fPIC $(CFLAGS) $(INCLUDE) $<

all: $(TARGET)
$(TARGET):$(OBJS)
	$(CC) -shared -Wl,-soname,$@ -o $(NEW_TARGET) $(OBJS) -lc
	ln -sf ./$(NEW_TARGET) ./$(TARGET)
	$(CC) -o main main.o -L. -lhello
	echo "$$PWD" >> /etc/ld.so.conf.d/my.conf
	ldconfig
	@echo done
dep:
	gccmakedep $(SRCS) $(INCLUDE)
clean:
	rm -rf test *.o 
	rm -rf lib*
