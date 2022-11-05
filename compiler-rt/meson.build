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
  c_rt_builtins_proj = subproject('builtins')
  c_rt_builtins_dep = c_rt_builtins_proj.get_value('c_rt_builtins_dep')
endif

# rest of these aren't yet supported, but ready for later time..
if c_rt_build_crt
  c_rt_crt_proj = subproject('crt')
  c_rt_crt_dep = c_rt_crt_proj.get_value('c_rt_crt_dep')
endif

if c_rt_build_sanitizers or c_rt_build_xray or c_rt_build_memprof
  c_rt_sanitizer_common_proj = subproject('sanitizer_common')
  c_rt_sanitizer_common_dep = c_rt_sanitizer_common_proj.get_value('c_rt_sanitizer_common_dep')
endif

if c_rt_build_sanitizers or c_rt_build_memprof
  c_rt_interception_proj = subproject('interception')
  c_rt
endif

if c_rt_build_sanitizers
  c_rt_stats_proj = subproject('stats')
  c_rt_stats_dep = c_rt_stats_proj.get_value('c_rt_stats_dep')
  c_rt_lsan_proj = subproject('lsan')
  c_rt_lsan_dep = c_rt_lsan_proj.get_value('c_rt_lsan_dep')
  c_rt_ubsan_proj = subproject('ubsan')
  c_rt_ubsan_dep = c_rt_ubsan_proj.get_value('c_rt_ubsan_dep')

  c_rt_all_sanitizers = ['asan','dfsan','msan','hwasan','tsan',
      'safestack','cfi','scudo','ubsan_minimal','gwp_asan']

  if c_rt_sanitizers_to_build.contains('all')
    c_rt_sanitizers_to_build = c_rt_all_sanitizers
  endif

  foreach s : c_rt_sanitizers_to_build
    if s == 'asan'
      c_rt_sanitizer_asan_proj = subproject('asan')
      c_rt_sanitizer_asan_dep = c_rt_sanitizer_asan_proj.get_value('c_rt_sanitizer_asan_dep')
    elif s = 'dfsan'
      c_rt_sanitizer_dfsan_proj = subproject('dfsan')
      c_rt_sanitizer_dfsan_dep = c_rt_sanitizer_dfsan_proj.get_value('c_rt_sanitizer_dfsan_dep')
    elif s = 'msan'
      c_rt_sanitizer_msan_proj = subproject('msan')
      c_rt_sanitizer_msan_dep = c_rt_sanitizer_msan_proj.get_value('c_rt_sanitizer_msan_dep')
    elif s = 'hwasan'
      c_rt_sanitizer_hwasan_proj = subproject('hwasan')
      c_rt_sanitizer_hwasan_dep = c_rt_sanitizer_hwasan_proj.get_value('c_rt_sanitizer_hwasan_dep')
    elif s = 'tsan'
      c_rt_sanitizer_tsan_proj = subproject('tsan')
      c_rt_sanitizer_tsan_dep = c_rt_sanitizer_tsan_proj.get_value('c_rt_sanitizer_tsan_dep')
    elif s = 'safestack'
      c_rt_sanitizer_safestack_proj = subproject('safestack')
      c_rt_sanitizer_safestack_dep = c_rt_sanitizer_safestack_proj.get_value('c_rt_sanitizer_safestack_dep')
    elif s = 'cfi'
      c_rt_sanitizer_cfi_proj = subproject('cfi')
      c_rt_sanitizer_cfi_dep = c_rt_sanitizer_cfi_proj.get_value('c_rt_sanitizer_cfi_dep')
    elif s = 'scudo'
      c_rt_sanitizer_scudo_proj = subproject('scudo')
      c_rt_sanitizer_scudo_dep = c_rt_sanitizer_scudo_proj.get_value('c_rt_sanitizer_scudo_dep')
    elif s = 'ubsan_minimal'
      c_rt_sanitizer_ubsan_minimal_proj = subproject('ubsan_minimal')
      c_rt_sanitizer_ubsan_minimal_dep = c_rt_sanitizer_ubsan_minimal_proj.get_value('c_rt_sanitizer_ubsan_minimal_dep')
    elif s = 'gwp_asan'
      c_rt_sanitizer_gwp_asan_proj = subproject('gwp_asan')
      c_rt_sanitizer_gwp_asan_dep = c_rt_sanitizer_gwp_asan_proj.get_value('c_rt_sanitizer_gwp_asan_dep')
    else
      message('Sanitizer not found: ', s, ', skipping.')
    endif
  endforeach
endif


if c_rt_build_profile
  c_rt_profile_proj = subproject('profile')
  c_rt_profile_dep = c_rt_profile_proj.get_value('c_rt_profile_dep')
endif

if c_rt_build_xray
  c_rt_xray_proj = subproject('xray')
  c_rt_xray_dep = c_rt_xray_proj.get_value('c_rt_xray_dep')
endif

if c_rt_build_libfuzzer
  c_rt_fuzzer_proj = subproject('fuzzer')
  c_rt_fuzzer_dep = c_rt_fuzzer_proj.get_value('c_rt_fuzzer_dep')
endif

if c_rt_build_memprof
  c_rt_memprof_proj = subproject('memprof')
  c_rt_memprof_dep = c_rt_memprof_proj.get_value('c_rt_memprof_dep')
endif

if c_rt_build_orc
  c_rt_orc_proj = subproject('orc')
  c_rt_orc_dep = c_rt_orc_proj.get_value('c_rt_orc_dep')
endif
