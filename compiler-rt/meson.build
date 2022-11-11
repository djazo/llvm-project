project('compiler-rt',
  ['c','cpp'],
  version: '16.x',
  meson_version: '>=0.60.0',
  license: 'Apache-2.0',
  default_options: [
    'default_library=static',
    'prefer_static=true',
    'optimization=s',
    'debug=false',
    'cpp_std=c++20',
    'c_std=c11',
    'werror=false',
    'warning_level=3'
    ])

c_com = meson.get_compiler('c')
cpp_com = meson.get_compiler('cpp')

if target_machine.system() == 'windows' or target_machine.system() == 'cygwin'
  tgt_win = true
else
  tgt_win = false
endif

if target_machine.system() == 'darwin'
  tgt_apple = true
else
  tgt_apple = false
endif

if target_machine.system() == 'android'
  tgt_android = true
else
  tgt_android = false
endif

if c_com.get_id() == 'msvc'
  tgt_msvc = true
else
  tgt_msvc = false
endif

c_rt_build_builtins = get_option('compiler_rt_build_builtins')
c_rt_baremetal_build = get_option('compiler_rt_baremetal_build')
c_rt_build_crt = get_option('compiler_rt_build_crt')
c_rt_build_gwp_asan = get_option('compiler_rt_build_gwp_asan')
c_rt_build_libfuzzer = get_option('compiler_rt_build_libfuzzer')
c_rt_build_memprof = get_option('compiler_rt_build_memprof')
c_rt_build_orc = get_option('compiler_rt_build_orc')
c_rt_build_profile = get_option('compiler_rt_build_profile')
c_rt_build_sanitizers = get_option('compiler_rt_build_sanitizers')
c_rt_build_standalone_libatomic = get_option('compiler_rt_build_standalone_libatomic')
c_rt_build_xray = get_option('compiler_rt_build_xray')
c_rt_build_xray_no_preinit = get_option('compiler_rt_build_xray_no_preinit')
c_rt_builtins_enable_pic = get_option('compiler_rt_builtins_enable_pic')
c_rt_builtins_hide_symbols = get_option('compiler_rt_builtins_hide_symbols')
c_rt_crt_use_eh_frame_registry = get_option('compiler_rt_crt_use_eh_frame_registry')
c_rt_enable_cet = get_option('compiler_rt_enable_cet')
c_rt_exclude_atomic_builtin = get_option('compiler_rt_exclude_atomic_builtin')
c_rt_sanitizers_to_build = get_option('compiler_rt_sanitizers_to_build')

if c_rt_build_builtins
  subdir('lib/builtin')
  c_rt_builtins_proj = subproject('builtins')
  c_rt_builtins_dep = c_rt_builtins_proj.get_value('c_rt_builtins_dep')
endif

# rest of these aren't yet supported, but ready for later time..
if c_rt_build_crt
  subdir('lib/crt')
endif

if c_rt_build_sanitizers or c_rt_build_xray or c_rt_build_memprof
  subdir('lib/sanitizer_common')
endif

if c_rt_build_sanitizers or c_rt_build_memprof
  subdir('lib/interception')
endif

if c_rt_build_sanitizers
  subdir('lib/stats')
  subdir('lib/lsan')
  subdir('lib/ubsan')

  c_rt_all_sanitizers = ['asan','dfsan','msan','hwasan','tsan',
      'safestack','cfi','scudo','ubsan_minimal','gwp_asan']

  if c_rt_sanitizers_to_build.contains('all')
    c_rt_sanitizers_to_build = c_rt_all_sanitizers
  endif

  foreach s : c_rt_sanitizers_to_build
    if s == 'asan'
      subdir('lib/asan')
    elif s = 'dfsan'
      subdir('lib/dfsan')
    elif s = 'msan'
      subdir('lib/msan')
    elif s = 'hwasan'
      subdir('lib/hwasan')
    elif s = 'tsan'
      subdir('lib/tsan')
    elif s = 'safestack'
      subdir('lib/safestack')
    elif s = 'cfi'
      subdir('lib/cfi')
    elif s = 'scudo'
      subdir('lib/scudo')
    elif s = 'ubsan_minimal'
      subdir('lib/ubsan_minimal')
    elif s = 'gwp_asan'
      subdir('lib/gwp_asan')
    else
      message('Sanitizer not found: ', s, ', skipping.')
    endif
  endforeach
endif


if c_rt_build_profile
  subdir('lib/profile')
endif

if c_rt_build_xray
  subdir('lib/xray')
endif

if c_rt_build_libfuzzer
  subdir('lib/fuzzer')
endif

if c_rt_build_memprof
  subdir('lib/memprof')
endif

if c_rt_build_orc
  subdir('lib/orc')
endif
