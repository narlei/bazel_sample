load("@build_bazel_rules_apple//apple:ios.bzl", "ios_application")
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")
load("@build_bazel_rules_apple//apple:versioning.bzl", "apple_bundle_version")
load("@build_bazel_rules_apple//apple:resources.bzl", "apple_resource_group")
load("@rules_xcodeproj//xcodeproj:defs.bzl", "top_level_target", "xcschemes", "xcodeproj")

apple_resource_group(
    name = "PerformanceTestAppAssets",
    resources = glob(["App/**/*.xcassets/**/*"]) + glob(["App/**/*.storyboard"]),
    visibility = ["//visibility:public"],
    tags = ["manual"],
)


swift_library(
    name = "BaseSource",
    tags = ["manual"],
    module_name = "BaseSource",
    srcs = glob(["App/**/*.swift"]),
    visibility = ["//visibility:public"],
    deps = [
        "//Libraries/LibraryA:LibraryACore",
        "//Libraries/LibraryA:LibraryAInterface",
        "//Libraries/LibraryB:LibraryB",
        "//Libraries/LibraryC:LibraryC",
        "//Libraries/LibraryD:LibraryD",
    ]
)

apple_bundle_version(
    name = "BazelSampleVersion",
    build_version = "1.2.3.4",
    short_version_string = "1.2.3",
    tags = ["manual"],
)

ios_application(
    name = "MyApp",
    bundle_id = "com.narlei.sample",
    families = [
        "iphone",
        "ipad",
    ],
    infoplists = ["App/Info.plist"],
    deps = [
        ":BaseSource",
    ],
    minimum_os_version = "16.0",
    visibility = ["//visibility:public"],
    resources = [":PerformanceTestAppAssets"],
    version = ":BazelSampleVersion",
)

######## Project ##########

XCODEPROJ_FRAMEWORK_TARGETS = [
]

XCODEPROJ_ASSOCIATED_EXTRA_FILES = {
}

XCODEPROJ_TEST_TARGETS = [
]

XCODEPROJ_FOCUSED_TARGETS = [
    "//:MyApp",
    "//Libraries/LibraryA:LibraryACore",
    "//Libraries/LibraryA:LibraryAInterface",
    "//Libraries/LibraryB:LibraryB",
    "//Libraries/LibraryC:LibraryC",
    "//Libraries/LibraryD:LibraryD",
]

XCODEPROJ_UNFOCUSED_TARGETS = [
]

XCODEPROJ_EXAMPLE_APPS = [
    top_level_target("//:MyApp", target_environments = ["simulator"])
]

SCHEMES = [
    xcschemes.scheme(
        name = "ProjectSample",
        profile = None,
        run = xcschemes.run(
            build_targets = [
            ],
            launch_target = xcschemes.launch_target(
                "//:MyApp",
                library_targets = [
                    "//Libraries/LibraryA:LibraryACore",
                    "//Libraries/LibraryA:LibraryAInterface",
                    "//Libraries/LibraryB:LibraryB",
                    "//Libraries/LibraryC:LibraryC",
                    "//Libraries/LibraryD:LibraryD",
                ],
                post_actions = [
                    xcschemes.pre_post_actions.build_script(title = "This is a post_action", script_text = "echo 'Bye'")
                ],
                pre_actions = [
                    xcschemes.pre_post_actions.build_script(title = "This is a pre_action", script_text = "echo 'Hi'")
                ]
            ),
        ),
    ),

    xcschemes.scheme(
        name = "Library_A",
        profile = None,
        run = xcschemes.run(
            build_targets = [
            ],
            launch_target = xcschemes.launch_target(
                library_targets = [
                    "//Libraries/LibraryA:LibraryACore",
                    "//Libraries/LibraryA:LibraryAInterface",
                ],
                post_actions = [
                    xcschemes.pre_post_actions.build_script(title = "This is a post_action", script_text = "echo 'Bye'")
                ],
                pre_actions = [
                    xcschemes.pre_post_actions.build_script(title = "This is a pre_action", script_text = "echo 'Hi'")
                ]
            ),
        ),
    ),
]

xcodeproj(
    name = "xcodeproj",
    associated_extra_files = XCODEPROJ_ASSOCIATED_EXTRA_FILES,
    bazel_env = {
        "PATH": "/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin",
    },
    build_mode = "bazel",
    bazel_path = "./bazelw",
    focused_targets = XCODEPROJ_FOCUSED_TARGETS,
    project_name = "BazelSample",
    xcschemes = SCHEMES,
    tags = ["manual"],
    top_level_targets = XCODEPROJ_TEST_TARGETS + XCODEPROJ_EXAMPLE_APPS + XCODEPROJ_FRAMEWORK_TARGETS,
    unfocused_targets = XCODEPROJ_UNFOCUSED_TARGETS,
    generation_mode = "incremental",
)