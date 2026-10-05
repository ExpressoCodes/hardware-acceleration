# hardware-acceleration

A small NixOS configuration snippet that enables hardware-accelerated video
decoding/encoding on Intel graphics via VA-API and VDPAU.

## What it does

Importing `hardware-acceleration.nix` into your NixOS configuration:

- enables `hardware.opengl`,
- installs the Intel media drivers and VA-API/VDPAU packages:
  - `intel-media-driver` (`LIBVA_DRIVER_NAME=iHD`, newer GPUs),
  - `vaapiIntel` (`LIBVA_DRIVER_NAME=i965`, older but works better for
    Firefox/Chromium in some cases),
  - `vaapiVdpau` and `libvdpau-va-gl` for the VDPAU↔VA-API bridge,
- builds `vaapiIntel` with hybrid codec support enabled.

## Usage

Copy `hardware-acceleration.nix` next to your `configuration.nix` and import it:

```nix
{
  imports = [
    ./hardware-acceleration.nix
  ];
}
```

Then rebuild:

```sh
sudo nixos-rebuild switch
```

After rebuilding you can confirm acceleration is available with `vainfo`.

## License

Released under the [MIT License](LICENSE).
