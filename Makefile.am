SUBDIRS = src 
LISP_PACKAGES = pdf-history.el pdf-info.el pdf-isearch.el		\
 pdf-links.el pdf-misc.el pdf-occur.el pdf-outline.el pdf-tools.el	\
 pdf-util.el pdf-render.el pdf-annot.el pdf-sync.el			\
 tablist.el tablist-filter.el
LISP_FILES = $(addprefix lisp/,$(LISP_PACKAGES))
EPKG_FILES = $(LISP_FILES) src/epdfinfo README.org images
EPKG_NAME = $(PACKAGE_NAME)-$(PACKAGE_VERSION)
EPKG_TAR_NAME = $(EPKG_NAME).tar
README_FILE = lisp/pdf-tools.el

EXTRA_DIST = $(LISP_FILES)
CLEANFILES = $(EPKG_TAR_NAME)
DISTCLEANFILES = configure depcomp install-sh missing src/Makefile.in src/config.h.in
TESTS_ENVIRONMENT = $(EMACS) -Q $(EPKG_TAR_NAME) -batch -l
TESTS = tests/install-basic.el

all-local: $(EPKG_TAR_NAME)

distclean-local:
	rm -rf -- aclocal.m4 autom4te.cache

$(EPKG_TAR_NAME): $(LISP_FILES)
	rm -fr -- $(EPKG_NAME)
	mkdir $(EPKG_NAME)
	echo "(define-package \"$(PACKAGE_NAME)\" \"$(PACKAGE_VERSION)\" \
	 	\"Support library for PDF documents.\")"  \
		> $(EPKG_NAME)/$(PACKAGE_NAME)-pkg.el
	cp -r $(EPKG_FILES) $(EPKG_NAME)/
	tar cf $(EPKG_TAR_NAME) $(EPKG_NAME)
	rm -r -- $(EPKG_NAME)

install: all
	if ! which -- "$(EMACS)"; then \
		echo "No emacs executable found, you have to set EMACS"; \
		false; \
	fi
	$(EMACS) -Q --batch --eval "(package-install-file \
	 	\"$$PWD/$(EPKG_TAR_NAME)\")"


