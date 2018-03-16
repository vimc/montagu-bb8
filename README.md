# montagu-bb8
Performs local backup between our servers. This wraps bb8 with Montagu specific 
bits. Essentially this is just the bb8 repo with a config file at the top level.

# Setup
Steps taken to set up the annex
1. Clone this repo anywhere
```
git clone https://github.com/vimc/montagu-bb8 --recursive
```

2. Run `./bb8/setup_starport.sh` as root, passing in the directory location of the starport as an argument.
```
sudo ./bb8/setup_starport.sh /mnt/data/starport
```

That's it. Note that this will create a `bb8` user and a symlink to the actual starport at `/var/lib/bb8/starport`

Steps taken to set up support/prod:
1. Clone this repo into the `montagu` directory
```
git clone https://github.com/vimc/montagu-bb8 --recursive

```

2. To use, enter the `bb8` dir and follow instructions in the README there (https://github.com/vimc/bb8). When
prompted for a SOURCE_CONFIG_PATH, use the `config.json` file in this repo (so
`../config.json` from the `bb8` dir).

