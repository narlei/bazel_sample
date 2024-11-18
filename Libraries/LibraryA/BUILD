load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library", "swift_test")

swift_library(
    name = "LibraryACore",
    module_name = "LibraryACore",
    srcs = glob(["Core/*.swift"]),
    visibility = ["//visibility:public"],
    tags = ["manual"],
    deps = [
        ":LibraryAInterface"
    ]
)

swift_library(
    name = "LibraryAInterface",
    module_name = "LibraryAInterface",
    srcs = glob(["Interface/*.swift"]),
    visibility = ["//visibility:public"],
    tags = ["manual"],
)

swift_test(
    name = "LibraryACoreTests",
    visibility = ["//visibility:public"],
    srcs = glob(["Tests/*.swift"]),
    deps = [
        ":LibraryACore",
    ],
)