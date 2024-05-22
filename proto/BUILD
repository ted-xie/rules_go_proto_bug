load("@rules_go//proto:def.bzl", "go_proto_library")

proto_library(
  name = "foo_proto",
  srcs = ["foo.proto"],
)

go_proto_library(
  name = "foo_go_proto",
  importpath = "proto.foo_go_proto",
  protos = [":foo_proto"],
)
