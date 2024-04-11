# Go Ops Tools

Compilation instructions for DevOps tools written in Go.

## `argocd`

```
make cli-local
mv -v dist/argocd ~/.local/bin
```

## `clusterctl`

## `k9s`

```
make build
mv -v execs/k9s ~/.local/bin
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
