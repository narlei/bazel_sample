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

Currently, we found some bugs in the incremental project generation:

1. Duplicated actions:

| Pre Action | Post Action |
|------------|-------------|
|![Pre](/Screenshots/pre_action.png)|![Post](/Screenshots/post_action.png)|

The pre-post actions are defined here: https://github.com/narlei/bazel_sample/blob/414777efed29d9c1cb1330bc45f0019917c825b1/BUILD#L94

2. When changing the focused targets, the project doesn't update automatically with the Xcode opened, it's needed to restart the Xcode to update the focused targets.
