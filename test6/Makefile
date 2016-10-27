VULKAN_SDK_PATH = /home/sauron/VulkanSDK/1.0.24.0/x86_64/
STB_INCLUDE_PATH = /home/sauron/stb
CFLAGS = -std=c++11 -I$(VULKAN_SDK_PATH)/include -I$(STB_INCLUDE_PATH)
LDFLAGS = -L$(VULKAN_SDK_PATH)/lib `pkg-config --static --libs glfw3` -lvulkan
GLSLCOMPILER = $(VULKAN_SDK_PATH)/bin/glslangValidator

VulkanTest: main.cpp vert.spv frag.spv
	g++ $(CFLAGS) -o VulkanTest main.cpp $(LDFLAGS) -g

vert.spv: shader.vert
	$(GLSLCOMPILER) -V ./shader.vert

frag.spv: shader.frag
	$(GLSLCOMPILER) -V ./shader.frag
	

.PHONY: test clean

test: VulkanTest
	LD_LIBRARY_PATH=$(VULKAN_SDK_PATH)/lib VK_LAYER_PATH=$(VULKAN_SDK_PATH)/etc/explicit_layer.d ./VulkanTest

gdb: VulkanTest
	LD_LIBRARY_PATH=$(VULKAN_SDK_PATH)/lib VK_LAYER_PATH=$(VULKAN_SDK_PATH)/etc/explicit_layer.d gdb ./VulkanTest

clean:
	rm -f VulkanTest

