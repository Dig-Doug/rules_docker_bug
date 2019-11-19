load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_file")

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "14ac30773fdb393ddec90e158c9ec7ebb3f8a4fd533ec2abbfd8789ad81a284b",
    strip_prefix = "rules_docker-0.12.1",
    urls = [
        "https://github.com/bazelbuild/rules_docker/archive/v0.12.1.tar.gz",
    ],
)

http_file(
    name = "docker_gpg",
    sha256 = "1500c1f56fa9e26b9b8f42452a553675796ade0807cdce11975eb98170b3a570",
    urls = [
        "https://download.docker.com/linux/ubuntu/gpg",
    ],
)

http_file(
    name = "llvm_gpg",
    sha256 = "ce6eee4130298f79b0e0f09a89f93c1bc711cd68e7e3182d37c8e96c5227e2f0",
    urls = [
        "https://apt.llvm.org/llvm-snapshot.gpg.key",
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

