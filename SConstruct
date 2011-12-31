import os

env = Environment()  # Initialize the environment

#Setup debugging symbols
env.Append( CPPFLAGS=" /RTC1 /MDd /Z7 /TP /errorReport:none " )
env.Append( LINKFLAGS=" /debug " )
env.Append( CPPFLAGS=" /Od " )
env.Append( CPPDEFINES=[ "_DEBUG" ] )

# Useful for printf() debugging.
#print "Version: " + env['MSVS_VERSION'] + " Suffix: " + env['MSVS']['PROJECTSUFFIX']
#for item in sorted(env.Dictionary().items()):
#	print "construction variable = '%s', value = '%s'" % item

helloSrc = ["hello.cpp"]
helloCSrc = ["helloC.c"]
helloIncs = []
helloLocalIncs = []
helloResources = []
helloMisc = []

helloExe = env.Program(target = 'hello', source = helloSrc)
helloCExe = env.Program(target = 'helloC', source = helloCSrc)

defaultTargets = [ helloExe, helloCExe ]

helloVcxproj = env.MSVSProject(
	target = 'hello' + env['MSVSPROJECTSUFFIX'],
	srcs = helloSrc,
#	incs = helloIncs,
#	localincs = helloLocalIncs,
#	resources = helloResources,
#	misc = helloMisc,
	buildtarget = helloExe,
	variant = 'Debug', # This doesn't actually create debug information
	auto_build_solution=0 # otherwise a sln for the vcproj will get created.
)
# TODO: get this working
#env.Clean('hello' + env['MSVSPROJECTSUFFIX'] + '.filters', helloVcxproj) # delete the filters file

helloCVcxproj = env.MSVSProject(
	target = 'helloC' + env['MSVSPROJECTSUFFIX'],
	srcs = helloCSrc,
	buildtarget = helloCExe,
	variant = 'Debug',
	auto_build_solution=0
)
#env.Clean(helloCVcxproj.target + '.filters', helloCVcxproj) # delete the filters file

vcprojTargets = [ helloVcxproj, helloCVcxproj ]

slnTarget = env.MSVSSolution(
	target = 'hello' + env['MSVSSOLUTIONSUFFIX'],
	projects = vcprojTargets,
	variant = 'Debug'
)


if os.sys.platform == "win32":
	defaultTargets += vcprojTargets + [ slnTarget ]

env.Default( defaultTargets )
