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


3. To use, from the `montagu-bb8` directory run

```
./bb8/setup config.json teamcity vault registry
```

See https://github.com/vimc/bb8#setup-leaf-machine for more explanation.  If prompted, please configure scheduling as directed.

3. To upgrade, pull the latest changes and repeat the `setup` step.

### Production

`bb8` is configured by the deploy task.  On initial setup, you will need to run, as the `montagu` user:

```
sudo ~/montagu/montagu-bb8/bb8/bb8_link_write
```

to install the link to the `bb8` script globally (you will be prompted if it is not configured correctly).

### Annex

On the annex, after successfully setting up `bb8` and `barman`, run

```
./montagu-bb8/scripts/schedule-barman-montagu-nightly
```

which will configure a nightly job that will create a restorable copy of the montagu database and put it via bb8 into the starport.

To upgrade `bb8`, as the `montagu` user:

1. Navigate to `~/montagu-bb8` and pull the latest changes.

2. From the `montagu-bb8` directory, configure `bb8` by running:

```
./bb8/setup config.json barman_to_starport
```
