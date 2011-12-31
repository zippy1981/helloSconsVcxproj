import os

env = Environment()  # Initialize the environment

# Uncomment the following to debug.
#print "Version: " + env['MSVS_VERSION'] + " Suffix: " + env['MSVS']['PROJECTSUFFIX']
#for item in sorted(env.Dictionary().items()):
#             print "construction variable = '%s', value = '%s'" % item

helloSrc = ["hello.cpp"]
helloCSrc = ["helloC.c"]
helloIncs = []
helloLocalIncs = []
helloResources = []
#helloMisc = [ 'SConstruct' ]
helloMisc = []

helloExe = env.Program(target = 'hello', source = helloSrc)
helloCExe = env.Program(target = 'helloC', source = helloCSrc)

helloVcxproj = env.MSVSProject(target = 'hello' + env['MSVSPROJECTSUFFIX'],
                srcs = helloSrc,
#                incs = helloIncs,
#                localincs = helloLocalIncs,
#                resources = helloResources,
#                misc = helloMisc,
                buildtarget = helloExe,
                variant = 'Release'
)

helloCVcxproj = env.MSVSProject(target = 'helloC' + env['MSVSPROJECTSUFFIX'],
                srcs = helloCSrc,
                buildtarget = helloCExe,
                variant = 'Release'
)

defaultTargets = [ helloExe, helloCExe ]

if os.sys.platform == "win32":
    defaultTargets += [ helloVcxproj, helloCVcxproj ]

env.Default( defaultTargets )