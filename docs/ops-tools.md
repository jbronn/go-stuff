# Go Ops Tools

Compilation instructions for DevOps tools written in Go.

## `argocd`

```
make cli-local
sudo cp -v dist/argocd /usr/local/bin
```

## `clusterctl`

## `istioctl`

```
# need to set `GO{ARCH,OS}` on macOS
# GOOS=darwin GOARCH=arm64 \
IGNORE_DIRTY_TREE=1 VERSION=$(git describe --tags --always) LDFLAGS="-extldflags -static -s -w" \
common/scripts/gobuild.sh \
istioctl/istioctl \
./istioctl/cmd/istioctl
sudo cp -v istioctl/istioctl /usr/local/bin
```

## `k9s`

```
make build
sudo cp -v execs/k9s /usr/local/bin
```

## `nuclio`

```
go build \
-ldflags="-s -w -X github.com/v3io/version-go.gitCommit=$(git rev-parse HEAD) -X github.com/v3io/version-go.label=$(git describe --tags --always) -X github.com/v3io/version-go.arch=$(dpkg --print-architecture 2> /dev/null || uname -m)" \
-o nuctl \
cmd/nuctl/main.go
sudo cp -v nuctl /usr/local/bin
```

## `opentofu`

```
CGO_ENABLED=1 go build -ldflags "-w -s -X 'github.com/opentofu/opentofu/version.dev=no'" -o dist/ ./cmd/tofu
sudo cp -v dist/tofu /usr/local/bin
```

## `sops`

```
make vendor
go build -o sops github.com/getsops/sops/v3/cmd/sops
sudo cp -v sops /usr/local/bin
```

## `vcluster`

```
# Build
export RELEASE_VERSION=v0.19.x
go generate -tags embed_charts ./...
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 GO111MODULE=on \
go build -mod vendor -tags embed_charts -ldflags "-X main.version=${RELEASE_VERSION}" -o out/vcluster cmd/vclusterctl/main.go

# Install
sudo cp -v out/vcluster /usr/local/bin
```

## `yq`

```
go build \
-ldflags="-X main.GitCommit=$(git rev-parse HEAD) -X main.GitDescribe=$(git describe --tags --always) -w -s"
sudo cp -v yq /usr/local/bin
```
