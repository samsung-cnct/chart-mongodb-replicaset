# Copyright 2016 The Kubernetes Authors All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM alpine:3.4
MAINTAINER Michael Venezia <mvenezia@gmail.com>

ENV PEER_FINDER_SRC=https://raw.githubusercontent.com/venezia/contrib/peer-finder-default-domain/pets/peer-finder/peer-finder.go

RUN apk update && apk upgrade && \
    apk add git openssl ca-certificates go bash && \
    mkdir -p /projects/src/peer-finder && cd /projects/src/peer-finder && \
    wget ${PEER_FINDER_SRC} && \
    GOPATH=/projects go get && GOPATH=/projects CGO_ENABLED=0 go build peer-finder.go && \
    mv peer-finder / && cd / && rm -rf /projects && \
    apk del git openssl ca-certificates go

ENTRYPOINT ["/install.sh"]

ADD files/* /

RUN chmod -c 755 /install.sh /on-start.sh /peer-finder
