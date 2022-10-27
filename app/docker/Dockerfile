# Copyright 2020 Alex Woroschilow (alex.woroschilow@gmail.com)
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
FROM ubuntu:20.04

ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

RUN apt-get -y update
RUN apt-get -y install apt-utils
RUN apt-get -y upgrade

RUN apt-get install -y kmod make gcc wget gnupg
RUN apt-get install -y rpm2cpio cpio
RUN apt-get install -y fuse
RUN apt-get install -y file

RUN wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://packages.microsoft.com/repos/edge/ stable main" >> /etc/apt/sources.list.d/microsoft_edge.list'
RUN apt update

RUN apt-get install -y microsoft-edge-stable