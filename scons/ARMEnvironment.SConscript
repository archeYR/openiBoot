#
# Setup our cross-compilation environment.
#

import os

def ARMEnvironment(*a, **kw):
	env = Environment(tools=['gas', 'gcc', 'gnulink', 'ar'], ENV=os.environ, *a, **kw)
	plat_flags = ['-mlittle-endian', '-mfpu=vfp', '-marm', '-fPIC']
	env.Append(CPPPATH = ['#includes'])
	env.Append(CPPFLAGS = plat_flags+['-nostdlib'])
	env.Append(ASPPFLAGS = ['-xassembler-with-cpp'])
	env.Append(LINKFLAGS = plat_flags+['-nostdlib', '-Tlinkscript.x', '-static', '-Wl,--omagic'])
	# omagic above is to make text writable, though I don't know why a newer toolchain necessitates that to successfully link... -- Joey Hewitt
	env.Append(LIBS = ['gcc'])

	env['PROGSUFFIX'] = ''

	if not env.has_key("CROSS"):
		if env['ENV'].has_key("CROSS"):
			env['CROSS'] = env['ENV']['CROSS']
		else:
			env["CROSS"] = 'arm-elf-'

	env["CC"] = env["CROSS"] + 'gcc'
	env["OBJCOPY"] = env["CROSS"] + 'objcopy'
	env["AR"] = env["CROSS"] + 'ar'

	return env
Export('ARMEnvironment')
