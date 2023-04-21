cmake_minimum_required(VERSION 3.24)

project(SpleeterRT)

add_executable(SpleeterRT
        codelet.c
        cpthread.c
        gemm.c
        im2col_dilated.c
        libsr_samplerate.c
        libsr_src_sinc.c
        main.c
        spleeter.c
        stftFix.c)

if (CMAKE_SYSTEM_NAME STREQUAL "Linux")
    target_include_directories(SpleeterRT PUBLIC "~/intel/oneapi/mkl/latest/include/")
    target_link_directories(SpleeterRT PUBLIC
            "~/intel/oneapi/mkl/latest/lib/intel64/"
            "~/OpenBLAS/lib/")
endif()

target_link_libraries(SpleeterRT PUBLIC
        #Linking order matters! Alphabetic often will not work here.
        openblas
        mkl_intel_lp64 #Depends on mkl_core
        mkl_core
        mkl_sequential
        m)
