# Subcult theme

Deep violet armor, lime energy, and a lilac focus line. The desktop reads like a Unit 01 cockpit instead of a generic neon terminal dump.

This fork is the **Subcult theme** base. Use `tools/apply-palette.py` to create palette-only variants such as `subcult-theme-catppuccin`, `subcult-theme-dracula`, or `subcult-theme-eldritch`. The tool copies this theme's styling unchanged and replaces only `colors.toml`; the stock Omarchy 4 generator then uses the adapted palette for generated integrations.

```bash
python3 tools/apply-palette.py /path/to/catppuccin /path/to/subcult-theme-catppuccin --name subcult-theme-catppuccin
```

The source may be an Omarchy theme directory or its `colors.toml`. The tool always copies this repository as the base, even when the source Omarchy theme has fewer files. Use `--base /path/to/another-subcult-theme` to adapt a different Subcult base. The source must provide the standard Omarchy ANSI keys plus `accent`, foreground/background, cursor, and selection colors. Existing output directories are never overwritten.

The custom GIMP, Typora, and qBittorrent files in this base are deliberately unchanged by the palette tool. Install those separately only when you want the Unit 01 app treatment; stock/generated integrations are the part that follows the variant palette.

## Preview

![Theme preview](preview.png)

## Install

Use the Omarchy theme installer:

```bash
omarchy-theme-install https://github.com/PatrickFanella/omarchy-01-theme
```

## Compatibility

- Omarchy 4 with the Quickshell-based Quattro desktop.
- The theme root stays compatible with the stock Omarchy 4 layout: `colors.toml`, `shell.toml`, and the standard app overrides.
- `shell.toml` controls native Quattro shell surfaces, while `colors.toml` supplies the palette for integrations that Omarchy generates.
- Reactive tmux and Starship files are opt-in additions installed by `install-app-themes`. They do not replace stock files in the theme root.
- Other generated integrations stay out of this repository so newer Omarchy templates can add support.
- `colors.toml` supplies Hyprland border colors through Omarchy's generated configuration.

## Included themes

- Quattro shell and Hyprland window colors
- Included terminal, GTK, browser, Discord, btop, icon, and Neovim configs
- GIMP 3.2, Typora, and qBittorrent themes for the installed desktop apps
- Full tmux config with plugins and bindings
- Unit 01 tmux status and Starship templates that follow the active Omarchy palette

## Install app themes

Install the three app themes, full tmux config, and opt-in Omarchy shell integrations:

From this checkout:

```bash
./install-app-themes
```

After `omarchy-theme-install`, run:

```bash
~/.config/omarchy/themes/01/install-app-themes
```

The installer always writes under the installing user's `$HOME/.config`; it does not use `XDG_CONFIG_HOME`. It manages these files:

- `$HOME/.config/GIMP/3.2/gimp.css`
- `$HOME/.config/Typora/themes/unit-01.css`
- `$HOME/.config/qBittorrent/themes/unit-01.qbtheme`
- `$HOME/.config/tmux/tmux.conf`
- `$HOME/.config/tmux/tmux.local.conf`
- `$HOME/.config/omarchy/themed/omarchy-01-tmux.tmux.conf.tpl`
- `$HOME/.config/omarchy/themed/omarchy-01-starship.toml.tpl`
- `$HOME/.config/omarchy/hooks/theme-set.d/90-omarchy-01-shell-integrations`
- `$HOME/.config/omarchy/integrations/omarchy-01-theme/installed-v1`

On first install, the script also seeds `$HOME/.config/tmux/themes/omarchy.tmux.conf` and `$HOME/.config/starship.toml` with static Unit 01 fallbacks. Switch to or reapply the theme once after installation to activate reactive generation. On each normal `omarchy-theme-set`, Omarchy's stock template generator renders the namespaced files in `$HOME/.local/state/omarchy/current/theme`. The hook atomically installs the rendered tmux status and Starship files. It reloads only the tmux theme fragment, never the full `tmux.conf`, then refreshes connected clients. Headless theme changes skip hooks, so the shell files update on the next normal theme set.

Installer reruns never sync the generated tmux theme or Starship output. After the sentinel exists, normal `omarchy-theme-set` runs own those files. This avoids conflicts with another active theme and does not reset old generated output. The tmux base config, app assets, templates, and hook remain managed. The project paths in `tmux.local.conf`, such as `Projects/active`, are under the installing user's `$HOME`.

Before writing anything, the installer checks every managed destination and looks for the predecessor hooks `sync-tmux` and `sync-starship`. Those hooks sort after this theme's `90-omarchy-01-shell-integrations` hook, overwrite its reactive output, and reload the full tmux config. The installer refuses all changes when it finds either hook unless you pass `--force`. With `--force`, it atomically moves each hook to a unique backup under `$HOME/.config/omarchy/integrations/omarchy-01-theme/hook-backups/`, outside the executable hook directory. A failed install restores the hooks. A successful install keeps the disabled backups and prints their paths. Replaced versions of the managed hook are backed up there too. Forced replacement also preserves every other different managed file or symlink in a uniquely named timestamped sidecar backup. The installer leaves legacy templates alone because they cannot update generated output after their hooks are disabled.

The installer does not edit app preferences. Restart GIMP, select **Unit 01** in Typora, and choose `unit-01.qbtheme` in qBittorrent preferences.

To remove the reactive integration, delete:

- `$HOME/.config/omarchy/themed/omarchy-01-tmux.tmux.conf.tpl`
- `$HOME/.config/omarchy/themed/omarchy-01-starship.toml.tpl`
- `$HOME/.config/omarchy/hooks/theme-set.d/90-omarchy-01-shell-integrations`
- `$HOME/.config/omarchy/integrations/omarchy-01-theme/installed-v1`

Remove `$HOME/.config/tmux/themes/omarchy.tmux.conf` and `$HOME/.config/starship.toml` separately only if no other theme owns them.

The tmux config requires tmux 3.5 or newer and [TPM](https://github.com/tmux-plugins/tpm). Its plugins and bindings use these runtime commands: `wl-copy` from `wl-clipboard`, `lsd`, `zoxide`, `fzf`, `bat`, the Bitwarden CLI (`bw`), and `jq`.

The repository includes `unit-01.qbtheme`. To rebuild it from source, run `./qbittorrent/build.sh`. Rebuilding requires Qt 6 `rcc` at `/usr/lib/qt6/rcc` or `rcc-qt6`; the build script refuses Qt 5.

## Wallpapers

<table>
  <tr>
    <td><img src="backgrounds/0-glitch-trio.jpg" width="220" alt="Glitch trio"></td>
    <td><img src="backgrounds/1-dusk-eva.jpg" width="220" alt="Dusk EVA"></td>
    <td><img src="backgrounds/2-blade-rooftop.jpg" width="220" alt="Blade rooftop"></td>
  </tr>
  <tr>
    <td><img src="backgrounds/3-rei-glitch.jpg" width="220" alt="Rei glitch"></td>
    <td><img src="backgrounds/4-eva-skull-cyan.jpg" width="220" alt="EVA skull cyan"></td>
    <td><img src="backgrounds/5-eva-ramiel-minimal.jpg" width="220" alt="Ramiel minimal"></td>
  </tr>
  <tr>
    <td><img src="backgrounds/6-eva-orb-minimal.jpg" width="220" alt="EVA orb minimal"></td>
    <td><img src="backgrounds/7-eva-mask-minimal.jpg" width="220" alt="EVA mask minimal"></td>
    <td><img src="backgrounds/8-eva-angel-minimal.jpg" width="220" alt="EVA angel minimal"></td>
  </tr>
  <tr>
    <td><img src="backgrounds/9-eva-core-minimal.jpg" width="220" alt="EVA core minimal"></td>
    <td><img src="backgrounds/10-eva-bloom-minimal.jpg" width="220" alt="EVA bloom minimal"></td>
    <td><img src="backgrounds/11-neon-unit01.jpg" width="220" alt="Neon Unit 01"></td>
  </tr>
  <tr>
    <td><img src="backgrounds/12-unit01-minimal.jpg" width="220" alt="Unit 01 minimal"></td>
    <td><img src="backgrounds/13-spear-charge.jpg" width="220" alt="Spear charge"></td>
    <td><img src="backgrounds/14-rei-pod.jpg" width="220" alt="Rei pod"></td>
  </tr>
  <tr>
    <td><img src="backgrounds/15-eva-skull-violet.jpg" width="220" alt="EVA skull violet"></td>
    <td><img src="backgrounds/16-running-unit01.jpg" width="220" alt="Running Unit 01"></td>
    <td><img src="backgrounds/17-berserk-closeup.jpg" width="220" alt="Berserk closeup"></td>
  </tr>
  <tr>
    <td><img src="backgrounds/18-apocalypse-halo.jpg" width="220" alt="Apocalypse halo"></td>
  </tr>
</table>

Optional animated backgrounds for third-party wallpaper tools: `19-pixel-unit01.mp4`, `20-hacking-system.mp4`, `21-fatal-error-screen.mp4`, and `shatter-mosaic-9285.mp4`. Stock Omarchy stills-only wallpaper pickers will ignore them. `20-hacking-system.mp4` is about 18MB.

## Requirements

- `Yaru-purple` icon theme
- Bash 5 for the app theme scripts
- tmux 3.5 or newer, TPM, `wl-clipboard`, `lsd`, `zoxide`, `fzf`, `bat`, `bw`, and `jq` for the tmux config
- Qt 6 `rcc` only when rebuilding `unit-01.qbtheme`

## Attribution

- Palette based on the evangelion.nvim colorscheme by xero.style
