include(FindPkgConfig)

pkg_check_modules(libuv REQUIRED IMPORTED_TARGET libuv)

if("${wren_SOURCE_DIR}" STREQUAL "")
    find_package(wren CONFIG REQUIRED)
else()
    add_subdirectory("${wren_SOURCE_DIR}" "${PROJECT_BINARY_DIR}/wren")
endif()

add_executable(wren_cli
    "cli/main.c"
    "cli/modules.c"
    "cli/modules.h"
    "cli/path.c"
    "cli/path.h"
    "cli/stat.h"
    "cli/vm.c"
    "cli/vm.h"
    "module/io.c"
    "module/io.h"
    "module/os.c"
    "module/os.h"
    "module/repl.c"
    "module/repl.h"
    "module/scheduler.c"
    "module/scheduler.h"
    "module/timer.c"
)
target_include_directories(wren_cli PRIVATE
    "cli"
    "module"
)
target_link_libraries(wren_cli
    PRIVATE
        wren::wren
        PkgConfig::libuv
)
set_property(TARGET wren_cli PROPERTY COMPILE_WARNING_AS_ERROR ON)
set_property(TARGET wren_cli PROPERTY OUTPUT_NAME wren)
