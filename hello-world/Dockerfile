FROM golang:alpine3.9 As builder
RUN apk update && apk upgrade && \
    apk add --no-cache git && \
    go get github.com/gorilla/mux

WORKDIR /app
ADD ./main.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a --installsuffix cgo -o main .

FROM alpine:3.9
WORKDIR /app
COPY --from=builder /app/main .
COPY ./templates/assets/k8s.svg templates/assets/k8s.svg
COPY ./templates/index.html templates/index.html
EXPOSE 8080
ENTRYPOINT [ "./main" ]

