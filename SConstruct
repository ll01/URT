env = Environment()

conan = SConscript('SConscript_conan')
env.MergeFlags(conan['conan'])

# ADD -O https://www.rapidtables.com/code/linux/gcc/gcc-o.html
CCFLAGS = []

if env['CC'] == 'cl':
    CCFLAGS = ["/openmp", "/DUSE_EIGEN"]
else:
    # assuming useing gcc
    CCFLAGS = ["-DUSE_EIGEN -fopenmp -Ofast"]
Library(
    'urt', Glob('src/*.cpp'), CPPPATH=env['CPPPATH'], CCFLAGS=CCFLAGS)

for file in Glob('examples/*.cpp'):
    Program(file, CPPPATH=env['CPPPATH'],
            CCFLAGS=CCFLAGS, LIBS=['urt'], LIBPATH='.')
