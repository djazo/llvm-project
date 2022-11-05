builtins_lib = library('compiler-rt',
  builtins_src,
  c_args: builtins_args,
  cpp_args: builtins_args,
  pic: true)

bultins_dep = declare_dependency(
  link_with: builtins_lib
  )

unwind_lib = library('unwind',
  unwind_src,
  c_args: unwind_args,
  cpp_args: unwind_args
  )

unwind_dep = declare_dependency(
  link_with: unwind_lib
  )

cxxabi_lib = library('cxxabi',
  cxxabi_src,
  c_args: cxxabi_args,
  cpp_args: cxxabi_args,
  pic: true,
  dependencies: [ unwind_dep, builtins_dep ]
  )

cxx_lib = library('cxx',
  cxx_src,
  c_args: cxx_args,
  cpp_args: cxx_args
  pic: true,
  link_with: cxxabi_lib
  )
