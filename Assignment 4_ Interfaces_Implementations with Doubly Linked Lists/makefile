GCC_OPTIONS = -std=c11 -pedantic-errors -Wstrict-prototypes -Wall -Wextra  -Werror -Werror=vla
OBJS = qdriver.o q.o
EXEC = q.out

$(EXEC) : $(OBJS)
	gcc $(GCC_OPTIONS) $(OBJS) -o q.out -lm
	
qdriver.o : qdriver.c q.h
	gcc $(GCC_OPTIONS) -c qdriver.c -o qdriver.o
	
q.o : q.c q.h
	gcc $(GCC_OPTIONS) -c q.c -o q.o

clean:
	rm $(OBJS) $(EXEC)
# name of C++ compiler
CXX       = g++
# options to C++ compiler
CXX_FLAGS = -std=c++17 -pedantic-errors -Wall -Wextra -Werror
# flag to linker to make it link with math library
LDLIBS    = -lm
# list of object files
OBJS      = dllist-driver.o dllist.o
# name of executable program
EXEC      = dllist.out

# by convention the default target (the target that is built when writing
# only make on the command line) should be called all and it should
# be the first target in a makefile
all : $(EXEC)

# however, the problem that arises with the previous rule is that make
# will think all is the name of the target file that should be created
# so, we tell make that all is not a file name
.PHONY : all

# this rule says that target $(EXEC) will be built if prerequisite
# files $(OBJS) have changed more recently than $(EXEC)
# text $(EXEC) will be replaced with value dllist.out
# text $(OBJS) will be substituted with list of prerequisites in line 10
# line 31 says to build $(EXEC) using command $(CXX) with
# options $(CXX_FLAGS) specified on line 6
$(EXEC) : $(OBJS)
	$(CXX) $(CXX_FLAGS) $(OBJS) -o $(EXEC) $(LDLIBS)

# target dllist-driver.o depends on both dllist-driver.cpp and dllist.h
# and is created with command $(CXX) given the options $(CXX_FLAGS)
dllist-driver.o : dllist-driver.cpp dllist.h
	$(CXX) $(CXX_FLAGS) -c dllist-driver.cpp -o dllist-driver.o
	
# target dllist.o depends on both dllist.cpp and dllist.h
# and is created with command $(CXX) given the options $(CXX_FLAGS)
dllist.o : dllist.cpp dllist.h
	$(CXX) $(CXX_FLAGS) -c dllist.cpp -o dllist.o

# says that clean is not the name of a target file but simply the name for
# a recipe to be executed when an explicit request is made
.PHONY : clean
# clean is a target with no prerequisites;
# typing the command in the shell: make clean
# will only execute the command which is to delete the object files
clean :
	rm -f $(OBJS) $(EXEC)

# says that rebuild is not the name of a target file but simply the name
# for a recipe to be executed when an explicit request is made
.PHONY : rebuild
# rebuild is for starting over by removing cleaning up previous builds
# and starting a new one
rebuild :
	$(MAKE) clean
	$(MAKE)

.PHONY : test
test : $(EXEC)
	./$(EXEC) > your-output.txt
	diff -y --strip-trailing-cr --suppress-common-lines your-output.txt output.txt