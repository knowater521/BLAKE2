set(B2_COMPILE_OPTIONS -O3 ${COMMON_C_FLAGS})

add_compile_options( ${B2_COMPILE_OPTIONS} )

# Build executables with check definition and target for running them if -DCHECK_BUILD=1 is passed
if( CHECK_BUILD )
	include_directories(../testvectors)
	add_executable(blake2s)
    add_executable(blake2b)
    add_executable(blake2sp)
    add_executable(blake2xb)
    add_executable(blake2bp)
    add_executable(blake2xs)
	target_compile_definitions(blake2b  PRIVATE BLAKE2B_SELFTEST )
	target_compile_definitions(blake2s  PRIVATE BLAKE2S_SELFTEST )
	target_compile_definitions(blake2sp PRIVATE BLAKE2SP_SELFTEST)
	target_compile_definitions(blake2xb PRIVATE BLAKE2XB_SELFTEST)
	target_compile_definitions(blake2bp PRIVATE BLAKE2BP_SELFTEST)
	target_compile_definitions(blake2xs PRIVATE BLAKE2XS_SELFTEST)
# Build libraries and b2sum is nothing is passed
else()
	add_library(blake2s)
    add_library(blake2b)
    add_library(blake2sp)
    add_library(blake2xb)
    add_library(blake2bp)
    add_library(blake2xs)
endif()

target_include_directories(blake2b  INTERFACE ${CMAKE_CURRENT_SOURCE_DIR} )
target_include_directories(blake2s  INTERFACE ${CMAKE_CURRENT_SOURCE_DIR} )
target_include_directories(blake2sp INTERFACE ${CMAKE_CURRENT_SOURCE_DIR} )
target_include_directories(blake2xb INTERFACE ${CMAKE_CURRENT_SOURCE_DIR} )
target_include_directories(blake2bp INTERFACE ${CMAKE_CURRENT_SOURCE_DIR} )
target_include_directories(blake2xs INTERFACE ${CMAKE_CURRENT_SOURCE_DIR} )

target_sources(blake2b
    PRIVATE
		blake2b.c
		blake2b-round.h
		blake2-impl.h
		blake2-config.h
		blake2b-load-sse41.h
		blake2b-load-sse2.h
	PUBLIC
		blake2.h
)

target_sources(blake2s
    PRIVATE
		blake2s.c
		blake2s-round.h
		blake2-impl.h
		blake2-config.h
		blake2s-load-sse41.h
		blake2s-load-xop.h
		blake2s-load-sse2.h
	PUBLIC
		blake2.h
)

target_sources(blake2sp
    PRIVATE
		blake2sp.c
		blake2s.c
		blake2s-round.h
		blake2-impl.h
		blake2-config.h
		blake2s-load-sse41.h
		blake2s-load-xop.h
		blake2s-load-sse2.h
	PUBLIC
		blake2.h
)

target_sources(blake2xb
    PRIVATE
		blake2xb.c
		blake2b.c
		blake2b-round.h
		blake2-impl.h
		blake2-config.h
		blake2b-load-sse41.h
		blake2b-load-sse2.h
	PUBLIC
		blake2.h
)

target_sources(blake2bp
    PRIVATE
		blake2bp.c
		blake2b.c
		blake2b-round.h
		blake2-impl.h
		blake2-config.h
		blake2b-load-sse41.h
		blake2b-load-sse2.h
	PUBLIC
		blake2.h
)

target_sources(blake2xs
    PRIVATE
		blake2xs.c
		blake2s.c
		blake2s-round.h
		blake2-impl.h
		blake2-config.h
		blake2s-load-sse41.h
		blake2s-load-xop.h
		blake2s-load-sse2.h
	PUBLIC
		blake2.h
)