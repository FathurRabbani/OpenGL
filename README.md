# Belajar OpenGL C++

# A. Download File library dan Software
1. [download software visual studio terbaru](https://visualstudio.microsoft.com/insiders/)
2. [download library GLFW windows pre-compiled binaries](https://www.glfw.org/download)
3. [download library glad](https://glad.dav1d.de/)
# B. konfigurasi visual studio
1. membuka software visual studio.
2. ketika memulai unduh workloads "desktop development with c++" dan klik install.
3. selesai install, create new project dengan pilihan empty project c++.
4. tentukan nama direktori dan alamat direktori untuk menyimpan project.
5. setelah itu klik kanan pada file nama "project" lalu klik properties.
6. pada properties klik linker > input > additional dependencies, tambahkan path "GLFW\glfw3.lib;opengl32.lib".
7. pada properties klik VC++ directories > library directories, tambahkan path "$(SolutionDir)\linking\lib;".
# C. Konfigurasi file library GLFW dan glad
1. buka folder alamat project yang tersimpan.
2. di dalam folder project buat folder baru bernama linking
3. di dalam folder linking buat folder baru bernama lib dan include
4. ekstrak file library GLFW dan Glad yang telah diunduh.
5. buka folder glfw-3.4.bin.WIN64 > Include, salin folder GLFW ke dalam folder project > linking > include.
6.  buka folder glfw-3.4.bin.WIN64 > LIB-vc2022, salin semua file .LIB dan tambahkan kedalam project > linking > lib > GLFW
7. buka folder hasil ekstrak glad, dan buka glad > include salin semua folder yang ada di dalam include ke dalam project > linking > include.
8. buka folder hasil ekstrak glad, buka glad > src, salin file glad.c ke dalam project berada satu path dengan main.cpp

# D. masukan kode program ini
```cpp
 #include <iostream>
#include <glad/glad.h>
#include <GLFW/glfw3.h>

void framebuffer_size_callback(GLFWwindow* window, int width, int height);

int main() {
	std::cout << "hello, world!" << std::endl;

	glfwInit();

	// opengl 3.3
	glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
	glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);

	glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

#ifdef __APPLE__
	glfwWindowHint(GLFW_OPENGL_FORWARD_COMPAT, GL_TRUE);
#endif // __APPLE__

	GLFWwindow* window = glfwCreateWindow(800, 600, "buka gl", NULL, NULL);

	// jika jendela tidak terbuka
	if (window == NULL) {
		std::cout << "gagal membuka opengl" << std::endl;
		glfwTerminate();
		return -1;
	}

	glfwMakeContextCurrent(window);

	if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)) {
		std::cout << "gagal inisialisasi GLAD!" << std::endl;
		return -1;
	}
	glViewport(0, 0, 800, 600);

	glfwSetFramebufferSizeCallback(window, framebuffer_size_callback);

	while (!glfwWindowShouldClose(window)) {
		// mengirim jendela baru
		glfwSwapBuffers(window);
		glfwPollEvents();
	}

	glfwTerminate();
	return 0;
}

void framebuffer_size_callback(GLFWwindow* window, int width, int height) {
	glViewport(0, 0, width, height);
}

```

lalu klik local  windows debugger.

# E. jika muncul kode error

## eror 1
![[media\error.png]]
solusinya adalah memindahkan urutan header 
```cpp
#include <GLFW/glfw3.h>
#include <glad/glad.h>
```
menjadi
```cpp
#include <glad/glad.h>
#include <GLFW/glfw3.h>
```
maka masalah error akan menghilang

## masalah eror 2
![[media\msvcr120.png]]
jika muncul "eror msvcr120.dll not found", maka perlu mengunduh file msvcr120 dari media browser, lalu file hasil unduh dimasukan ke dalam "local disk > windows > SysWOW64 dan local disk > windows > System32" setelah itu restart.