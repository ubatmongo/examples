# Query Quickstart

<!-- TOC -->

- [Query Quickstart](#query-quickstart)
    - [Ref](#ref)
    - [Build](#build)
    - [Run](#run)
    - [Query](#query)
        - [explore targets](#explore-targets)
            - [rules of a package](#rules-of-a-package)
            - [dependencies of a project](#dependencies-of-a-project)
            - [graph](#graph)
            - [reverse dependency](#reverse-dependency)
            - [attribute based search](#attribute-based-search)

<!-- /TOC -->


## Ref

[Query Quickstart](https://bazel.build/versions/7.2.0/query/quickstart?hl=en)


## Build

```bash
bazel build //:runner

INFO: Analyzed target //:runner (84 packages loaded, 3924 targets configured).
INFO: Found 1 target...
Target //:runner up-to-date:
  bazel-bin/runner
  bazel-bin/runner.jar
INFO: Elapsed time: 3.494s, Critical Path: 0.10s
INFO: 1 process: 24 action cache hit, 1 internal.
INFO: Build completed successfully, 1 total action

```


## Run

```bash
bazel-bin/runner
-------------- MENU ---------------
Pizza - Cheesy Delicious Goodness
Macaroni & Cheese - Kid-approved Dinner
-----------------------------------
```

## Query

### explore targets


#### rules of a package

```bash

$ bazel query //src/main/java/com/example/dishes/...
---
//src/main/java/com/example/dishes:macAndCheese
//src/main/java/com/example/dishes:pizza


$ bazel query //src/main/java/com/example/dishes/
---
ERROR: invalid package name 'src/main/java/com/example/dishes/': package names may not end with '/' (perhaps you meant ":"?)
FAIL: 7


$ bazel query //src/main/java/com/example/dishes
---
ERROR: no such target '//src/main/java/com/example/dishes:dishes': target 'dishes' not declared in package 'src/main/java/com/example/dishes' defined by /Users/udita.bose/spaces/bazelbuild/examples/query-quickstart/src/main/java/com/example/dishes/BUILD
FAIL: 7


$ bazel query //src/main/java/com/example/dishes:dishes
---
ERROR: no such target '//src/main/java/com/example/dishes:dishes': target 'dishes' not declared in package 'src/main/java/com/example/dishes' defined by /Users/udita.bose/spaces/bazelbuild/examples/query-quickstart/src/main/java/com/example/dishes/BUILD
FAIL: 7


$ bazel query //src/main/java/com/example/dishes:all
---
//src/main/java/com/example/dishes:macAndCheese
//src/main/java/com/example/dishes:pizza
```

#### dependencies of a project

```bash

bazel query "deps(//:runner)"
---

//:runner
//:src/main/java/com/example/Runner.java
//src/main/java/com/example/dishes:MacAndCheese.java
//src/main/java/com/example/dishes:Pizza.java
//src/main/java/com/example/dishes:macAndCheese
//src/main/java/com/example/dishes:pizza
//src/main/java/com/example/ingredients:Cheese.java
//src/main/java/com/example/ingredients:Dough.java
//src/main/java/com/example/ingredients:Macaroni.java
//src/main/java/com/example/ingredients:Tomato.java
//src/main/java/com/example/ingredients:cheese
//src/main/java/com/example/ingredients:dough
//src/main/java/com/example/ingredients:macaroni
//src/main/java/com/example/ingredients:tomato
//src/main/java/com/example/restaurant:Cafe.java
//src/main/java/com/example/restaurant:Chef.java
//src/main/java/com/example/restaurant:cafe
//src/main/java/com/example/restaurant:chef
@bazel_tools//src/conditions:host_windows
@bazel_tools//src/conditions:host_windows_arm64_constraint
@bazel_tools//src/conditions:host_windows_x64_constraint
@bazel_tools//src/conditions:remote
@bazel_tools//src/conditions:windows
@bazel_tools//src/main/cpp/util:blaze_exit_code
@bazel_tools//src/main/cpp/util:errors
@bazel_tools//src/main/cpp/util:errors.h
@bazel_tools//src/main/cpp/util:errors_posix.cc
@bazel_tools//src/main/cpp/util:errors_windows.cc
@bazel_tools//src/main/cpp/util:exit_code.h
@bazel_tools//src/main/cpp/util:file.cc
@bazel_tools//src/main/cpp/util:file.h
@bazel_tools//src/main/cpp/util:file_platform.h
@bazel_tools//src/main/cpp/util:file_posix.cc
@bazel_tools//src/main/cpp/util:file_windows.cc
@bazel_tools//src/main/cpp/util:filesystem
@bazel_tools//src/main/cpp/util:ijar
@bazel_tools//src/main/cpp/util:logging
@bazel_tools//src/main/cpp/util:logging.cc
@bazel_tools//src/main/cpp/util:logging.h
@bazel_tools//src/main/cpp/util:path.cc
@bazel_tools//src/main/cpp/util:path.h
@bazel_tools//src/main/cpp/util:path_platform.h
@bazel_tools//src/main/cpp/util:path_posix.cc
@bazel_tools//src/main/cpp/util:path_windows.cc
@bazel_tools//src/main/cpp/util:port
@bazel_tools//src/main/cpp/util:port.cc
@bazel_tools//src/main/cpp/util:port.h
@bazel_tools//src/main/cpp/util:strings
@bazel_tools//src/main/cpp/util:strings.cc
@bazel_tools//src/main/cpp/util:strings.h
@bazel_tools//src/main/native/windows:file.cc
@bazel_tools//src/main/native/windows:file.h
@bazel_tools//src/main/native/windows:lib-file
@bazel_tools//src/main/native/windows:lib-process
@bazel_tools//src/main/native/windows:process.cc
@bazel_tools//src/main/native/windows:process.h
@bazel_tools//src/main/native/windows:util.cc
@bazel_tools//src/main/native/windows:util.h
@bazel_tools//src/tools/launcher:bash_launcher
@bazel_tools//src/tools/launcher:bash_launcher.cc
@bazel_tools//src/tools/launcher:bash_launcher.h
@bazel_tools//src/tools/launcher:dummy.cc
@bazel_tools//src/tools/launcher:java_launcher
@bazel_tools//src/tools/launcher:java_launcher.cc
@bazel_tools//src/tools/launcher:java_launcher.h
@bazel_tools//src/tools/launcher:launcher
@bazel_tools//src/tools/launcher:launcher.cc
@bazel_tools//src/tools/launcher:launcher.h
@bazel_tools//src/tools/launcher:launcher_base
@bazel_tools//src/tools/launcher:launcher_main.cc
@bazel_tools//src/tools/launcher:launcher_maker
@bazel_tools//src/tools/launcher:launcher_maker.cc
@bazel_tools//src/tools/launcher:python_launcher
@bazel_tools//src/tools/launcher:python_launcher.cc
@bazel_tools//src/tools/launcher:python_launcher.h
@bazel_tools//src/tools/launcher/util:data_parser
@bazel_tools//src/tools/launcher/util:data_parser.cc
@bazel_tools//src/tools/launcher/util:data_parser.h
@bazel_tools//src/tools/launcher/util:dummy.cc
@bazel_tools//src/tools/launcher/util:launcher_util.cc
@bazel_tools//src/tools/launcher/util:launcher_util.h
@bazel_tools//src/tools/launcher/util:util
@bazel_tools//third_party/def_parser:def_parser
@bazel_tools//third_party/def_parser:def_parser.cc
@bazel_tools//third_party/def_parser:def_parser.h
@bazel_tools//third_party/def_parser:def_parser_lib
@bazel_tools//third_party/def_parser:def_parser_main.cc
@bazel_tools//tools/build_defs/build_info:java_build_info
@bazel_tools//tools/build_defs/build_info/templates:non_volatile_file.properties.template
@bazel_tools//tools/build_defs/build_info/templates:redacted_file.properties.template
@bazel_tools//tools/build_defs/build_info/templates:volatile_file.properties.template
@bazel_tools//tools/cpp:current_cc_toolchain
@bazel_tools//tools/cpp:empty_lib
@bazel_tools//tools/cpp:link_extra_lib
@bazel_tools//tools/cpp:link_extra_libs
@bazel_tools//tools/cpp:malloc
@bazel_tools//tools/cpp:toolchain_type
@bazel_tools//tools/def_parser:def_parser
@bazel_tools//tools/def_parser:def_parser.exe
@bazel_tools//tools/def_parser:def_parser_windows
@bazel_tools//tools/def_parser:no_op.bat
@bazel_tools//tools/jdk:current_java_toolchain
@bazel_tools//tools/jdk:java_plugins_flag_alias
@bazel_tools//tools/jdk:launcher_flag_alias
@bazel_tools//tools/jdk:runtime_toolchain_type
@bazel_tools//tools/jdk:toolchain_type
@bazel_tools//tools/launcher:launcher
@bazel_tools//tools/launcher:launcher.exe
@bazel_tools//tools/launcher:launcher_maker
@bazel_tools//tools/launcher:launcher_maker.exe
@bazel_tools//tools/launcher:launcher_maker_windows
@bazel_tools//tools/launcher:launcher_windows
@@platforms//os:os
@@platforms//os:windows
@@rules_cc+//cc:current_cc_toolchain
@rules_java//java/bazel/rules:java_stub_template.txt
@rules_java//toolchains:current_java_toolchain
```

```bash
bazel query --noimplicit_deps "deps(//:runner)"
---
//:runner
//:src/main/java/com/example/Runner.java
//src/main/java/com/example/dishes:MacAndCheese.java
//src/main/java/com/example/dishes:Pizza.java
//src/main/java/com/example/dishes:macAndCheese
//src/main/java/com/example/dishes:pizza
//src/main/java/com/example/ingredients:Cheese.java
//src/main/java/com/example/ingredients:Dough.java
//src/main/java/com/example/ingredients:Macaroni.java
//src/main/java/com/example/ingredients:Tomato.java
//src/main/java/com/example/ingredients:cheese
//src/main/java/com/example/ingredients:dough
//src/main/java/com/example/ingredients:macaroni
//src/main/java/com/example/ingredients:tomato
//src/main/java/com/example/restaurant:Cafe.java
//src/main/java/com/example/restaurant:Chef.java
//src/main/java/com/example/restaurant:cafe
//src/main/java/com/example/restaurant:chef
@bazel_tools//tools/jdk:launcher_flag_alias
```


#### graph

```bash
bazel query   "deps(//:runner)" --output graph | dot -Tsvg > scripts/all_deps.svg
```


#### reverse dependency

```bash
$ bazel query  "rdeps(//:runner, //src/main/java/com/example/restaurant:Chef.java)
---

//:runner
//src/main/java/com/example/restaurant:Chef.java
//src/main/java/com/example/restaurant:cafe
//src/main/java/com/example/restaurant:chef
```

```bash
bazel query  "rdeps(//..., //src/main/java/com/example/restaurant:Chef.java)"
//:runner
//src/main/java/com/example/restaurant:Chef.java
//src/main/java/com/example/restaurant:cafe
//src/main/java/com/example/restaurant:chef
```


```bash
$ bazel query  "rdeps(//src/main/java/com/example/restaurant/..., //src/main/java/com/example/dishes)"
---
ERROR: no such target '//src/main/java/com/example/dishes:dishes': target 'dishes' not declared in package 'src/main/java/com/example/dishes' defined by /Users/udita.bose/spaces/bazelbuild/examples/query-quickstart/src/main/java/com/example/dishes/BUILD
FAIL: 7

bazel query  "rdeps(//src/main/java/com/example/restaurant/..., //src/main/java/com/example/dishes/...)"
---
//src/main/java/com/example/dishes:macAndCheese
//src/main/java/com/example/dishes:pizza
//src/main/java/com/example/restaurant:cafe
//src/main/java/com/example/restaurant:chef
```

```bash
bazel query  "rdeps(//src/main/java/com/example/restaurant/..., //src/main/java/com/example/dishes/...)"  --output graph | dot -Tsvg > scripts/rdeps.svg
```

#### attribute based search

```bash
bazel query 'attr(tags, "pizza", //:runner)
WARNING: Running Bazel server needs to be killed, because the startup options are different.
Starting local Bazel server (8.2.1) and connecting to it...
WARNING: For repository 'rules_java', the root module requires module version rules_java@7.11.1, but got rules_java@8.11.0 in the resolved dependency graph. Please update the version in your MODULE.bazel or set --check_direct_dependencies=off
INFO: Empty results
```

```bash
bazel query 'attr(tags, "pizza", //:all)
INFO: Empty results
```

```bash
bazel query 'attr(tags, "pizza", //...)  # attr(<type_of_attr>, <value_of_attr>, <domain_of_search>)
---
//src/main/java/com/example/customers:amir
//src/main/java/com/example/reviews:review
```
