load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_jar")

http_archive(
    name = "build_bazel_rules_apple",
    sha256 = "34c41bfb59cdaea29ac2df5a2fa79e5add609c71bb303b2ebb10985f93fa20e7",
    url = "https://github.com/bazelbuild/rules_apple/releases/download/3.1.1/rules_apple.3.1.1.tar.gz",
)

load(
    "@build_bazel_rules_apple//apple:repositories.bzl",
    "apple_rules_dependencies",
)

apple_rules_dependencies()

http_archive(
    name = "build_bazel_rules_swift",
    sha256 = "28a66ff5d97500f0304f4e8945d936fe0584e0d5b7a6f83258298007a93190ba",
    url = "https://github.com/bazelbuild/rules_swift/releases/download/1.13.0/rules_swift.1.13.0.tar.gz",
)

load(
    "@build_bazel_rules_swift//swift:repositories.bzl",
    "swift_rules_dependencies",
)

swift_rules_dependencies()

load(
    "@build_bazel_rules_swift//swift:extras.bzl",
    "swift_rules_extra_dependencies",
)

swift_rules_extra_dependencies()

load(
    "@build_bazel_apple_support//lib:repositories.bzl",
    "apple_support_dependencies",
)

apple_support_dependencies()

load(
    "@build_bazel_rules_apple//apple:apple.bzl",
    "provisioning_profile_repository",
)

provisioning_profile_repository(
    name = "local_provisioning_profiles",
)

# Required for rules_xcodeproj
http_archive(
    name = "bazel_features",
    sha256 = "9fcb3d7cbe908772462aaa52f02b857a225910d30daa3c252f670e3af6d8036d",
    strip_prefix = "bazel_features-1.0.0",
    url = "https://github.com/bazel-contrib/bazel_features/releases/download/v1.0.0/bazel_features-v1.0.0.tar.gz",
)
load("@bazel_features//:deps.bzl", "bazel_features_deps")
bazel_features_deps()

http_archive(
    name = "rules_xcodeproj",
    sha256 = "ccc719851a9942c53b9359984106e9fa5c5c97d9621b346243b638b18ec097f9",
    url = "https://github.com/MobileNativeFoundation/rules_xcodeproj/releases/download/1.16.0/release.tar.gz",
)

load(
    "@rules_xcodeproj//xcodeproj:repositories.bzl",
    "xcodeproj_rules_dependencies",
)

xcodeproj_rules_dependencies()

http_jar(
    name = "bazel_diff",
    sha256 = "7943790f690ad5115493da8495372c89f7895b09334cb4fee5174a8f213654dd",
    urls = [
        "https://github.com/Tinder/bazel-diff/releases/download/5.0.0/bazel-diff_deploy.jar",
    ],
)

http_archive(
    name = "build_bazel_rules_ios",
    sha256 = "2dbf4d17fc6e454ae3113869a095afa79b1f2182782f999533d17fef5bbdf88b",
    url = "https://github.com/bazel-ios/rules_ios/releases/download/3.1.1/rules_ios.3.1.1.tar.gz",
)

load(
    "@build_bazel_rules_ios//rules:repositories.bzl",
    "rules_ios_dependencies"
)

rules_ios_dependencies()