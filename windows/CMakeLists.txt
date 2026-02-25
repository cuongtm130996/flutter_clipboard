# List of plugin source files
list(APPEND PLUGIN_SOURCES
  "clipboard_plugin.cpp"
  "clipboard_plugin.h"
)

# Create the plugin target
add_library(clipboard_plugin SHARED
  ${PLUGIN_SOURCES}
)

# Apply standard settings
target_compile_features(clipboard_plugin PUBLIC cxx_std_17)
target_compile_options(clipboard_plugin PRIVATE /W4 /wd"4100")
target_compile_options(clipboard_plugin PRIVATE /EHsc)
target_compile_definitions(clipboard_plugin PRIVATE "_HAS_EXCEPTIONS=0")
target_compile_definitions(clipboard_plugin PRIVATE "$<$<CONFIG:Debug>:_DEBUG>")
target_compile_definitions(clipboard_plugin PRIVATE "NOMINMAX")

# Link against Flutter plugin wrapper
target_link_libraries(clipboard_plugin PRIVATE flutter_wrapper_plugin)

# Required Windows system libraries
target_link_libraries(clipboard_plugin PRIVATE gdiplus shlwapi)

# 🔥 Quan trọng: expose parent folder để resolve
# <clipboard/clipboard_plugin.h>
target_include_directories(clipboard_plugin PUBLIC
  "${CMAKE_CURRENT_SOURCE_DIR}/.."
)