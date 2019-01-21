# montagu-bb8
Performs local backup between our servers. This wraps bb8 with Montagu specific 
bits. Essentially this is just the bb8 repo with a config file at the top level.

## Setup
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

### Support
Steps taken to set up Support:

1. As the `montagu` user, clone this repository into the `montagu` user home directory

```
git clone https://github.com/vimc/montagu-bb8 --recursive

```

2. Set up the global `bb8` link with

```
sudo ./montagu-bb8/bb8/bb8_link_write
```

(this is the only step that requires root privileges)


2. To use, from `montagu-bb8` run

```
./bb8/setup config.json teamcity vault registry
```

See https://github.com/vimc/bb8#setup-leaf-machine for more explanation.  If prompted, please configure scheduling as directed.

3. To upgrade, pull the latest changes and repeat step 2. 

### Production

`bb8` is no longer installed by the deploy task.

To upgrade `bb8`:

1. As the `montagu` user on production, navigate to `~/montagu-bb8` and pull the latest version (you may need to run `git submodule update`)

2.  From `montagu-bb8` run
```
./bb8/setup config.json main_db_restore orderly

```

### Annex

On the annex, after successfully setting up `bb8` and `barman`, run

```
./scripts/schedule-barman-montagu-nightly
```

which will configure a nightly job that will create a restorable copy of the montagu database and put it via bb8 into the starport.

To upgrade `bb8`:

1. Navigate to `/home/montagu/montagu-bb8` and pull the latest changes.

2. Run 
```
sudo ./setup ../config.json barman_to_starport
```
