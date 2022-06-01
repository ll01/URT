env = Environment()
conan = SConscript('SConscript_conan')
env.MergeFlags(conan['conan'])

# ADD -O https://www.rapidtables.com/code/linux/gcc/gcc-o.html
CCFLAGS = []

if env['CC'] == 'cl':
    CCFLAGS = ["/openmp", "/DUSE_EIGEN"]
else:
    # assuming using gcc
    CCFLAGS = ["-DUSE_EIGEN -fopenmp -Ofast"]

if ARGUMENTS.get('debug', 0):
    if env['CC'] == 'cl':
        CCFLAGS.extend(['/Zi', '/EHsc', '/DEBUG'])
        symbolsSavePath = ARGUMENTS.get('symbols', '')
        if symbolsSavePath:
            CCFLAGS.append(f'/Fd{symbolsSavePath}/')
    else:
        CCFLAGS.append('-g')

Library(
    'urt', Glob('src/*.cpp'), CPPPATH=env['CPPPATH'], CCFLAGS=CCFLAGS)


def compile_program(path):
    Program(
        path, CPPPATH=env['CPPPATH'], CCFLAGS=CCFLAGS, LIBS=['urt'],
        LIBPATH='.', LINKFLAGS=['/Zi', '/EHsc', '/DEBUG'])


target = ARGUMENTS.get('target')
if target:
    compile_program(target)
else:
    examples = Glob('examples/*.cpp')
    for path in examples:
        compile_program(path)
