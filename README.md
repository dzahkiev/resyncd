# resyncd

Synchronizes macOS local files and directorines with a remotes.
Inspired by [Lsyncd](https://github.com/axkibe/lsyncd/issues/587#issuecomment-598831069).

## Installation

```
$ go get github.com/idr0id/resyncd
$ resyncd example.toml
```

ИЛИ

склонируй себе репозиторий в GOPATH/src/github.com/idr0id
затем: go build -o resyncd main.go logger.go config.go rsync.go synchronizer.go utils.go watcher.go file_matcher.go
затем сделай так mv ./resyncd $(go env GOPATH)/bin/
и попробуй после этого просто сделать resyncd

nano -w ~/.zshrc
export GOPATH=$HOME/go
export GOROOT=/usr/local/go
export GOBIN=$GOPATH/bin
export PATH=$PATH:$GOPATH
export PATH=$PATH:$GOROOT/bin
export PATH=$PATH:$(go env GOPATH)/bin

```
$ resyncd example.toml
```

## Configuration

```
[[sync]]
source = "/Users/username/projects/example"
target = "root@example.com:/srv/http/example.com"
exclude = [
  "**/.idea",
  "**/.git",
  "some-file-in-any-folder",
  "/path/to/specified/file"
]
  [sync.rsync]
  rsh = "/usr/bin/ssh -i /Users/username/.ssh/id_rsa -o StrictHostKeyChecking=no"
  acls = true
  perms = true
  
[[sync]]
source = "/Users/username/projects/example2"
target = "root@example.com:/srv/http/example2.com"
exclude = [
  "**/.idea",
  "**/.git",
]
  [sync.rsync]
  rsh = "/usr/bin/ssh -i /Users/username/.ssh/id_rsa -o StrictHostKeyChecking=no"
  acls = true
  perms = true
```
