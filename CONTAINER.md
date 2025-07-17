# Container Images and Binary Releases

This project provides both pre-built container images and native binaries for smokescreen that are automatically built and published.

## Binary Releases

Pre-compiled binaries are available for download from the [GitHub Releases](https://github.com/stripe/smokescreen/releases) page:

- **Linux**: `smokescreen-linux-amd64`, `smokescreen-linux-arm64`
- **macOS**: `smokescreen-darwin-amd64`, `smokescreen-darwin-arm64`

Each release includes:
- Binaries for amd64 and arm64 for mac and linux

### Download and Install

```bash
# Download the latest binary (replace with your platform)
curl -L -o smokescreen https://github.com/stripe/smokescreen/releases/latest/download/smokescreen-linux-amd64

# Make it executable
chmod +x smokescreen

# Run
./smokescreen --help
  ```

## Container Images

### Available Images

The container images are available at:
- `ghcr.io/stripe/smokescreen:latest` - Latest release

## Supported Platforms

- `linux/amd64` - Intel/AMD 64-bit
- `linux/arm64` - ARM 64-bit

## Running the Container

### Basic Usage

```bash
docker run -p 4750:4750 ghcr.io/stripe/smokescreen:latest  --listen-ip 0.0.0.0 --listen-port 4750
```

Smokescreen can then be used like in `curl --proxy localhost:4750 http://example.com`.

## Verification

To verify the image signature:

```bash
cosign verify ghcr.io/stripe/smokescreen:latest \
  --certificate-identity-regexp="https://github.com/stripe/smokescreen" \
  --certificate-oidc-issuer="https://token.actions.githubusercontent.com"
```

## Building Locally

To build the container image outside of CI:

```bash
# Install ko
go install github.com/ko-build/ko@latest

# Build for multiple platforms
ko build . --platform=linux/amd64,linux/arm64 --local
```
