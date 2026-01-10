c = meson.get_compiler('c')
mutekix_lib = c.find_library('mutekix', required : true)
wbc_engine = get_option('wbc_engine')

wb = executable('wb',
  'main.c',
  include_directories : ext_include,
  name_suffix: 'elf',
  dependencies: mutekix_lib,
  link_with : ext_lib,
  install : false,
  c_args: ['-DMINIGB_APU_AUDIO_FORMAT_S16SYS', '-DWB_ENGINE_PEANUT'],
  link_args: ['-Wl,--gc-sections'])

if wbc_engine == 'peanut'
  wbc = executable('wbc',
    'main.c',
    include_directories : ext_cgb_include,
    name_suffix: 'elf',
    dependencies: mutekix_lib,
    link_with : ext_cgb_lib,
    install : false,
    c_args: ['-DPEANUT_FULL_GBC_SUPPORT=1', '-DMINIGB_APU_AUDIO_FORMAT_S16SYS', '-DWB_ENGINE_PEANUT'],
    link_args: ['-Wl,--gc-sections'])
elif wbc_engine == 'walnut'
  wbc = executable('wbc',
    'main.c',
    include_directories : ext_cgb_include,
    name_suffix: 'elf',
    dependencies: mutekix_lib,
    link_with : ext_cgb_lib,
    install : false,
    c_args: ['-DPEANUT_FULL_GBC_SUPPORT=1', '-DMINIGB_APU_AUDIO_FORMAT_S16SYS', '-DWB_ENGINE_WALNUT'],
    link_args: ['-Wl,--gc-sections'])
else
  error('Unknown wbc_engine value. Please report this as a bug.')
endif

if romtool.found() and elf2bestape.found()
  romspec = custom_target('romspec',
    input: 'romspec.toml',
    output: 'romspec.rom',
    command: [romtool, 'build', '@INPUT@', '-o', '@OUTPUT@'],
    build_by_default: true)

  romspec_cgb = custom_target('romspec-cgb',
    input: 'romspec.cgb.toml',
    output: 'romspec.cgb.rom',
    command: [romtool, 'build', '@INPUT@', '-o', '@OUTPUT@'],
    build_by_default: true)

  custom_target('wb-bestape',
    input: [wb, romspec],
    output: 'wb.exe',
    command: [elf2bestape, '-o', '@OUTPUT@', '-r', '@INPUT1@', '@INPUT0@'],
    build_by_default: true)

  custom_target('wbc-bestape',
    input: [wbc, romspec_cgb],
    output: 'wbc.exe',
    command: [elf2bestape, '-o', '@OUTPUT@', '-r', '@INPUT1@', '@INPUT0@'],
    build_by_default: true)
endif
