# Changelog

## 1.4.0 - 2026-08-06

### Added
- Avery 5163 US Letter layout: 4 x 2 in, 10 labels per sheet (2 x 5).
- Avery Presta 94220 US Letter layout: 2 x 1 in, 24 labels per sheet (3 x 8).
- Avery 22806 US Letter layout: 2 x 2 in, 12 labels per sheet (3 x 4).

### Fixed
- Confirmed multi-label printing with the current InvenTree / WeasyPrint environment.
- Corrected 4 x 2 in label orientation for Avery 5163 by using 101.6 mm width x 50.8 mm height.

### Maintenance
- Removed all temporary HTML / per-cell debug file generation.
- Restored the production printing path to the known-working implementation.
- Bumped the plugin version from 1.3.1 to 1.4.0.

### Validation
- Avery 5163 was validated with multiple selected parts on a single US Letter sheet.
- Avery 94220 and Avery 22806 definitions are included but should receive a physical alignment test before consuming a full sheet.
