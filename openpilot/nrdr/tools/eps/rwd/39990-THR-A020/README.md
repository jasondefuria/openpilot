# Honda Odyssey 39990-THR-A020

| File | Payload | Embedded identity |
| --- | --- | --- |
| `stock_39990-THR-A020.rwd` | Stock application; three-ID container header | `39990-THR-A020` |
| `mod25xv2-39990-THR,A020.rwd` | Historical R2 calibration; known incorrect runtime CRC at `0x6FF7C` | `39990-THR,A020` |
| `mod25xv3-39990-THR,A020.rwd` | Same calibration as v2, with runtime CRC and dependent checksums corrected | `39990-THR,A020` |

| `mod25xv4-39990-THR,A020.rwd` | V3 torque calibration with banks 1–3 minimum-engagement fields zeroed and checksums updated | `39990-THR,A020` |

**V2 has a known runtime CRC mismatch.** Earlier verification covered the container and application sums but missed this block CRC. It is retained for comparison, not as the corrected image.

V3 changes only eight decoded checksum bytes relative to v2: the CRC at `0x6FF7C`, application checksum A at `0x7FF80`, and C at `0x7FFFE`. The RWD container checksum is also updated. No executable code, torque calibration, identity, header, or minimum-speed values changed.

| Offline check | Stock | V3 |
| --- | --- | --- |
| CRC-32/BZIP2 of `0x40000–0x4FF5F`, stored at `0x4FF7C` | `134AE5B1` | `134AE5B1` |
| CRC-32/BZIP2 of `0x60000–0x6FF5F`, stored at `0x6FF7C` | `9A305122` | `6956DAFD` |
| Application checksum A | `D0CA` | `C15D` |
| Application checksum C | `A6E0` | `C5BA` |
| Complete application BE16 word sum | `0000` | `0000` |
| RWD container checksum | `045553B8` | `0455557E` |

All listed stock/V3 values reproduce. Both application markers (`4837` and `B7C8`) and the cipher roundtrip also check correctly.

All four files are 475,237 bytes, with application start `0xC000` and payload length `0x74000`. Headers list `39990-THR-A020`, `39990-THR-A010`, and `39990-THR,A020` as source identity lookup entries; inclusion does not establish ECU hardware compatibility. Each encryption-key header contains exactly one value.

V3 retains R2's banks 1–3 main/reference torque changes. Banks 4–7 remain stock. Minimum-speed calibration remains 10 counts in banks 1–3 and 70 in banks 4–7. The filename does not establish uniform 2.5x scaling or measured physical torque. F181 cannot distinguish v2 from v3 because their embedded identities match.

Offline integrity does not establish ECU acceptance or physical steering safety. No automatic flashing or controller tuning is configured by this folder.

Verify file hashes with `shasum -a 256 -c SHA256SUMS` from this directory.

## V4 offline verification

V4 differs from V3 in six calibration bytes: minimum-engagement words at `0x57B00`, `0x57E00`, `0x58100`, `0x67B00`, `0x67E00`, and `0x68100` change from 10 to 0. Eight internal checksum bytes and the container checksum are updated. All other payload bytes, including torque curves, executable code, and firmware identities, are unchanged. Banks 4–7 retain their existing values.

| Check | V4 verified value |
| --- | --- |
| Runtime CRC at `0x4FF7C` | `134AE5B1` |
| Runtime CRC at `0x6FF7C` | `DA5B0744` |
| Application checksum A | `5E6D` |
| Application checksum C | `8B9A` |
| Complete application BE16 word sum | `0000` |
| RWD container checksum | `045554EA` |

These are static file-integrity checks. Zero-speed steering behavior and ECU acceptance have not been validated. V4 reports the same `39990-THR,A020` identity as V2/V3, so F181 cannot identify which version is installed.
