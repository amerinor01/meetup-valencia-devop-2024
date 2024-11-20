# Instructions

## 1. Get the devshell template and run it.

``` bash
nix flake new -t "github:numtide/devshell" .

# enter the shell
nix develop # or `direnv allow` if you want to use direnv

```

## Include more dependencies
```toml
[[env]]
name = "super_secrete_stuff"
value = "foo"

[devshell]
packages = [
  "nodejs_18",
  "python311",
  "go"
]

```


