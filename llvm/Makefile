# LLVM version.
# TODO: update to use LLVM 15.0 (instead of rc1)
VER=22.1.8

ROOT_DIR=$(shell pwd)

all: prepare

# Copy *.ll test cases.
.ONESHELL:
prepare: llvm-${VER}.src
	cd llvm-project-llvmorg-${VER}/llvm/test/
	find . -type d | xargs -I '{}' mkdir -p '${ROOT_DIR}/test/{}'
	find . -type f -name '*.ll' | xargs -I '{}' cp '{}' '${ROOT_DIR}/test/{}'
	cd ${ROOT_DIR}
	find test -type d | xargs -I '{}' rmdir -p --ignore-fail-on-non-empty '{}'

# Fetch source code.
fetch: llvm-${VER}.src

llvm-${VER}.src: | llvm-${VER}.tar.gz
	tar -xvf llvmorg-${VER}.tar.gz


llvm-${VER}.tar.gz:
	if [ -f "./llvmorg-${VER}.tar.gz" ]; then
		echo "File exists"
	else
		echo "--------begin fetching--------"
		wget -O $@ "https://github.com/llvm/llvm-project/archive/refs/tags/llvmorg-${VER}.tar.gz"
	fi
#
clean:
	find test -type f -name '*.ll' | xargs -I '{}' $(RM) '{}'
	find test -type d | xargs -I '{}' rmdir -p --ignore-fail-on-non-empty '{}'
	$(RM) -R llvmorg-${VER}
	$(RM) llvmorg-${VER}.tar.gz

.PHONY: all fetch clean
