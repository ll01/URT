import platform
env = Environment()

conan = SConscript('SConscript_conan')
env.MergeFlags(conan['conan'])


env['SYSTEM'] = platform.system().lower()
# ADD -O https://www.rapidtables.com/code/linux/gcc/gcc-o.html
CCFLAGS=[]
if env['SYSTEM'] in ['linux', 'darwin']:
    CCFLAGS=["-DUSE_EIGEN -fopenmp"]
if env['SYSTEM'] == 'windows':
    CCFLAGS=["/openmp", "/DUSE_EIGEN"]
# for  key, value in env.items():
#     print(key, ':', value)
SharedLibrary(
    'lib/urt', Glob('src/*.cpp'), CPPPATH=env['CPPPATH'], CCFLAGS=CCFLAGS)