import platform
env = Environment()
conan = SConscript('SConscript_conan')
env.MergeFlags(conan['conan'])
env['SYSTEM'] = platform.system().lower()
# ADD -O https://www.rapidtables.com/code/linux/gcc/gcc-o.html


if env['CC'] == 'cl':
    env.Append(CCFLAGS = ["/openmp", "/DUSE_EIGEN"])
else:
    # assuming using gcc or clang 
     env.Append(CCFLAGS = ['-DUSE_EIGEN', '-Ofast'])

if 'linux' in env['SYSTEM']:
    env['CCFLAGS'].Append('-fopenmp')
elif 'darwin' in env['SYSTEM']:
    print("working on getting openmp working on macos")

if ARGUMENTS.get('debug', 0):
    if env['CC'] == 'cl':
        env['CCFLAGS'].extend(['/Zi', '/EHsc', '/DEBUG'])
        symbolsSavePath = ARGUMENTS.get('symbols', '')
        env.append(LINKFLAGS = ['/DEBUG'])
        if symbolsSavePath:
            env['CCFLAGS'].append(f'/Fd{symbolsSavePath}/')
    else:
        env['CCFLAGS'].append('-g')

Library(
    'urt', Glob('src/*.cpp'), CPPPATH=env['CPPPATH'], CCFLAGS=env['CCFLAGS'])


def compile_program(path):
    Program(
        path, CPPPATH=env['CPPPATH'], CCFLAGS=env['CCFLAGS'], LIBS=['urt'],
        LIBPATH='.', LINKFLAGS=env['LINKFLAGS'])


target = ARGUMENTS.get('target')
if target:
    compile_program(target)
else:
    examples = Glob('examples/*.cpp')
    for path in examples:
        compile_program(path)
