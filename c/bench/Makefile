include ../../common.mk

FLATC?=flatc
PROTOC?=protoc

.PHONY: test
test: build
	build/bench
	@echo
	@$(FLATC) --version
	@$(PROTOC) --version

build: install
	$(COLF) -b build/gen -f -s 1024 c ../../testdata/bench/scheme.colf
	$(PROTOC) --cpp_out=build/gen -I../../testdata/bench ../../testdata/bench/scheme.proto
	$(FLATC) --cpp -o build/gen ../../testdata/bench/scheme.fbs

	$(CC) $(CFLAGS) -o build/Colfer.o -c -std=c99 -O3 build/gen/Colfer.c
	$(CC) $(CFLAGS) -o build/bench -std=c++11 -O3 -lstdc++ -lbenchmark bench.cpp build/Colfer.o

.PHONY: clean
clean:
	rm -fr build
