FROM --platform=linux/amd64 ubuntu:22.04 as builder

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y build-essential python3 git
RUN apt install -y apt-transport-https curl gnupg
RUN curl -fsSL https://bazel.build/bazel-release.pub.gpg | gpg --dearmor > bazel.gpg
RUN mv bazel.gpg /etc/apt/trusted.gpg.d/
RUN echo 'deb [arch=amd64] https://storage.googleapis.com/bazel-apt stable jdk1.8' | tee /etc/apt/sources.list.d/bazel.list
RUN apt update && apt install -y bazel

COPY . /repo
WORKDIR /repo
ENV GIT_VERSION=foo
RUN bazel build //common/tools:verible-patch-tool

FROM ubuntu:22.04 as package
COPY --from=builder /repo/bazel-bin/common/tools/verible-patch-tool /
