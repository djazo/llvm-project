# unwinding library

# get options
unwind_enable_cet = get_option('libunwind_enable_cet')
unwind_enable_assertions = get_option('libunwind_enable_assertions')
unwind_enable_pedantic = get_option('libunwind_enable_pedantic')
unwind_enable_werror = get_option('libunwind_enable_werror')
unwind_hide_symbols = get_option('libunwind_hide_symbols')
unwind_enable_cross_unwinding = get_option('libunwind_enable_cross_unwinding')
unwind_enable_threads = get_option('libunwind_enable_threads')
unwind_enable_arm_wmmx = get_option('libunwind_enable_arm_wmmx')
unwind_is_baremetal = get_option('libunwind_is_baremetal')
unwind_has_pthread_lib = get_option('libunwind_has_pthread_lib')
unwind_use_frame_header_cache = get_option('libunwind_use_frame_header_cache')

# handle warning args
unwind_wanted_warning_args = [
  '-W',
  '-Wall',
  '-Wchar-subscripts',
  '-Wconversion',
  '-Wmismatched-tags',
  '-Wmissing-braces',
  '-Wnewline-eof',
  '-Wno-unused-function',
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

if unwind_enable_werror
  unwind_wanted_warning_args += [
    '-Werror',
    '-WX',
    ]
else
  unwind_wanted_warning_args += [
    '-Wno-error',
    '-WX-'
    ]
endif

unwind_warning_args = cpp_com.get_supported_arguments(
  unwind_wanted_warning_args,
  checked: 'warn'
  )

# handle other args
unwind_wanted_args = []
if unwind_enable_pedantic
  unwind_wanted_args += '-pedantic'
endif

unwind_wanted_args += [
  '-fstrict-aliasing',
  '-EHsc',
  '-funwind-tables',
  '-fno-exceptions',
  '-fno-rtti',
  ]

unwind_compile_args = cpp_com.get_supported_arguments(
  unwind_wanted_args,
  checked: 'warn'
  )

# handle defines

unwind_defines = []
if unwind_enable_assertions
  unwind_defines += '-D_DEBUG'
endif

if not unwind_enable_cross_unwinding
  unwind_defines += '-D_LIBUNWIND_IS_NATIVE_ONLY'
endif

if not unwind_enable_threads
  unwind_defines += '-D_LIBUNWIND_HAS_NO_THREADS'
elif unwind_has_pthread_lib
  unwind_defines += '-D_UNWIND_LINK_PTHREAD_LIB'
endif

if unwind_enable_arm_wmmx
  unwind_defines += '-D__ARM_WMMX'
endif

if unwind_is_baremetal
  unwind_defines += '-D_LIBUNWIND_IS_BAREMETAL'
endif

if unwind_use_frame_header_cache
  unwind_defines += '-D_LIBUNWIND_USE_FRAME_HEADER_CACHE'
endif

if unwind_remember_heap_alloc
  unwind_defines += '-D_LIBUNWIND_REMEMBER_HEAP_ALLOC'
endif

# link arguments 
unwind_link_args = []

if cpp_com.has_link_argument('-nodefaultlibs')
  unwind_link_args += '-nodefaultlibs'
elif cpp_com.has_link_argument('-nostdlib++')
  unwind_link_args += '-nostdlib++'
endif
  

# collect includes and sources
unwind_inc = include_directories('include')
unwind_src = files([
  'src/libunwind.cpp',
  'src/Unwind-EHABI.cpp',
  'src/Unwind-seh.cpp',
  'src/UnwindLevel1.c',
  'src/UnwindLevel1-gcc-ext.c',
  'src/Unwind-sjlj.c',
  'src/UnwindRegistersRestore.S',
  'src/UnwindRegistersSave.S'
  ])

# collect args
unwind_args = unwind_warning_args + unwind_compile_args + unwind_defines

# ready to do:
# unwind_lib = library('unwind',
#   unwind_src,
#   c_args: unwind_args,
#   cpp_args: unwind_args,
#   include_directories: unwind_inc,
#   link_args: unwind_link_args,
#   )

