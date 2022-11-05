# get options
cxxabi_enable_exceptions = get_option('libcxxabi_enable_exceptions')
cxxabi_enable_assertions = get_option('libcxxabi_enable_assertions')
cxxabi_enable_pedantic = get_option('libcxxabi_enable_pedantic')
cxxabi_enable_werror = get_option('libcxxabi_enable_werror')
cxxabi_use_llvm_unwinder = get_option('libcxxabi_use_llvm_undwinder')
cxxabi_use_compiler_rt = get_option('libcxxabi_use_compiler_rt')
cxxabi_enable_threads = get_option('libcxxabi_enable_threads')
cxxabi_has_pthread_api = get_option('libcxxabi_has_pthread_api')
cxxabi_has_extrenal_thread_library = get_option('libcxxabi_has_external_thread_library')
cxxabi_build_external_thread_library = get_option('libcxxabi_build_external_thread_library')
cxxabi_enable_forgiving_dynamic_cast = get_option('libcxxabi_enable_forgiving_dynamic_cast')
cxxabi_enable_new_delete_definitions = get_option('libcxxabi_enable_new_delete_definitions')
cxxabi_enable_static = get_option('libcxxabi_enable_static')
cxxabi_enable_shared = get_option('libcxxabi_enable_shared')
cxxabi_baremetal = get_option('libcxxabi_baremetal')
cxxabi_silent_terminate = get_option('libcxxabi_silent_terminate')
cxxabi_non_demangling_terminate = get_option('libcxxabi_non_demangling_terminate')
cxxabi_hermetic_static_library = get_option('libcxxabi_hermetic_static_library')

# handle warning args
cxxabi_wanted_warning_args = [
  '-Werror=return-type',
  '-W',
  '-Wall',
  '-Wchar-subscripts',
  '-Wconversion',
  '-Wmismatched-tags',
  '-Wmissing-braces',
  '-Wnewline-eof',
  '-Wunused-function',
  '-Wshadow',
  '-Wshorten-64-to-32',
  '-Wsign-compare',
  '-Wsign-conversion',
  '-Wstrict-aliasing=2',
  '-Wstrict-overflow=4',
  '-Wunused-parameter',
  '-Wunused-variable',
  '-Wwrite-strings',
  '-Wundef',
  '-Wno-suggest-override',
  ]

if cxxabi_enable_werror
  cxxabi_wanted_warning_args += [
    '-Werror',
    '-WX',
    ]
else
  cxxabi_wanted_warning_args += [
    '-Wno-error',
    '-WX-',
    ]
endif

# definitions
cxxabi_def = [
  '-D_LIBCXXABI_BUILDING_LIBRARY',
  '-D_LIBCPP_BUILDING_LIBRARY'
  ]
