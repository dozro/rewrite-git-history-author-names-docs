---
title: Installation
weight: 11
---

# Installation

## building from source

Currently, the only way to install the tool is by building it yourself.

You must have **GNU Make** and **Go** installed on your system.  

Running `make install` will also install the corresponding manpages.

### cloning

```bash
git clone https://codeberg.org/dozrye/git-rewrite-authors-and-resign.git
cd git-rewrite-authors-and-resign
```

Clone the repository to retrieve the full source code and build scripts

### compiling

```bash
make build
```

```makefile
$(COMPILETARGET): precheck
   @echo "compiling"
   go build -o $(COMPILETARGET) $(SRC)

$(COMPILETARGETRESIGN): precheck
   @echo "compiling"
   go build -o $(COMPILETARGETRESIGN) $(SRCRESIGN)

.Phony: user-install build all
build: $(COMPILETARGET) $(COMPILETARGETRESIGN)
```

Compile the project using Make.
This step builds the binaries for both `git-rewrite-authors` and `git-re-sign`.

On the right side you see the shell command and the relevant part in the Makefile.

### installing

```bash
make install
```

```makefile
.Phony: system-install system-man-install installdirs
PREFIX ?= /usr/local
system-install: $(COMPILETARGET) $(COMPILETARGETRESIGN) $(COMPILETARGETRESIGN) system-man-install installdirs
   install -m 555 $(COMPILETARGET) $(PREFIX)/bin/$(COMPILEDNAME)
   install -m 555 $(COMPILETARGETRESIGN) $(PREFIX)/bin/$(COMPILENAMERESIGN)
.Phony: normal-install install install-strip
normal-install: system-install
install: system-install
```

Install the built binaries and manpages into your system (default prefix: `/usr/local`).
This requires root privileges unless you change the installation prefix.
