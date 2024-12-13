# Go Ops Tools

Compilation instructions for DevOps tools written in Go.

## `argocd`

```
make cli-local
mv -v dist/argocd ~/.local/bin
```

## `clusterctl`

## `istioctl`

macOS:

```
mkdir out
GOOS=darwin GOARCH=arm64 LDFLAGS='-extldflags -static -s -w' \
common/scripts/gobuild.sh \
out/istioctl \
./istioctl/cmd/istioctl
sudo cp -v out/istioctl /usr/local/bin
```

Linux:

```
GOOS=linux GOARCH=amd64 LDFLAGS='-extldflags -static -s -w' \
common/scripts/gobuild.sh \
$HOME/.local/bin/istioctl \
./istioctl/cmd/istioctl
```

## `k9s`

```
make build
mv -v execs/k9s ~/.local/bin
```

## `nuclio`


macOS:

```
GOOS=darwin GOARCH=arm64 go build \
-ldflags="-s -w -X github.com/v3io/version-go.gitCommit=$(git rev-parse HEAD) -X github.com/v3io/version-go.label=1.14.0 -X github.com/v3io/version-go.arch=arm64" \
-o nuctl \
cmd/nuctl/main.go
sudo cp -v nuctl /usr/local/bin
```

## `opentofu` on macOS

```
CGO_ENABLED=1 go build -ldflags "-w -s -X 'github.com/opentofu/opentofu/version.dev=no'" -o dist/ ./cmd/tofu
sudo cp -v dist/tofu /usr/local/bin
```

## `sops`

```
make vendor
go build -o ~/.local/bin/sops github.com/getsops/sops/v3/cmd/sops
```

## `vcluster`

```
# Build
export RELEASE_VERSION=v0.19.x
go generate -tags embed_charts ./...
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 GO111MODULE=on \
go build -mod vendor -tags embed_charts -ldflags "-X main.version=${RELEASE_VERSION}" -o out/vcluster cmd/vclusterctl/main.go

# Install
mv -v out/vcluster ~/.local/bin
```

## `yq`

```
go build \
-ldflags="-X main.GitCommit=$(git rev-parse HEAD) -X main.GitDescribe=$(git describe --tags --always) -w -s"
sudo cp -v yq /usr/local/bin
```
