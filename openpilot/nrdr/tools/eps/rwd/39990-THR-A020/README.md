# Honda Odyssey 39990-THR-A020

These files have passed offline container, payload reconstruction, and checksum validation. Both RWD headers list `39990-THR-A020`, `39990-THR-A010`, and `39990-THR,A020` as source identity lookup entries. The A010 entry matches the supplied A010/A020 stock container; ECU acceptance and hardware compatibility have not been verified.

| File | Payload | Embedded identity |
| --- | --- | --- |
| `stock_39990-THR-A020.rwd` | Original stock application payload, with a three-ID container header | `39990-THR-A020` |
| `mod25xv1-39990-THR,A020.rwd` | Experimental R2 calibration with modified firmware identity | `39990-THR,A020` |

Despite the `mod25xv1` filename, the modified payload matches R2, including the mirrored `0x67xxx` table changes. It is not uniform 2.5x scaling across all tables or operating conditions. Physical torque has not been measured; 2.5x physical assist is not established.

Both files are 475,237 bytes, with application start `0xC000` and payload length `0x74000`. Each encryption-key header contains exactly one value. Container checksums and internal application checksums pass; the complete application 16-bit word sum is zero.

Offline integrity does not establish ECU flash acceptance, safe vehicle operation, or compatible openpilot controller gains. These files are provided for research and controlled bench evaluation. No automatic flashing or controller tuning is configured by this folder.

Verify file integrity with `shasum -a 256 -c SHA256SUMS` from this directory.
