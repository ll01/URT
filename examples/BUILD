load("@rules_cc//cc:defs.bzl", "cc_binary", "cc_library")

cc_binary(
    name = "example1",
    srcs = ["example1.cpp"],
    deps = [
        "@eigen//:eigen",
        "@boost//:boost",
        "//:URT"
    ],
    copts = ["-DUSE_EIGEN"],
    linkstatic=False,
)

cc_binary(
    name = "example2",
    srcs = ["example2.cpp"],
    deps = [
        "//:URT"
    ],
    copts = ["-DUSE_EIGEN"],
)

cc_binary(
    name = "example3",
    srcs = ["example3.cpp"],
    deps = [
        "//:URT"
    ],
    copts = ["-DUSE_EIGEN"],
)

cc_binary(
    name = "example4",
    srcs = ["example4.cpp"],
    deps = [
        "//:URT"
    ],
    copts = ["-DUSE_EIGEN"],
)

cc_binary(
    name = "example5",
    srcs = ["example5.cpp"],
    deps = [
        "//:URT"
    ],
    copts = ["-DUSE_EIGEN"],
)
