#目标文件(可执行文件)
TARGET=spider
#源文件(使用扩展通配符wildcard获取当前目录下所有的cpp文件)
SOURCES=$(wildcard *.cpp)
#依赖文件(使用替换通配符patsubst获取OBJS列表)
OBJS=$(patsubst %.cpp,%.o,$(SOURCES))

#编译器选项
CXX:=g++
#优化
OPTIMIZATION?=-O2 -DNDEBUG
WARNINGS=-Wall
#WARNINGS=-Wall -Werror
REAL_CXXFLAGS=$(OPTIMIZATION) $(CXXFLAGS) $(WARNINGS) $(DEBUG) $(PROF) 
#依赖的动态库
REAL_LDFLAGS=$(LDFLAGS) $(PROF) -rdynamic -lpthread -levent -lcrypt -ldl


#定义构建步骤和依赖关系
all: $(TARGET)
	@if [ ! -d ../download ]; then mkdir ../download; fi

#生成可执行文件
$(TARGET): $(OBJS)
	$(CXX) -o $@ $(REAL_LDFLAGS) $^

#生成目标文件
.cpp.o:
	$(CXX) -c $(REAL_CXXFLAGS) $<

clean:
	-rm -rf $(TARGET) $(OBJS)
	-rm -rf ../$(TARGET)

#-g选项,添加调试信息
debug:
	$(MAKE) OPTIMIZATION="" DEBUG="-g -ggdb -g3"

gprof:
	$(MAKE) PROF="-pg" 

install:
	-cp -f $(TARGET) ../

.PHONY: all clean debug gprof install
