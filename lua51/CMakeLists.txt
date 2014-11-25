set(library_source_names
lapi.c      lcode.c   ldo.c    lgc.c     llex.c      loadlib.c   loslib.c   lstring.c  ltablib.c  lzio.c
lauxlib.c   ldblib.c  ldump.c  linit.c   lmathlib.c  lobject.c   lparser.c  lstrlib.c  ltm.c      lundump.c  print.c
lbaselib.c  ldebug.c  lfunc.c  liolib.c  lmem.c      lopcodes.c  lstate.c   ltable.c   lvm.c)

set(source_dir "lua-5.1.5/src")
foreach(name ${library_source_names})
	list(APPEND library_sources ${source_dir}/${name})
endforeach()

add_library(lua51_lib ${library_sources})
set_target_properties(lua51_lib PROPERTIES OUTPUT_NAME "lua51")

add_executable(lua51_host ${source_dir}/lua.c)
set_target_properties(lua51_host PROPERTIES OUTPUT_NAME "lua")
target_link_libraries(lua51_host lua51_lib)

add_executable(lua51_compiler ${source_dir}/luac.c)
set_target_properties(lua51_compiler PROPERTIES OUTPUT_NAME "luac")
target_link_libraries(lua51_compiler lua51_lib)

set(install_dir "lua51")
install(TARGETS lua51_lib lua51_host lua51_compiler
	RUNTIME DESTINATION ${install_dir}
	LIBRARY DESTINATION ${install_dir}
	ARCHIVE DESTINATION ${install_dir}
)
install(DIRECTORY "${source_dir}/" DESTINATION "${install_dir}/include")
