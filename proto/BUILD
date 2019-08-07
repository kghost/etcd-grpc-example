package(default_visibility = ["//visibility:public"])

load("@rules_proto//proto:defs.bzl", "proto_library")

proto_library(
    name = "etcd_kv_proto",
    srcs = ["etcd/mvcc/mvccpb/kv.proto"],
    deps = [":gogo_proto"],
    proto_source_root = "proto",
)

proto_library(
    name = "etcd_auth_proto",
    srcs = ["etcd/auth/authpb/auth.proto"],
    deps = [":gogo_proto"],
    proto_source_root = "proto",
)

proto_library(
    name = "gogo_proto",
    srcs = ["gogoproto/gogo.proto"],
    deps = ["@com_google_protobuf//:descriptor_proto"],
    proto_source_root = "proto",
)

proto_library(
    name = "etcd_rpc_proto",
    srcs = ["etcd/etcdserver/etcdserverpb/rpc.proto"],
    deps = [
        ":etcd_kv_proto",
        ":etcd_auth_proto",
        ":gogo_proto",
        "@com_google_googleapis_protos//google/api:annotations_proto",
    ],
    proto_source_root = "proto",
)

cc_proto_library(
    name = "etcd_rpc_cc",
    deps = [":etcd_rpc_proto"],
)

load("@com_github_grpc_grpc//bazel:cc_grpc_library.bzl", "cc_grpc_library")
cc_grpc_library(
    name = "etcd_rpc_service",
    srcs = [":etcd_rpc_proto"],
    grpc_only = True,
    proto_only = False,
    use_external = True,
    well_known_protos = True,
    deps = [":etcd_rpc_cc"],
)
