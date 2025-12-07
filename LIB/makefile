CC=g++

SHARED_PATH= src/shared
STATIC_PATH= src/static
INCLUDE_PATH= inc

CFLAGS= -c -I $(INCLUDE_PATH) -O3
LFLAGS= -O3

SHARED_CFLAGS= $(CFLAGS) -fpic
STATIC_CFLAGS= $(CFLAGS)

SHARED_LFLAGS= $(LFLAGS) -shared


FILENAMES= Matrix zeroMatrix squareMatrix upTriangleMatrix downTriangleMatrix unityMatrix diagonalMatrix
INCLUDE_FILES= $(FILENAMES:%=$(INCLUDE_PATH)/%.hpp)
SHARED_OBJECTS= $(FILENAMES:%=$(SHARED_PATH)/%.o)
STATIC_OBJECTS= $(FILENAMES:%=$(STATIC_PATH)/%.o)

all: shared static copy

shared: $(SHARED_OBJECTS)
	$(CC) $(SHARED_LFLAGS) $(SHARED_OBJECTS) -o output/libKRMatrix.so

static: $(STATIC_OBJECTS)
	ar rcs output/libKRMatrix.a $(STATIC_OBJECTS)

copy:
	cp $(INCLUDE_FILES) output

$(SHARED_PATH)/%.o: src/%.cpp mkdirs
	$(CC) $(SHARED_CFLAGS) $< -o $@

$(STATIC_PATH)/%.o: src/%.cpp mkdirs
	$(CC) $(STATIC_CFLAGS) $< -o $@

mkdirs:
	mkdir -p $(STATIC_PATH)
	mkdir -p $(SHARED_PATH)
	mkdir -p output

clean:
	rm -rf $(STATIC_PATH)
	rm -rf $(SHARED_PATH)
	rm -rf output
	
