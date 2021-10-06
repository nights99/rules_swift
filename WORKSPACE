workspace(name = "build_bazel_rules_swift")

# Fails under CI because of update_workspace_to_deps_heads
# workspace(
#     name = "build_bazel_rules_swift",
#     managed_directories = {"@exampledeps": [".build"]}, 
# )

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

load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")

bazel_skylib_workspace()

# For API doc generation
# This is a dev dependency, users should not need to install it
# so we declare it in the WORKSPACE
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "io_bazel_stardoc",
    patches = ["//doc:stardoc.pr103.patch"],
    sha256 = "f89bda7b6b696c777b5cf0ba66c80d5aa97a6701977d43789a9aee319eef71e8",
    strip_prefix = "stardoc-d93ee5347e2d9c225ad315094507e018364d5a67",
    urls = [
        "https://github.com/bazelbuild/stardoc/archive/d93ee5347e2d9c225ad315094507e018364d5a67.tar.gz",
    ],
protobuf_deps()

# I don't know where to put this since sub workspaces does not work well in bazel
# https://github.com/bazelbuild/bazel/issues/2391
load(
    "@build_bazel_rules_swift//swift:package.bzl",
    "swift_package_install",
)

swift_package_install(
    name = "exampledeps",
    package = "@//:Package.swift",
    package_resolved = "@//:Package.resolved",
    #symlink_build_path = True, Fails under CI
    debug = True
)
