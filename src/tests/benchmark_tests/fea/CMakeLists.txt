# ------------------------------------------------------------------------------
# Additional include paths and libraries
# ------------------------------------------------------------------------------

if(NOT ENABLE_MODULE_IRRLICHT)
    return()
endif()

# ------------------------------------------------------------------------------

set(COMPILER_FLAGS "${CH_CXX_FLAGS}")
set(LINKER_FLAGS "${CH_LINKERFLAG_EXE}")
list(APPEND LIBS "ChronoEngine")

include_directories(${CH_IRRLICHTINC})
set(COMPILER_FLAGS "${COMPILER_FLAGS} ${CH_IRRLICHT_CXX_FLAGS}")
list(APPEND LIBS "ChronoEngine_irrlicht")

# ------------------------------------------------------------------------------

set(TESTS
  btest_FEA_ANCFshell
  btest_FEA_contact
)

foreach(PROGRAM ${TESTS})
    message(STATUS "...add ${PROGRAM}")

    add_executable(${PROGRAM}  "${PROGRAM}.cpp")
    source_group(""  FILES "${PROGRAM}.cpp")

    set_target_properties(${PROGRAM} PROPERTIES
        FOLDER tests
        COMPILE_FLAGS "${COMPILER_FLAGS}"
        LINK_FLAGS "${LINKER_FLAGS}"
    )
    target_link_libraries(${PROGRAM} ${LIBS} benchmark_main)
endforeach(PROGRAM)
