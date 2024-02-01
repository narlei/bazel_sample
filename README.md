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

Duplicated actions:

| Pre Action | Post Action |
|------------|-------------|
|![Pre](/Screenshots/pre_action.png)|![Post](/Screenshots/post_action.png)|

The pre-post actions are defined here: https://github.com/narlei/bazel_sample/blob/414777efed29d9c1cb1330bc45f0019917c825b1/BUILD#L94
