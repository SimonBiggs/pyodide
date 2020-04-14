PYODIDE_ROOT=$(abspath ..)
include ../Makefile.envs

all: emsdk/.complete

emsdk/.complete:
	if [ -d emsdk ]; then rm -rf emsdk; fi
	git clone --depth 1 https://github.com/juj/emsdk.git
	( \
		cd emsdk && \
		./emsdk install --build=Release sdk-fastcomp-$(EMSCRIPTEN_VERSION)-64bit binaryen-$(EMSCRIPTEN_VERSION)-64bit && \
		cd ./binaryen/$(EMSCRIPTEN_VERSION)_64bit_binaryen/ && \
    make && \
	  cd ../../.. && \
		cd emsdk/clang/fastcomp/build_$(EMSCRIPTEN_VERSION)_64/ && \
    make && \
    cd ../../.. && \
		./emsdk activate --embedded --build=Release sdk-fastcomp-$(EMSCRIPTEN_VERSION)-64bit binaryen-$(EMSCRIPTEN_VERSION)-64bit && \
    touch .complete \
	)

clean:
	rm -rf emsdk
