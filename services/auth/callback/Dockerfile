FROM golang:1.23.6 as build
WORKDIR /auth/callback
# Copy dependencies list
COPY go.mod go.sum ./
# Build with optional lambda.norpc tag
COPY main.go .
RUN go build -tags lambda.norpc -o main main.go
# Copy artifacts to a clean image
FROM public.ecr.aws/lambda/provided:al2023
COPY --from=build /auth/callback/main ./main
ENTRYPOINT [ "./main" ]
