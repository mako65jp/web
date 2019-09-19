#-------------------------------------------------------------------------------------------------------------
# Copyright (c) Microsoft Corporation. All rights reserved.
# Licensed under the MIT License. See https://go.microsoft.com/fwlink/?linkid=2090316 for license information.
#-------------------------------------------------------------------------------------------------------------

FROM mcr.microsoft.com/dotnet/core/sdk:2.1

# Avoid warnings by switching to noninteractive
# 非対話型に切り替えることで警告を回避します
ENV DEBIAN_FRONTEND=noninteractive

# Or your actual UID, GID on Linux if not the default 1000
# または、デフォルトの1000ではない場合、Linuxの実際のUID、GID
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Configure apt and install packages
RUN apt-get update \
    && apt-get -y install --no-install-recommends apt-utils dialog 2>&1 \
    #
    # Verify git, process tools, lsb-release (common in install instructions for CLIs) installed
    # git、プロセスツール、lsb-release（CLIのインストール手順に共通）がインストールされていることを確認します
    && apt-get -y install git procps lsb-release \
    #
    # Create a non-root user to use if preferred - see https://aka.ms/vscode-remote/containers/non-root-user.
    # 必要に応じて使用する非rootユーザーを作成します-https://aka.ms/vscode-remote/containers/non-root-userを参照してください。
    && groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Uncomment the next three lines to add sudo support
    # [オプション] sudoサポートを追加するには、次の3行のコメントを解除します
    # && apt-get install -y sudo \
    # && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    # && chmod 0440 /etc/sudoers.d/$USERNAME \
    #
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Switch back to dialog for any ad-hoc use of apt-get
# apt-getのアドホックな使用のためにダイアログに切り替えます
ENV DEBIAN_FRONTEND=

EXPOSE 5000
