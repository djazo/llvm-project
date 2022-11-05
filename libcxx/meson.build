# get options

cxx_enable_assertions = get_option('libcxx_enable_assertions')
cxx_enable_shared = get_option('libcxx_enable_shared')
cxx_enable_static = get_option('libcxx_enable_static')
cxx_enable_filesystem = get_option('libcxx_enable_filesystem')
cxx_enable_parallel_algorithms = get_option('libcxx_enable_parallel_algorithms')
cxx_enable_debug_mode = get_option('libcxx_enable_debug_mode')
cxx_enable_random_device = get_option('libcxx_enable_random_device')
cxx_enable_localization = get_option('libcxx_enable_localization')
cxx_enable_unicode = get_option('libcxx_enable_unicode')
cxx_enable_wide_characters = get_option('libcxx_enable_wide_characters')
cxx_enable_vendor_availability_annotations = get_option('libcxx_enable_vendor_availability_annotations')
cxx_abi_unstable = get_option('libcxx_abi_unstable')
cxx_use_compiler_rt = get_option('libcxx_use_compiler_rt')
cxx_enable_new_delete_definitions = get_option('libcxx_enable_new_delete_definitions')
cxx_use_llvm_unwinder = get_option('libcxx_use_llvm_unwinder')
cxx_enable_exceptions = get_option('libcxx_enable_exceptions')
cxx_enable_rtti = get_option('libcxx_enable_rtti')
cxx_enable_threads = get_option('libcxx_enable_threads')
cxx_enable_monotonic_clock = get_option('libcxx_enable_monotonic_clock')
cxx_has_musl_libc = get_option('libcxx_has_musl_libc')
cxx_has_pthread_api = get_option('libcxx_has_pthread_api')
cxx_has_external_thread_api = get_option('libcxx_has_external_thread_api')
cxx_build_external_thread_library = get_option('libcxx_build_external_thread_library')
cxx_enable_pedantic = get_option('libcxx_enable_pedantic')
cxx_enable_werror = get_option('libcxx_enable_werror')
cxx_disable_macro_conflict_warnings = get_option('libcxx_disable_macro_conflict_warnings')
cxx_hermetic_static_library = get_option('libcxx_hermetic_static_library')

# treat warnings

cxx_wanted_warning_args = [
  '-Wall',
  '-Wextra',
  '-W',
  '-Wwrite-strings',
  '-Wno-unused-parameter',
  '-Wno-long-long',
  '-Werror=return-type',
  '-Wextra-semi',
  '-Wundef',
  '-Wformat-nonliteral',
  '-Wno-user-defined-literals',
  '-Wno-covered-switch-default',
  '-Wno-suggest-override',
  ]

if cxx_enable_werror
  cxx_wanted_warning_args += [
    '-Werror',
    '-WX',
    ]
else
  cxx_wanted_warning_args += [
    '-Wno-error',
    '-WX-',
    ]
endif

cxx_warning_args = cpp_com.get_supported_arguments(
  cxx_wanted_warning_args,
  checked: 'warn'
  )

# arguments
cxx_wanted_args = []

if cxx_enable_pedantic
  cxx_wanted_args += '-pedantic'
endif

if cxx_enable_exceptions
  cxx_wanted_args += '-EHsc'
else
  cxx_wanted_args += [
    '-EHs-',
    '-EHa-',
    '-fno-exceptions'
    ]
endif

if not cxx_enable_rtti
  cxx_wanted_args += [
    '-GR-',
    '-fno-rtti'
    ]
endif

if cpp_com.has_link_argument('-nodefaultlibs')
  cxx_wanted_args += '-nodefaultlibs'
elif cpp_com.has_link_argument('-nostdlib++')
  cxx_wanted_args += '-nostdlib++'
endif


