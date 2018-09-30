#
# The root build file for OpeniBoot.
#

import SCons

#
# Configuration, change this stuff
#
version="0.3"
# /Configuration

SConscript([
	'scons/ARMEnvironment.SConscript',
	'scons/Git.SConscript',
	])
Import('*')

henv = Environment()
Export('henv')
henv.SConscript(['scons/Doxygen.SConscript'])

# https://scons.org/doc/1.0.1/HTML/scons-user/x2361.html
vars = Variables()
vars.Add('VERSION_PKGSUFFIX', 'A suffix for the version number', '')
vars.Add('VERSION_BUILD', 'A hash to indicate version', GetGitCommit())

env = ARMEnvironment(variables = vars)
env.Append(CPPDEFINES=[
	'OPENIBOOT_VERSION='+version+'${VERSION_PKGSUFFIX}',
	'OPENIBOOT_VERSION_BUILD=${VERSION_BUILD}',
	])
env.Append(CPPFLAGS = ['-Wall'])
Export('env')

def localize(env, ls):
	return [File(f) for f in ls]
env.AddMethod(localize, "Localize")

# Documentation
docs = henv.Doxygen("Doxyfile")
Alias("docs", docs)

# Base Target Sources
base_src = env.Localize([
	'device.c',
	'mtd.c',
	'bdev.c',
	'nand.c',
	'vfl.c',
	'ftl.c',
	'audiohw.c',
	'actions.c',
	'commands.c',
	'framebuffer.c',
	'images.c',
	'malloc.c',
	'nvram.c',
	'openiboot.c',
	'printf.c',
	'scripting.c',
	'sha1.c',
	'stb_image.c',
	'syscfg.c',
	'tasks.c',
	'util.c',
	'aes_wrap.c',
	'nostdlib.c',
	])
Export('base_src')

# Build-Environment Modules
henv.SConscript([
	'images/SConscript',
	'mk8900image/SConscript',
	'scons/Module.SConscript',
	])

# Target Modules
env.SConscript([
	'hfs/SConscript',
	'radio-pmb8876/SConscript',
	'radio-pmb8878/SConscript',
	'radio-xgold618/SConscript',
	'usb-synopsys/SConscript',
	'nor-cfi/SConscript',
	'nor-spi/SConscript',
	'vfl-vfl/SConscript',
	'vfl-vsvfl/SConscript',
	'ftl-yaftl/SConscript',
	'acm/SConscript',
	'menu/SConscript',
	'installer/SConscript',
	'arch-arm/SConscript',
	])
