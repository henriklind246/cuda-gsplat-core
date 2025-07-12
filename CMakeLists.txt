cmake_minimum_required(VERSION 3.25)
project(cuda_gsplat_core LANGUAGES CXX CUDA)

# 1. Create the target **before** you tweak it
add_library(gsplat_core STATIC
    src/rasterize_points.cu
    src/main.cpp         # placeholder driver
)

# 2. Tell CMake where the public headers live
target_include_directories(gsplat_core PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

# 3. Choose language standards
target_compile_features(gsplat_core PUBLIC cxx_std_20 cuda_std_20)

# 4. Add any extra flags (now the target exists, so this is safe)
target_compile_options(gsplat_core PRIVATE
    $<$<COMPILE_LANGUAGE:CUDA>:--use_fast_math>
)
