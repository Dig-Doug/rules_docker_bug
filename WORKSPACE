load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "51867e97bfbf392cc4619f207b4760007732fc1c08a68d501bc0ae0ce33a4a21",
    strip_prefix = "rules_docker-9b06b0c2af5be46bd880b44ba762e8b972177450",
    urls = [
        "https://github.com/bazelbuild/rules_docker/archive/9b06b0c2af5be46bd880b44ba762e8b972177450.tar.gz",
    ],
)

####################################
# Workspace setup

load(
    "@io_bazel_rules_docker//toolchains/docker:toolchain.bzl",
    docker_toolchain_configure = "toolchain_configure",
)

docker_toolchain_configure(
    name = "docker_config",
)

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)

container_repositories()

load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_deps()

load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_pull",
)

container_pull(
    name = "official_ubuntu",
    digest = "sha256:eb70667a801686f914408558660da753cde27192cd036148e58258819b927395",
    registry = "index.docker.io",
    repository = "library/ubuntu",
)

container_pull(
    name = "rbe_ubuntu16_04",
    digest = "sha256:98cd34f400a696c0409a3aa0411923b7198aced800a84f23b31f883f8bf407e7",
    registry = "marketplace.gcr.io",
    repository = "google/rbe-ubuntu16-04",
)

