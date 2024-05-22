# Bug in rules_go + --experimental_sibling_repository_layout

## Environment

* rules_go: 0.48
  * Also reproduces at latest rules_go commit (354a98f4acf2333b7603ede50dd5fbc20ae315b1)
* bazel: 7.1.2
* OS: Linux (Debian-based derivative)

## Overview

rules_go seems to have an issue with building go_proto_library dependencies as remote deps when bazel's `--experimental_sibling_repository_layout` is used.

This project has two levels: an outer project and an inner project (called "submodule").

In the outer project: `bazelisk build proto:foo_go_proto` succeeds.

In the inner project: `bazelisk build @maybe_rules_go_proto_bug//proto:foo_go_proto` succeeds.

In the inner proejct: `bazelisk build @maybe_rules_go_proto_bug//proto:foo_go_proto --experimental_sibling_repository_layout` fails with this error:

```
Could not find file in descriptor database: ../maybe_rules_go_proto_bug~/proto/foo.proto: No such file or directory
2024/05/22 16:40:13 error running protoc: exit status 1
```
