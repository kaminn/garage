# Build the Go Binary
FROM golang:1.20 as build_sales-api
ENV CGO_ENABLED 0
ARG BUILD_REF

# Copy the source code into the container.
COPY . /service

# Build the service binary.
WORKDIR /service
RUN go build -ldflags "-X main.build=${BUILD_REF}"

# Run the Go Binary in Alpine.
FROM alpine:3.14
ARG BUILD_DATE
ARG BUILD_REF
COPY --from=build_sales-api /service/garage /service/garage
WORKDIR /service
CMD ["./garage"]

LABEL org.opencontainers.image.created="${BUILD_DATE}" \
      org.opencontainers.image.title="sales-api" \
      org.opencontainers.image.authors="William Kennedy <bill@ardanlabs.com>" \
      org.opencontainers.image.source="https://github.com/ardanlabs/service/app/sales-api" \
      org.opencontainers.image.revision="${BUILD_REF}" \
      org.opencontainers.image.vendor="Ardan Labs"