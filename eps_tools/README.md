# EPS tools moved

The EPS implementation, firmware images, parser, and documentation now live at
[`openpilot/nrdr/tools/eps`](../openpilot/nrdr/tools/eps/README.md).

These compatibility launchers keep existing `eps_tools/...` commands working.
New instructions use the shorter commands from the repository root, such as
`python3 flash.py`.

The local `mod25xv3-39990-THR,A020.rwd` copy matches the [documented CRC-corrected image](../openpilot/nrdr/tools/eps/rwd/39990-THR-A020/README.md). V2 has a known runtime CRC mismatch; see that comparison before using either file.

V3 SHA-256: `1b1da8bd79114c87f77f98bb69d1574777df0fe709d40fea7863fd9c52ac6ac9`.
