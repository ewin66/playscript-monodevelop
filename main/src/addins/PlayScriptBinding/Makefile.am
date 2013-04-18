SUBDIRS = . Autotools AspNet

include $(top_srcdir)/xbuild.include

PARSE = parse.exe

TESTFILES = 

TESTDLLS = \
	$(NUNIT_LIBS)

TESTASSEMBLY = $(top_builddir)/build/bin/CSharpBinding.Test.dll

$(TESTASSEMBLY) : $(build_test_sources) $(build_resources)
	$(CSC) $(CSC_FLAGS) -debug "-define:GMCS_SOURCE;NET_2_0;MS_COMPATIBLE;FULL_AST;BOOTSTRAP_BASIC" -unsafe  -codepage:utf8 -out:$@ -target:library $(DLLS) $(TESTDLLS) $(REFS) /r:$(ASSEMBLY) \
	$(monodoc_libflags) $(build_resources:%=/resource:%) $(build_test_sources)

parse: $(PARSE)

$(PARSE): parse.cs all
	$(CSC) -out:$@ parse.cs $(REFS) -r:$(ASSEMBLY)

run-parse-test: $(PARSE)
	MONO_PATH=$(top_builddir)/build/AddIns/BackendBindings/:$(top_builddir)/build/bin/ mono $(PARSE) .

CLEANFILES = $(PARSE) $(PARSE).mdb
