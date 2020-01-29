Run the script below (sometimes you have to do it twice):
 
```shell
git reset --hard 3f415776e73bdf7acc90eaca52557e1c7cf664cb

rm -rf common-assets/node_modules
pushd common-assets && yarn && popd

# Uncomment below and it fixes bazel error
#bazel --noworkspace_rc build --worker_quit_after_build @npm_common-assets//:node_modules

git reset --hard 91261ed4232774372dd2c9c7dd103640dbbe71ab

# Uncomment below and it fixes bazel error, but postinstall fails
#git reset --hard 60a7b73948fa49926a331e50fee140266ba9df8f

bazel --noworkspace_rc build --worker_quit_after_build @npm_common-assets//:node_modules
```

It should result in an error like the following:

```
INFO: Analyzed target @npm_common-assets//:node_modules (0 packages loaded, 0 targets configured).
INFO: Found 1 target...
ERROR: missing input file '@npm_common-assets//:node_modules/@babel/core/lib/transformation/util/missing-plugin-helper.js'
ERROR: /private/var/tmp/_bazel_chris/1a743f6e6ae983da82c3cfec7dc4b342/external/npm_common-assets/BUILD.bazel:5374:1: @npm_common-assets//:node_modules: missing input file 'LabelCause{label=@npm_common-assets//:node_modules/@babel/core/lib/transformation/util/missing-plugin-helper.js, msg=missing input file '@npm_common-assets//:node_modules/@babel/core/lib/transformation/util/missing-plugin-helper.js'}'
ERROR: missing input file '@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-function-name/LICENSE'
ERROR: /private/var/tmp/_bazel_chris/1a743f6e6ae983da82c3cfec7dc4b342/external/npm_common-assets/BUILD.bazel:5374:1: @npm_common-assets//:node_modules: missing input file 'LabelCause{label=@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-function-name/LICENSE, msg=missing input file '@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-function-name/LICENSE'}'
ERROR: missing input file '@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-function-name/README.md'
ERROR: /private/var/tmp/_bazel_chris/1a743f6e6ae983da82c3cfec7dc4b342/external/npm_common-assets/BUILD.bazel:5374:1: @npm_common-assets//:node_modules: missing input file 'LabelCause{label=@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-function-name/README.md, msg=missing input file '@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-function-name/README.md'}'
ERROR: missing input file '@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-function-name/lib/index.js'
ERROR: /private/var/tmp/_bazel_chris/1a743f6e6ae983da82c3cfec7dc4b342/external/npm_common-assets/BUILD.bazel:5374:1: @npm_common-assets//:node_modules: missing input file 'LabelCause{label=@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-function-name/lib/index.js, msg=missing input file '@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-function-name/lib/index.js'}'
ERROR: missing input file '@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-function-name/package.json'
ERROR: /private/var/tmp/_bazel_chris/1a743f6e6ae983da82c3cfec7dc4b342/external/npm_common-assets/BUILD.bazel:5374:1: @npm_common-assets//:node_modules: missing input file 'LabelCause{label=@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-function-name/package.json, msg=missing input file '@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-function-name/package.json'}'
ERROR: missing input file '@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-get-function-arity/LICENSE'
ERROR: /private/var/tmp/_bazel_chris/1a743f6e6ae983da82c3cfec7dc4b342/external/npm_common-assets/BUILD.bazel:5374:1: @npm_common-assets//:node_modules: missing input file 'LabelCause{label=@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-get-function-arity/LICENSE, msg=missing input file '@npm_common-assets//:node_modules/@babel/core/node_modules/@babel/helper-get-function-arity/LICENSE'}'
....
Target @npm_common-assets//:node_modules failed to build
Use --verbose_failures to see the command lines of failed build steps.
ERROR: /private/var/tmp/_bazel_chris/1a743f6e6ae983da82c3cfec7dc4b342/external/npm_common-assets/BUILD.bazel:5374:1 309 input file(s) do not exist
INFO: Elapsed time: 0.563s, Critical Path: 0.00s
INFO: 0 processes.
FAILED: Build did NOT complete successfully

```
