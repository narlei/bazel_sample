# This is a rules_xcodeproj Sample

To run the project just checkout the main branch and run

```
make create_project
```

Or mannually:

```
	bazel run //:xcodeproj
	open BazelSample.xcodeproj
```

Currently, we found some bugs on the incremental project generation:

1. Duplicated actions:

| Pre Action | Post Action |
|------------|-------------|
|![Pre](/Screenshots/pre_action.png)|![Post](/Screenshots/post_action.png)|

2. When changing the focused targets, the project don't update automatically with the Xcode opened, it's needed to restart the xcode to update the focused targets.