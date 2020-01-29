workspace(
    name = "repro",
    managed_directories = {
        "@npm_root": ["node_modules"],
        "@npm_common-assets": ["common-assets/node_modules"],
    }
)
load(
    "@bazel_tools//tools/build_defs/repo:http.bzl",
    "http_archive",
    "http_jar",
    "http_file",
)

http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "c97bf38546c220fa250ff2cc052c1a9eac977c662c1fc23eda797b0ce8e70a43",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/1.1.0/rules_nodejs-1.1.0.tar.gz"],
)

load("@build_bazel_rules_nodejs//:index.bzl", "node_repositories", "yarn_install")

node_repositories(
  package_json = ["//:package.json"],
  node_version = "10.16.0",
  yarn_version = "1.16.0",
  node_repositories = {
    "10.16.0-darwin_amd64": ("node-v10.16.0-darwin-x64.tar.gz", "node-v10.16.0-darwin-x64", "6c009df1b724026d84ae9a838c5b382662e30f6c5563a0995532f2bece39fa9c"),
    "10.16.0-linux_amd64": ("node-v10.16.0-linux-x64.tar.xz", "node-v10.16.0-linux-x64", "1827f5b99084740234de0c506f4dd2202a696ed60f76059696747c34339b9d48"),
  },
  yarn_repositories = {
    "1.16.0": ("yarn-v1.16.0.tar.gz", "yarn-v1.16.0", "df202627d9a70cf09ef2fb11cb298cb619db1b958590959d6f6e571b50656029"),
  },
  node_urls = ["https://nodejs.org/dist/v{version}/{filename}"],
  yarn_urls = ["https://github.com/yarnpkg/yarn/releases/download/v{version}/{filename}"],
)

yarn_install(
    name = "npm_common-assets",
    package_json = "//common-assets:package.json",
    yarn_lock = "//common-assets:yarn.lock",
    symlink_node_modules = False,
)

yarn_install(
    name = "npm_root",
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
    symlink_node_modules = False,
)
