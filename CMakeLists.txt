cmake_minimum_required(VERSION 3.18)
project(cuda_gsplat_core LANGUAGES CXX CUDA)

# Set standards
set(CMAKE_CUDA_STANDARD 17)
set(CMAKE_CXX_STANDARD 17)

# Optional: use CUDA fast math
option(CUDA_FAST_MATH "Enable fast math optimizations" ON)
if (CUDA_FAST_MATH)
  target_compile_options(gsplat_core PRIVATE $<$<COMPILE_LANGUAGE:CUDA>:--use_fast_math>)
endif()

# Add your source files here
add_executable(gsplat_core
    src/main.cpp
    src/rasterize_points.cu
)

# Optional: set target properties
set_target_properties(gsplat_core PROPERTIES
    CUDA_SEPARABLE_COMPILATION ON
    CUDA_ARCHITECTURES 86 # Adjust if needed
)
