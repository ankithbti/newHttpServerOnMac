###############
## Makefile
###############

BIN=../bin/Binary
STATIC_LIB=../lib/libAdd.a
SHARED_LIB=../lib/libAdd.so
BOOST_INSTALL_ROOT=/usr/local

ARCH = $(shell uname -m)	# ARCH becomes the output from the uname -m command.
CXX=/usr/bin/g++
CXXFLAGS=-g -O2 -Wall $(INCS) $(ARCH)

SRCS = Add.cpp
MAIN_SRC = Main.cpp HttpServer.cpp HttpClientConnManager.cpp HttpClientConnection.cpp HttpHeader.cpp HttpRequest.cpp

OBJS = $(patsubst %.cpp, %.o, $(SRCS))
MAIN_OBJ = $(patsubst %.cpp, %.o, $(MAIN_SRC))

INCS = -I../include \
       -I$(BOOST_INSTALL_ROOT)/include \

LIBS = \
        -lboost_thread-mt \
        -lboost_system-mt \
	-lpthread
	
$(BIN): $(OBJS) $(MAIN_OBJ)
	$(CXX) -o $(BIN) $(OBJS) $(MAIN_OBJ) $(LIBS)

$(STATIC_LIB): $(OBJS)
	/usr/bin/ar rcs $(STATIC_LIB) $(OBJS)

$(SHARED_LIB): $(OBJS)
	$(CXX) -shared $^ -o $@

all: $(BIN) run

createlib: $(STATIC_LIB) $(SHARED_LIB)
	
run:
	@echo "----------------------------"
	@echo "Running the programme. "
	@echo "----------------------------"
	$(BIN)
	@echo "----------------------------"

clean:
	rm -rf $(BIN) *.o
