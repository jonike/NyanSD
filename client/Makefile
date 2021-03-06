# Makefile for the NyanSD reference implementation client.
#
# 2020/04/27, Maya Posch

GCC = g++
MAKEDIR = mkdir -p
RM = rm

OUTPUT = nyansd_client
INCLUDE = -I $(TOP)/src
LIB := -L ../lib -lnyansd -lPocoNet -lPocoUtil -lPocoFoundation
CFLAGS := $(INCLUDE) -std=c++11 -g3

# Check for MinGW and patch up POCO
# The OS variable is only set on Windows.
ifdef OS
	CFLAGS := $(CFLAGS) -U__STRICT_ANSI__ -DPOCO_WIN32_UTF8
	#LIB += -lws2_32
else
	LIB += -pthread
endif

SOURCES := $(wildcard *.cpp)
OBJECTS := $(addprefix obj/,$(notdir) $(SOURCES:.cpp=.o))

all: makedir bin/$(OUTPUT)

makedir:
	$(MAKEDIR) obj
	$(MAKEDIR) bin

obj/%.o: %.cpp
	$(GCC) -c -o $@ $< $(CFLAGS)
	
bin/$(OUTPUT): $(OBJECTS)
	$(GCC) -o $@ $(OBJECTS) $(LIB)

clean:
	$(RM) $(OBJECTS)
	