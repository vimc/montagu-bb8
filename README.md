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

1. Clone this repo into the `/montagu` directory
```
git clone https://github.com/vimc/montagu-bb8 --recursive

```

2. To use, enter the `bb8` dir and run
```
sudo ./setup ../config.json teamcity vault registry

```
See https://github.com/vimc/bb8#setup-leaf-machine for more explanation.

3. To upgrade, pull the latest changes and repeat step 2. 

### Production
`bb8` is installed by the deploy task. 

To upgrade `bb8`:

1. Navigate to the `/montagu/deploy/montagu-bb8` directory and pull the latest version.

2.  Run
```
sudo ./setup ../config.json main_db_restore orderly

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
