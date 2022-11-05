project('LLVM project',
        ['c','cpp'],
       version: '16.x',
       meson_version: '>=0.60.0',
       license: 'Apache-2.0',
       default_options: [
         'default_library=static',
         'prefer_static=true',
         'optimization=s',
         'cpp_std=c++20',
         'warning_level=3'
       ]
       )

c_com = meson.get_compiler('c')
cpp_com = meson.get_compiler('cpp')

compiler_rt_proj = subproject('compiler-rt')
compiler_rt_dep = compiler_rt_proj.get_variable('compiler_rt_dep')

unwind_proj = subproject('libunwind')
unwind_dep = unwind_proj.get_variable('unwind_dep')

cxxabi_proj = subproject('libcxxabi',
        default_options: [
                'libcxxabi_cxx_include=' + meson.project_source_root() / 'libcxx/include'
                ])
cxxabi_dep = cxxabi_proj.get_variable('cxxabi_dep')

cxx_proj = subproject('libcxx',
        default_options: [
                'libcxx_cxxabi_include=' + meson.project_source_root() / 'libcxxabi/include'
                ])
cxx_dep = cxx_proj.get_variable('cxx_dep')
