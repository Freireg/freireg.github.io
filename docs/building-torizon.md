# Building Torizon OS

## Torizon (on Toradex hardware)

To build Torizon OS on Toradex modules, follow the knowledge-base article:

<https://developer.toradex.com/knowledge-base/build-torizoncore>

## Common Torizon (on third-party BSPs)

Start with the [machine-specific guide](index.md#building) for your board. If
your machine is not listed, or you prefer a manual setup, you can follow these
generic steps:

1. **Download the layers** for the `scarthgap` branch. Torizon OS is split into
   two layers — the distro (`meta-torizon`) and the BSP adaptations
   (`meta-torizon-bsp`) — plus their dependencies:

    ```bash
    $ git clone https://github.com/torizon/meta-torizon.git -b scarthgap-7.x.y
    $ git clone https://github.com/torizon/meta-torizon-bsp.git -b master
    $ git clone https://github.com/uptane/meta-updater.git -b scarthgap
    $ git clone https://git.yoctoproject.org/git/meta-virtualization -b scarthgap
    ```

2. **Set up the environment**: source the `setup-environment` script shipped in
   `meta-torizon-bsp/scripts` (the BSP layer owns the build tooling and machine
   selection).
3. **Configure your build**:

    - Add **both** `meta-torizon` and `meta-torizon-bsp` (and their
      dependencies) to your `conf/bblayers.conf` file.
    - Edit `conf/local.conf` to set the `MACHINE` you wish to build.
    - In the same file, set the distribution to `DISTRO='common-torizon'`.

4. **Build an image**: start building one of the available Torizon images:

    - `torizon-docker`
    - `torizon-minimal`
    - `torizon-podman` (**experimental**)
