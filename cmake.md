# Cmake exampe

### Default
```make
# make
all:
    gcc main.c lib1.c lib2.c -o main
```
```bash
# launch
make all
```
### Spit into stages
```make
all: main

main: main.o lib1.o lib2.o
    gcc main.o lib1.o lib2.o -o main

main.o: main.c lib1.h lib2.h
    gcc -c main.c

lib1.o: lib1.c lib1.h
    gcc -c lib1.c

lib2.o: lib2.c lib2.h
    gcc -c lib2.c

clean:
    rm -rf *.o main
```

### With variables
```make
CC = gcc
CFLAGS = -Wall

all: main

main: main.o lib1.o lib2.o
    $(СС) main.o lib1.o lib2.o -o main

main.o: main.c lib1.h lib2.h
    $(CC) $(CFLAGS) -c main.c

lib1.o: lib1.c lib1.h
    $(CC) $(CFLAGS) -c lib1.c

lib2.o: lib2.c lib2.h
    $(CC) $(CFLAGS) -c lib2.c

clean:
    rm -rf *.o main
```

### More variables
```make
CC=gcc
CFLAGS=-c -Wall
LDFLAGS= 
SOURCES=main.c lib1.c lib2.c
OJBECTS=$(SOURCES:.c=.o)
EXECUTABLE=main

all: $(SOURCES) $(EXECUTABLE)

$(EXECUTABLE): $(OBJECTS)
    $(CC) $(LDFLAGS) $(OJBECTS) -o $@

.c.o:
    $(CC) $(CFLAGS) $< -o $@
```


