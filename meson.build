project(
    'libcanlib',
    'c',
    'cpp',
    version : '3.6.1',
    default_options : [
        'c_std=gnu99',
        'cpp_std=gnu++17',
        'board=TOOL1RR'
    ]
)

includes = [
    'src/'
]

sources = [
    'src/CanMessageBuffer.cpp',
    'src/CanMessageFormats.cpp',
    'src/CanMessageGenericParser.cpp',
    'src/CanSettings.cpp',
    'src/RRF3Common.cpp'
]

if get_option('board') == 'TOOL1RR'
    includes += []
    sources += []

    add_project_arguments(
        '-D__SAME51N19A__',
        '-DRTOS',
        '-c',
        '-mcpu=cortex-m4',
        '-mthumb',
        '-fno-math-errno',
        '-mfpu=fpv4-sp-d16',
        '-mfloat-abi=hard',
        '-mfp16-format=ieee',
        '-ffunction-sections',
        '-fdata-sections',
        '-nostdlib',
        '-Wundef',
        '-Wdouble-promotion',
        '-Werror=return-type',
        '-Werror=implicit',
        '-fsingle-precision-constant',
        '-Wa,-ahl=$*.s',
        language : 'c'
    )

    add_project_arguments(
        '-D__SAME51N19A__',
        '-DRTOS',
        '-c',
        '-mcpu=cortex-m4',
        '-mthumb',
        '-fno-math-errno',
        '-mfpu=fpv4-sp-d16',
        '-mfloat-abi=hard',
        '-mfp16-format=ieee',
        '-ffunction-sections',
        '-fdata-sections',
        '-fno-threadsafe-statics',
        '-fno-rtti',
        '-fno-exceptions',
        '-nostdlib',
        '-Wundef',
        '-Wdouble-promotion',
        '-Werror=return-type',
        '-fsingle-precision-constant',
        '-Wa,-ahl=$*.s',
        '-fstack-usage',
        '-fdump-rtl-expand',
        language : 'cpp'
    )
endif

libfreertos = subproject('libfreertos')
libfreertos_dep = libfreertos.get_variable('libfreertos_dep')

librrflibraries = subproject('librrflibraries')
librrflibraries_dep = librrflibraries.get_variable('librrflibraries_dep')

libcanlib = static_library(
    'canlib',
    sources,
    include_directories : include_directories(includes),
    dependencies : [
        libfreertos_dep,
        librrflibraries_dep
    ]
)

libcanlib_dep = declare_dependency(
    include_directories : include_directories(includes),
    link_with : libcanlib
)
