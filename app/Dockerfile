FROM golang:latest

RUN go get github.com/constabulary/gb/...

RUN mkdir -p /go/src/app
WORKDIR /go/src/app

COPY . /go/src/app
RUN gb build