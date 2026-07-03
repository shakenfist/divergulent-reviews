# Phase 1 findings: the distinct-patch count

Headline: **≈61574 carried patches → 60642 distinct** (canonical normalisation v1, strip_path,keep_context; dedup ratio 1.02x).

Distinct raw bodies (pre-normalisation): 61193.

## Sensitivity matrix (path in/out x context in/out)

| variant | patch rows | distinct bodies | distinct fingerprints | dedup ratio |
| --- | ---: | ---: | ---: | ---: |
| strip_path,keep_context (canonical) | 61574 | 61193 | 60642 | 1.02x |
| strip_path,drop_context | 61574 | 61193 | 59429 | 1.04x |
| keep_path,keep_context | 61574 | 61193 | 60896 | 1.01x |
| keep_path,drop_context | 61574 | 61193 | 60571 | 1.02x |

## Multiplicity histogram (distinct fingerprints by package recurrence)

| distinct packages | fingerprints |
| --- | ---: |
| 1 | 60154 |
| 2 | 368 |
| 3-5 | 101 |
| 6-10 | 9 |
| 11-50 | 9 |
| 51+ | 1 |

## Top-recurring fingerprints (canonical)

### `939f5f96d45d8f30` — 53 packages, 53 rows

```
---
+++
@@
+/.pc
```

### `e3b0c44298fc1c14` — 30 packages, 32 rows

```

```

### `5a30e4d72a5863e1` — 29 packages, 29 rows

```
---
+++
@@
     format: "umd",
     indent: false,
     extend: true,
-    banner: `// ${meta.homepage} v${meta.version} Copyright ${(new Date).getFullYear()} ${meta.author.name}`,
+    banner: `// ${meta.homepage} v${meta.version} Copyright ${(new Date(process.env.SOURCE_DATE_EPOCH ? (process.env.SOURCE_DATE_EPOCH * 1000) : new Date().getTime())).getFullYear()} ${meta.author.name}`,
     globals: Object.assign({}, ...Object.keys(meta.dependencies || {}).filter(key => /^d3-/.test(key)).map(key => ({[key]: "d3"})))
   },
   plugins: []
```

### `e1a63622212c3bd4` — 28 packages, 28 rows

```
---
+++
@@
-import {terser} from "rollup-plugin-terser";
-import * as meta from "./package.json";
+const { terser } = require("rollup-plugin-terser");
+const meta = require("./package.json");

 const config = {
   input: "src/index.js",
@@
   plugins: []
```

### `9aa633123a941df8` — 28 packages, 28 rows

```
---
+++
@@

 	if test ${IS_PYTHON_SCRIPT} -eq 0 && test -z ${PYTHON};
 	then
-		local PYTHON=`which python 2> /dev/null`;
+		local PYTHON=`which python3 python 2> /dev/null`;

 		if ! test -x ${PYTHON};
 		then
@@
```

### `312c61d44ce3ff04` — 20 packages, 20 rows

```
---
+++
@@
+
+/.pc/
+/_build/
```

### `d0b0a3d344faf7c8` — 17 packages, 17 rows

```
---
+++
@@
+include debian/Makefile.plb
```

### `9c4a61da27d19055` — 15 packages, 15 rows

```
---
+++
@@
+.pc
```

### `222c95d90bf88b5c` — 13 packages, 13 rows

```
---
+++
@@
     # configparser.NoOptionError (if it lacks "VCS="). See the docstring at
     # the top of versioneer.py for instructions on writing your setup.cfg .
     setup_cfg = os.path.join(root, "setup.cfg")
-    parser = configparser.SafeConfigParser()
+    parser = configparser.ConfigParser()
     with open(setup_cfg, "r") as f:
-        parser.readfp(f)
+        parser.read_file(f)
     VCS = parser.get("versioneer", "VCS")  # mandatory
```

### `104ed5878d0e1285` — 13 packages, 13 rows

```
---
+++
@@
      [*linux*],[archive_cmds='$CC -shared $pic_flag $libobjs $deplibs $compiler_flags $wl-soname $wl$soname -o $lib'])])

 dnl check for pkg-config (explained in detail in libosmocore/configure.ac)
-AC_PATH_PROG(PKG_CONFIG_INSTALLED, pkg-config, no)
+AC_PATH_TOOL(PKG_CONFIG_INSTALLED, pkg-config, no)
 if test "x$PKG_CONFIG_INSTALLED" = "xno"; then
         AC_MSG_WARN([You need to install pkg-config])
 fi
```

### `0744c178c63511c6` — 10 packages, 10 rows

```
---
+++
@@
+Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
+
+The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
+
+THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

### `3dc3204a7dc1c871` — 9 packages, 9 rows

```
---
+++
@@


 # Example configuration for intersphinx: refer to the Python standard library.
-intersphinx_mapping = {'http://docs.python.org/': None}
+intersphinx_mapping = {'python': ('http://docs.python.org/', None)}
```

### `ca4a1787d7d4cd3e` — 8 packages, 8 rows

```
---
+++
@@
 from pathlib import Path

 import pytest
-from scspell import Report
-from scspell import SCSPELL_BUILTIN_DICT
-from scspell import spell_check
+try:
+    from scspell import Report
+    from scspell import SCSPELL_BUILTIN_DICT
```

### `11337ae00ffd46ec` — 8 packages, 8 rows

```
---
+++
@@
 AC_SUBST(LIBTOOL_DEPS)

 dnl Check for pkg-config
-AC_PATH_PROG(PKGCONFIG,[pkg-config])
+AC_PATH_TOOL(PKGCONFIG,[pkg-config])

 dnl Support of internationalization (i18n)
 AM_GNU_GETTEXT([external])

```

### `4d2d3b9ea62f062e` — 7 packages, 7 rows

```
---
+++
@@
 # path before files name in the file list and in the header files. If set
 # to NO the shortest path that makes the file name unique will be used.

-FULL_PATH_NAMES        = YES
+FULL_PATH_NAMES        = NO

 # If the FULL_PATH_NAMES tag is set to YES then the STRIP_FROM_PATH tag
 # can be used to strip a user-defined part of the path. Stripping is
```

### `3b8dfcfa9cb748ef` — 7 packages, 7 rows

```
---
+++
@@
+import Distribution.Simple
+main = defaultMain
```

### `d237a7f879abdf85` — 6 packages, 6 rows

```
---
+++
@@
 }

 #[test]
+#[ignore = "currently broken"]
 fn cross_validate_constants_with_c() {
     let mut c_constants: Vec<(String, String)> = Vec::new();

```

### `b9f58a19fc7170c7` — 6 packages, 6 rows

```
---
+++
@@
 AC_SUBST(LIBTOOL_DEPS)

 dnl Check for pkg-config
-AC_PATH_PROG(PKGCONFIG,[pkg-config])
+AC_PATH_TOOL(PKGCONFIG,[pkg-config])

 dnl Support of internationalization (i18n)
 AM_GNU_GETTEXT([external])
```

### `6ef4443481c6987c` — 6 packages, 6 rows

```
---
+++
@@
 EXTRA_DIST =		README.md compat.h config.h.in dict.h log.h \
 			table_stdio.h util.h

-smtpdir =		${prefix}/libexec/smtpd
+smtpdir =		$(pkglibexecdir)

 install-exec-local: $(noinst_PROGRAMS)
 	$(MKDIR_P) $(DESTDIR)$(smtpdir)
---
```

### `ea55626cb3822b8c` — 5 packages, 5 rows

```
---
+++
@@
     "__implicit-crypto-backend-for-tests",
 ]
 default-features = false
-
-[target."cfg(windows)".dev-dependencies.sequoia-openpgp]
-version = "2"
-features = [
-    "crypto-cng",
-    "__implicit-crypto-backend-for-tests",
```

### `db4b0dda85cc17c3` — 5 packages, 5 rows

```
---
+++
@@
+exportPattern("^[[:alpha:]]+")
```

### `b9af804d9770fa78` — 5 packages, 5 rows

```
---
+++
@@
 sub runtests {
   my %arg = @_;

-  $arg{strip_comments} = 1;
   $arg{wrap_in_html} = 1;
   $arg{base_uri} ||= 'http://www.test.com';
   my $minimal = $arg{minimal} || 0;
```

### `797452bb954f39c0` — 5 packages, 5 rows

```
---
+++
@@
 # shortest path that makes the file name unique will be used
 # The default value is: YES.

-FULL_PATH_NAMES        = YES
+FULL_PATH_NAMES        = NO

 # The STRIP_FROM_PATH tag can be used to strip a user-defined part of the path.
 # Stripping is only done if one of the specified strings matches the left-hand
```

### `ce2a7aa20a2f3f3b` — 4 packages, 4 rows

```
---
+++
@@
             <plugin>
                 <groupId>org.apache.felix</groupId>
                 <artifactId>maven-bundle-plugin</artifactId>
+                <extensions>true</extensions>
                 <configuration>
                     <instructions>
                         <Bundle-SymbolicName>${groupId}.${artifactId};singleton=true</Bundle-SymbolicName>
```

### `903fef5d6a756752` — 4 packages, 4 rows

```
---
+++
@@

 enable_verbose_cpan_testing();

-realclean_files('inc');
-
 WriteAll;

 # ---- Workaround for broken module ----
```

## Per-package intra-package dedup (patches != distinct)

| source package | patches | distinct fingerprints |
| --- | ---: | ---: |
| geomview | 8 | 7 |
| libcdk5 | 4 | 3 |
| libtk-img | 7 | 6 |
| libxml2 | 28 | 27 |
| netrik | 7 | 6 |
| node-envinfo | 10 | 9 |
| node-minipass | 16 | 15 |
| oscrypto | 5 | 4 |
| python3-stdlib-extensions | 66 | 25 |
| rust-coreutils | 76 | 74 |
| sawfish-themes | 21 | 20 |
| service-wrapper-java | 7 | 6 |

## Honest accounting

Packages processed: 18821.

| state | packages |
| --- | ---: |
| patched | 18821 |

Fetch failures: 0. Non-quilt skipped: 0.
