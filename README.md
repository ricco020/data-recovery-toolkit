# data-recovery-toolkit

> Cross-platform CLI utilities for hands-on data recovery work  -  disk imaging, SMART monitoring, file-carving wrappers, RAID triage.

Companion reference site: **[Save My Disk](https://www.save-my-disk.com/)**.

## Tools included

| Tool | Purpose |
|------|---------|
| `bin/smart-monitor.sh` | Daily S.M.A.R.T health monitor with configurable thresholds + email alerts. |
| `bin/ddrescue-safe.sh` | Two-pass GNU ddrescue wrapper with logbook resume  -  safer disk imaging from failing drives. |
| `bin/raid-triage.py` | Walks a candidate failing array, reports component metadata (mdadm/lvm/zpool/btrfs), suggests reassembly path. |
| `bin/photorec-wrap.sh` | Pre-configured PhotoRec wrapper with file-type whitelist + structured output. |

## Quickstart

```bash
git clone https://github.com/ricco020/data-recovery-toolkit
cd data-recovery-toolkit
sudo ./bin/smart-monitor.sh                 # daily health check
sudo ./bin/ddrescue-safe.sh /dev/sdb img.bin # rescue failing drive
sudo ./bin/raid-triage.py                    # identify array members
```

## Dependencies

```
apt install smartmontools gddrescue mdadm lvm2 zfsutils-linux testdisk
# or
brew install smartmontools ddrescue testdisk
```

Python 3.8+. No third-party libraries (pure stdlib).

## Methodology

Each tool implements a documented recovery workflow. Pre-execution checks reject obvious mistakes (writing to source device, overwriting non-blank images, missing block-device permissions).

The full workflow context, when each tool applies, and the underlying data-recovery methodology is documented at the companion site:
- [Recovery methodology (EN)](https://www.save-my-disk.com/en/methodology)
- [Méthodologie de récupération (FR)](https://www.save-my-disk.com/fr/methodologie)
- [Benchmark study (160 sessions, DOI)](https://doi.org/10.5281/zenodo.20507434)

## Editorial references

- [Best data recovery software 2026](https://www.save-my-disk.com/en/best-data-recovery-software-2026)
- [Recover deleted files Windows 10/11](https://www.save-my-disk.com/en/recover-deleted-files-windows-10-11)
- [Recover files after ransomware](https://www.save-my-disk.com/en/recover-files-after-ransomware)
- [Data recovery software benchmark (FR)](https://www.save-my-disk.com/fr/benchmark-logiciels-recuperation-donnees-2026)

## Safety notes

These tools touch block devices and can destroy data when misused. They include guard rails (refusing to write to mounted filesystems, refusing to overwrite non-image files, requiring explicit confirmation), but you remain responsible for what you run on production data.

Always image first, work from the image  -  never recover directly on the failing source.

## License

MIT  -  see [LICENSE](LICENSE).

## Contributing

Issues and PRs welcome. Tools added must:
- Include `--help` output
- Refuse destructive operations without explicit `--yes` or interactive confirmation
- Document any side effects
