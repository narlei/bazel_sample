load("@build_bazel_rules_apple//apple:ios.bzl", "ios_application")
load("@build_bazel_rules_apple//apple:resources.bzl", "apple_resource_group")
load("@build_bazel_rules_apple//apple:versioning.bzl", "apple_bundle_version")
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")
load("@rules_xcodeproj//xcodeproj:defs.bzl", "top_level_target", "xcodeproj", "xcschemes")

apple_resource_group(
    name = "PerformanceTestAppAssets",
    resources = glob(["App/**/*.xcassets/**/*"]) + glob(["App/**/*.storyboard"]),
    tags = ["manual"],
    visibility = ["//visibility:public"],
)

swift_library(
    name = "MySampleSource",
    srcs = glob(["App/**/*.swift"]),
    module_name = "MySampleSource",
    tags = ["manual"],
    visibility = ["//visibility:public"],
    deps = [
        "//Libraries/LibraryA:LibraryACore",
        "//Libraries/LibraryA:LibraryAInterface",
    ],
)

apple_bundle_version(
    name = "BazelSampleVersion",
    build_version = "1.2.3.4",
    short_version_string = "1.2.3",
    tags = ["manual"],
)

ios_application(
    name = "MySampleApp",
    bundle_id = "com.narlei.sample",
    families = [
        "iphone",
        "ipad",
    ],
    infoplists = ["App/Info.plist"],
    minimum_os_version = "16.0",
    resources = [":PerformanceTestAppAssets"],
    version = ":BazelSampleVersion",
    visibility = ["//visibility:public"],
    deps = [
        ":MySampleSource",
    ],
)

######## Project ##########

XCODEPROJ_FOCUSED_TARGETS = [
    "//:MySampleApp",  # Comment this line to simulate working without the app on focus targets
    "//:MySampleSource",
    "//Libraries/LibraryA:LibraryACore",
    "//Libraries/LibraryA:LibraryAInterface",
    "//Libraries/LibraryA:LibraryACoreTests",  # Adicionado aqui
]

SCHEMES = [
    xcschemes.scheme(
        name = "ProjectSample",
        profile = None,
        run = xcschemes.run(
            build_targets = [
                xcschemes.top_level_anchor_target(
                    label = "//:MySampleApp",
                    library_targets = [
                        "//:MySampleSource",
                        "//Libraries/LibraryA:LibraryACore",
                        "//Libraries/LibraryA:LibraryAInterface",
                    ],
                ),
            ],
            # Comment the launch_target to simulate working without the app on focus targets
            launch_target = xcschemes.launch_target(
                "//:MySampleApp",
            ),
        ),
        test = xcschemes.test(
            test_targets = [
                xcschemes.test_target(
                    "//Libraries/LibraryA:LibraryACoreTests",
                ),
            ],
            test_options = xcschemes.test_options(
                app_language = "pt-BR",
                app_region = "BR",
            ),
        )
    ),
]

xcodeproj(
    name = "xcodeproj",
    bazel_env = {
        "PATH": "/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin",
    },
    bazel_path = "./bazelw",
    build_mode = "bazel",
    focused_targets = XCODEPROJ_FOCUSED_TARGETS,
    generation_mode = "incremental",
    project_name = "BazelSample",
    tags = ["manual"],
    top_level_targets = [
        top_level_target(
            "//:MySampleApp",
            target_environments = ["simulator"],
        ),
        "//Libraries/LibraryA:LibraryACoreTests",
    ],
    xcschemes = SCHEMES,
)