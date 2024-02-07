# This is a rules_xcodeproj Sample

To run the project just checkout the main branch and run

```
make create_project
```

Or manually:

```
bazel run //:xcodeproj
open BazelSample.xcodeproj
```

Currently, we found a bug in the incremental project generation:

We're creating an `ios_application` with a dependency:

https://github.com/narlei/bazel_sample/blob/17ffe7284ca411f532194b991dd105fe30455dde/BUILD#L45

The `MySampleSource` contains the app dependencies:

https://github.com/narlei/bazel_sample/blob/17ffe7284ca411f532194b991dd105fe30455dde/BUILD#L21

The bug is when I'm trying to focus on the `MySampleSource` and on `MySampleApp`:

https://github.com/narlei/bazel_sample/blob/17ffe7284ca411f532194b991dd105fe30455dde/BUILD#L65

```
ERROR: Internal precondition failure:
tools/generators/xcschemes/src/Generator/CreateCustomSchemeInfos.swift:461: Run build target "@//:MySampleSource ios-sim_arm64-min16.0-applebin_ios-ios_sim_arm64-dbg-ST-21282182d87c" not found in:
[@//:MySampleApp ios-sim_arm64-min16.0-applebin_ios-ios_sim_arm64-dbg-ST-21282182d87c, @//Libraries/LibraryA:LibraryACore ios-sim_arm64-min16.0-applebin_ios-ios_sim_arm64-dbg-ST-21282182d87c, @//Libraries/LibraryA:LibraryAInterface ios-sim_arm64-min16.0-applebin_ios-ios_sim_arm64-dbg-ST-21282182d87c, @//Libraries/LibraryB:LibraryB ios-sim_arm64-min16.0-applebin_ios-ios_sim_arm64-dbg-ST-21282182d87c, @//Libraries/LibraryC:LibraryC ios-sim_arm64-min16.0-applebin_ios-ios_sim_arm64-dbg-ST-21282182d87c, @//Libraries/LibraryD:LibraryD ios-sim_arm64-min16.0-applebin_ios-ios_sim_arm64-dbg-ST-21282182d87c]
```

The rules_xcodeproj isn't finding the `MySampleSource` on the target lists.
This is a target of a xcscheme:

https://github.com/narlei/bazel_sample/blob/17ffe7284ca411f532194b991dd105fe30455dde/BUILD#L99

Removing the `MySampleApp` from the focus list (and from the `launch_target`) works without errors, finding the `MySampleSource`, but it creates a xscheme without the launch app.


