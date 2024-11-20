# Instructions

## 1. Get the devenv (by installing with nix)

``` bash
nix shell nixpkgs#devenv
```

## Create the devenv
```bash
devenv init
```

## Add some service
```nix
#devenv.nix
 services.postgres = {
    enable = true;
    package = pkgs.postgresql_15;
    initialDatabases = [{ name = "mydb"; }];
    extensions = extensions: [
      extensions.postgis
      extensions.timescaledb
    ];
    settings.shared_preload_libraries = "timescaledb";
    initialScript = "CREATE EXTENSION IF NOT EXISTS timescaledb;";
  };

```

## Run the service
```bash
devenv up
```

## Try service
```bash
devenv shell
psql -d mydb
```
