load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")

swift_library(
    name = "LibraryB",
    module_name = "LibraryB",
    srcs = glob(["**/**/*.swift"]),
    visibility = ["//visibility:public"],
    tags = ["manual"],
)