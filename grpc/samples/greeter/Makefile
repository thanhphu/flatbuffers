CXXFLAGS = -I/home/thanhphu/Code/flatbuffers/include `pkg-config --cflags grpc grpc++`
LDFLAGS = -lgrpc -lgrpc++ -lgrpc++_unsecure -lgrpc++_reflection -lgpr

# LD_LIBRARY_PATH ?= /home/thanhphu/Code/grpc/libs/dbg
.PHONY: all
all: greeter_generated.h greeter_server greeter_client

greeter_generated.h: greeter.fbs
	flatc --grpc --cpp $<

greeter_server: server.cpp greeter.grpc.fb.cc greeter_generated.h greeter.grpc.fb.h
	g++ -std=c++17 -g $(CXXFLAGS) server.cpp greeter.grpc.fb.cc $(LDFLAGS) -o $@

greeter_client: client.cpp greeter.grpc.fb.cc greeter_generated.h greeter.grpc.fb.h
	g++ -std=c++17 -g $(CXXFLAGS) client.cpp greeter.grpc.fb.cc $(LDFLAGS) -o $@

clean:
	rm greeter_server
	rm greeter_client