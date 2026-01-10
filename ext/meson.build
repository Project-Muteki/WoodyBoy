wbc_engine = get_option('wbc_engine')

ext_minigb_apu_include = include_directories('Peanut-GB/examples/sdl2/minigb_apu')
ext_peanut_gb_include = include_directories('Peanut-GB')
ext_walnut_cgb_include = include_directories('Walnut-CGB')
ext_peanut_gbc_include = include_directories('Peanut-GBC')
ext_include = [ext_minigb_apu_include, ext_peanut_gb_include]
ext_cgb_include = [ext_minigb_apu_include]

if wbc_engine == 'walnut'
  ext_cgb_include += ext_walnut_cgb_include
else
  ext_cgb_include += ext_peanut_gbc_include
endif

ext_lib = static_library('ext',
  'Peanut-GB/examples/sdl2/minigb_apu/minigb_apu.c',
  include_directories : ext_include,
  pic : false,
  c_args: ['-DMINIGB_APU_AUDIO_FORMAT_S16SYS'],
)

ext_cgb_lib = static_library('ext_gbc',
  'Peanut-GB/examples/sdl2/minigb_apu/minigb_apu.c',
  include_directories : ext_cgb_include,
  pic : false,
  c_args: ['-DMINIGB_APU_AUDIO_FORMAT_S16SYS'],
)
