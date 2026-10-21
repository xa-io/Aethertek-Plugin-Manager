# Aethertek Plugin Manager

Update your installed Dalamud plugins using ZIP download links from their publishers.

APM releases include a plugin manifest and icon for repository installation and version detection.

## Quick start

1. Open APM with `/apm`.
2. Copy the publisher's direct ZIP download link.
3. Check **I trust the publisher**. If the target is a supported public plugin, add it through **Add public plugins** and enable its host in Dalamud.
4. Click **Check clipboard for updates**. APM matches the ZIP filename to an eligible plugin in its list, validates the package, and chooses the destination. Select a plugin first only if APM asks you to distinguish multiple eligible copies with the same name.

Keep APM enabled until the update finishes. A running development plugin is unloaded and reloaded automatically; a disabled development plugin stays disabled. Private access updates require the intended supported host to be loaded.

The ZIP filename must match the plugin, for example `PluginName.zip` or `PluginName-v0.0.0.1.zip`. Version and revision labels in the filename are optional and do not determine the installed version. APM reads versions from the validated package. Only use packages from publishers you trust.

## One clipboard update button

- **Private access package:** A matching Access DLL and private JSON go into `pluginConfigs/<PluginName>/tasks/`. APM supports compatible hosts by their installed plugin identity and access IPC, without a fixed plugin-name list. Include the public plugin in APM and enable its compatible host first. Its public DLL and Dalamud manifest stay unchanged.
- **Development package:** A matching plugin DLL and regular Dalamud JSON go into the matched existing development directory. Optional debug symbols are supported; bundled C# helper sources are skipped. A ZIP containing only the matching plugin DLL is also supported; its installed JSON is preserved.

The JSON is inside the ZIP. Ordinary development plugins also use JSON, so APM checks its format and the DLL identity to choose the route. Invalid private packages are rejected before any files change. Historical signed Access-DLL-only packages still use their host's access folder.

New compatible plugins do not require an APM release just to add their names. Their public host must provide the access directory and package-validation services. Adding a plugin to the repository feed or APM list alone does not supply these services; APM explains which endpoints are missing if a host is incompatible.

**Check clipboard for updates** scans eligible APM registrations; hidden entries and disabled development plugins still qualify. A public host must be included and loaded to receive private access updates. Row selection is for details, removal, and resolving a duplicate-name match. **Reload plugin list** separately rereads Dalamud's registered plugins. There are no per-plugin update icons, selected-plugin update button, Advanced toggle, or Ctrl requirement. **Overwrite** remains available for an unchanged package. After an update, open the plugin to confirm its features initialized successfully.

## Options

- **Hide / Show hidden plugins:** Keep the list tidy and restore hidden entries.
- **Hide directories:** Hide folder paths in APM for screenshots.
- **Add public plugins:** Search installed public plugins and choose which APM can match for supported private access packages. Their public host DLLs remain managed by Dalamud.
- **Automatic Updates:** Allow dev and included public plugins to request a private access update through their **Check Updates** button. Off by default; publisher trust must also be enabled. Copy the matching publisher ZIP link first. APM opens to show progress and handles validation, unloading, replacement, and reloading. This option does not poll for updates in the background.
- **Create backups:** Keep backups in a `backups` folder beside the updated plugin's installed DLL. Enabled by default.
- **Overwrite:** Allow reinstalling an unchanged package. Private access packages update when either the private version or public-facing version increases. Other package types retain their version/revision policy.
- **Open on plugin load:** Open APM automatically when it loads.

Your selections and settings are remembered across reloads. With backups off, temporary recovery files are removed after a successful update or rollback; failed recovery or cleanup may leave files for recovery.

## Troubleshooting

Private access ZIPs contain the access DLL and matching JSON. APM checks the ZIP filename against eligible registered plugins before downloading, validates the package, and displays the installed private and public host versions. The JSON keeps the independently updated private version separate from its public-facing version. The installed public plugin manifest remains managed by Dalamud. If more than one eligible copy has the same plugin name, select the intended copy and check again.

**Already patched to this version** means the update identity is unchanged. Enable **Overwrite** to reinstall it.

**Access package rejected:** APM shows the installed public plugin version and stable/testing channel when available, the access package version, and its declared public version. If the public versions differ, use the publisher's matching public release in Dalamud (`/xlplugins`) or request an access package for your installed version. A package intended for a testing release may not work with the stable release. The private package revision can differ from the public version; the host decides compatibility. APM does not change files when the host rejects a package, and **Overwrite** cannot bypass that rejection.

If those versions already match, download a fresh package and check the host's own `/xllog` rejection with its publisher. Matching version labels alone do not guarantee compatibility. Hosts that return only a yes/no validation result cannot provide APM with an exact rejection reason.

**Mismatched DLL/JSON or older package:** APM reports the available version details and explains whether to download a complete matching ZIP or a newer build. Do not edit version numbers or mix files from different releases. Expected validation rejections have a readable warning in `/xllog`; technical details remain available at debug level. Recovery failures continue to report an error.

**Injection failed due to not being on Dalamud Release build** means the public host requires the release branch and refused the private update. Errors appear in red directly below **Check clipboard for updates**. Select the release branch in XIVLauncher, restart the game, and try again. Staging (`stg`) and API preview branches such as `api16` do not qualify; an unknown branch can also be refused. Overwrite does not bypass this requirement.

For a failed download, copy a fresh direct link; Discord attachment links can expire. For other failures, check APM's status message and search `/xllog` for `[APM]`.
