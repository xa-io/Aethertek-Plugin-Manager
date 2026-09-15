# Aethertek Plugin Manager

Update your installed Dalamud plugins using ZIP download links from their publishers.

APM releases include a plugin manifest and icon for repository installation and version detection.

## Quick start

1. Open APM with `/apm`.
2. Copy the publisher's direct ZIP download link.
3. Check **I trust the publisher** and select the matching plugin.
4. For a development plugin update, click the first refresh button or **Update selected plugin from clipboard**.

Keep APM enabled until the update finishes. A running plugin is unloaded and reloaded automatically; a disabled plugin stays disabled.

The ZIP filename must match the plugin, for example `PluginName.zip` or `PluginName-v0.0.0.1.zip`. Versions without the `v` prefix are also supported. Only use packages from publishers you trust.

## Refresh buttons

- **First refresh button:** Updates a development plugin's installed files from the ZIP link in your clipboard.
- **Second refresh button (Advanced):** Enable **Advanced options**, then hold **Ctrl** and click the second refresh button to inject the publisher's configuration/module package. Files go into the plugin's configuration directory, including `pluginConfigs/<PluginName>/tasks/` for plugins that use that layout. Check **Configuration destination** for the resolved target; turn off **Hide directories** if needed.

## Options

- **Hide / Show hidden plugins:** Keep the list tidy and restore hidden entries.
- **Hide directories:** Hide folder paths in APM for screenshots.
- **Add public plugins:** Search installed public plugins and choose which appear in the list. Their normal updates remain managed by Dalamud.
- **Advanced options:** Shows the second refresh button for Ctrl+click configuration/module injection.
- **Create backups:** Keep backups in a `backups` folder beside the updated plugin's installed DLL. Enabled by default.
- **Overwrite:** Allow reinstalling the current version. Older versions are always blocked.
- **Open on plugin load:** Open APM automatically when it loads.

Your selections and settings are remembered across reloads. With backups off, temporary recovery files are removed after a successful update or rollback; failed recovery or cleanup may leave files for recovery.

## Troubleshooting

**Already patched to this version** means no update is needed. Enable **Overwrite** if you want to reinstall that version.

For a failed download, copy a fresh direct link; Discord attachment links can expire. For other failures, check APM's status message and search `/xllog` for `[APM]`.
