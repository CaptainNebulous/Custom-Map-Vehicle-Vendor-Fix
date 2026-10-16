# Custom Map Vehicle Vendor Fix

**Automatically repairs broken vehicle vendor, vehicle spawner, and helicopter repair-pad connections on custom Rust maps.**

Custom Map Vehicle Vendor Fix is a lightweight Oxide/uMod plugin that restores missing references between vehicle vendors and their associated vehicle spawners on custom Rust maps.

Custom maps, prefab changes, or Rust updates can sometimes leave vehicle vendors disconnected from the entities responsible for spawning vehicles. This plugin searches for nearby spawners and reconnects them automatically.

It also supports helicopter spawners and their repairable helipads, helping restore functionality to custom Airwolf locations.

## Features

- **Automatic Vendor Linking** — Finds vehicle vendors without valid spawner references and reconnects them.
- **Helicopter Repair-Pad Support** — Links helicopter spawners to nearby repairable Airwolf helipads.
- **Preserves Existing Connections** — Avoids replacing valid vehicle spawner references.
- **Nearest-Spawner Detection** — Selects the closest eligible spawner within a 25-meter radius.
- **Automatic Initialization** — Runs after the server finishes initializing.
- **Efficient Entity Scanning** — Collects vehicle vendors and spawners in a single pass through server entities.
- **Diagnostic Logging** — Reports successful connections and missing nearby entities.
- **No Player Commands** — Operates automatically without requiring player interaction.

## How It Works

When the Rust server finishes initializing, the plugin scans existing server entities and identifies vehicle vendors, vehicle spawners, and relevant helicopter repair pads.

### Vehicle Vendor Repair

For each vehicle vendor:

1. Checks whether an existing vehicle spawner reference is valid.
2. Searches within 25 meters if the reference is missing or invalid.
3. Selects the closest eligible vehicle spawner.
4. Assigns the reference to the vendor.
5. Refreshes the vendor's network cache.
6. Logs the result.

Valid existing connections are preserved.

### Helicopter Repair-Pad Linking

For helicopter spawners, including Airwolf spawners:

1. Checks the existing repairable-helipad reference.
2. Searches within 25 meters if the reference is invalid.
3. Identifies the nearest eligible Airwolf repair pad.
4. Updates the spawner's repair-pad reference when necessary.
5. Logs the repair pad's current state and usability.

The plugin respects Rust's existing helicopter repair-pad settings rather than changing the server's repair requirements.

## Installation

1. Download `CustomMapVehicleVendorFix.cs`.
2. Upload it to your server's `oxide/plugins` directory.
3. Allow Oxide/uMod to compile and load the plugin.
4. Restart the server or reload the plugin after the relevant map entities are initialized.
5. Review the server console for connection results.

No additional configuration is required.

## Configuration

This plugin does not generate a configuration file.

The following search distances are defined in the source code:

| Setting | Value |
|---|---|
| Vehicle Vendor Search Radius | 25 meters |
| Helicopter Repair-Pad Search Radius | 25 meters |

## Commands and Permissions

**Commands:** None

**Permissions:** None

All functionality runs automatically on the server.

## Console Logging

The plugin provides diagnostic messages for:

- Successfully linked vehicle vendors
- Missing nearby vehicle spawners
- Missing Airwolf repair pads
- Helicopter repair-pad connection status
- Repair-pad linking errors
- Total entities checked and repaired

These messages help administrators identify misplaced or incorrectly connected custom-map prefabs.

## Compatibility and Dependencies

| Requirement | Details |
|---|---|
| **Game** | Rust (PC) |
| **Framework** | Oxide/uMod |
| **Additional Plugin Dependencies** | None |
| **Configuration File** | Not required |
| **External Database** | Not required |
| **Player Interface** | None |

The plugin uses native Rust entity references and is intended for custom maps containing vehicle vendors, vehicle spawners, or repairable helicopter pads.

Compatibility with individual Rust updates depends on the availability of the referenced game classes and fields.

## Important Notes

- Designed to repair missing entity references, not incorrectly placed prefabs.
- Vehicle spawners must be within the configured search radius.
- Repairable Airwolf helipads must use the expected prefab.
- Existing valid vendor-to-spawner references are not replaced.
- The plugin does not create missing vehicle spawners or repairable helipads.
- Connections are checked when the server finishes initializing.

For a permanent custom-map solution, correcting the original prefab references in the map editor is recommended.

## Credits

**Original author:** Pinkstink

**Version:** 1.1.4

**Additional credit:** Pe7erS, credited in the plugin's source description for updates.

---

**Custom Map Vehicle Vendor Fix** provides a straightforward way to restore broken vehicle vendor connections on custom Rust maps without unnecessary configuration or administrative commands.
