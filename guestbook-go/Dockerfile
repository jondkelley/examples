# Copyright 2016 The Kubernetes Authors.
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

FROM golang:1.10.0
RUN go get github.com/codegangsta/negroni \
           github.com/gorilla/mux \
           github.com/xyproto/simpleredis
WORKDIR /app
ADD ./main.go .
RUN CGO_ENABLED=0 GOOS=linux go build -o main .

RUN adduser --disabled-password --gecos '' --uid 11000 guestbook
RUN apt-get update && apt-get install -y tcpdump bash sudo
RUN echo 'guestbook ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

#FROM scratch

#COPY --from=0 /etc/passwd /etc/passwd
#COPY --from=0 /usr/sbin/tcpdump /usr/sbin/tcpdump
#COPY --from=0 /bin/bash /bin/bash

WORKDIR /app
#COPY --from=0 /app/main .
COPY ./public/index.html public/index.html
COPY ./public/script.js public/script.js
COPY ./public/style.css public/style.css
USER guestbook
CMD ["/app/main"]
EXPOSE 3000
