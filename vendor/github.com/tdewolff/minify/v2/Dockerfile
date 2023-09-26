# Use this image to build the executable
FROM golang:1.18-alpine@sha256:77f25981bd57e60a510165f3be89c901aec90453fd0f1c5a45691f6cb1528807 AS build

WORKDIR /go/src/github.com/tdewolff/minify
COPY . /go/src/github.com/tdewolff/minify/

RUN apk add --no-cache git ca-certificates make bash
RUN /usr/bin/env bash -c make install


# Final image containing the executable from the previous step
FROM alpine:3@sha256:7144f7bab3d4c2648d7e59409f15ec52a18006a128c733fcff20d3a4a54ba44a

COPY --from=build /go/bin/minify /usr/bin/minify
COPY "containerfiles/container-entrypoint.sh" "/init.sh"

ENTRYPOINT ["/init.sh"]
