# Windows 98 Desktop and Retro Games Roadmap

Status: planned; implementation has not started.
Created: October 28, 2026.

## Objective

Evolve the existing Roundtable 98 Electron desktop into a more faithful Windows 98 style experience and add playable, locally imported retro games. Preserve working AI connections, existing conversations, notes, and GitHub Releases updates.

## Starting point

Version 0.3.0 already provides Debate Room, AI Chat, Notepad, Debate Archive, Connections, Software Updates, movable and resizable windows, a shared taskbar, local persistence, and GitHub Releases update checks. This roadmap extends those foundations.

## Stage 1 — Windows 98 desktop foundation

- [ ] Make the desktop the opening screen, with Debate Room available as an app.
- [ ] Establish consistent classic teal wallpaper, gray controls, navy active title bars, gray inactive title bars, beveled borders, dotted focus outlines, and appropriate system typography.
- [ ] Replace Unicode shortcut symbols with an original, consistent set of pixel-style icons.
- [ ] Add My Computer, My Documents, Control Panel, and Games as desktop destinations.
- [ ] Make My Computer and My Documents browse the app's virtual folders and saved documents first; unrestricted access to the host filesystem is outside the initial scope.
- [ ] Add double-click shortcuts, keyboard activation, desktop context menus, and window system menus.
- [ ] Improve resize handles and persist window positions, sizes, and maximized state; constrain restored windows to the current display.
- [ ] Add wallpaper, interface scaling, optional sound, and reduced-motion settings.
- [ ] Use original or appropriately licensed assets; do not redistribute Microsoft graphics, fonts, or sounds without permission.
- [ ] Keep keyboard focus, readable scaling, and host operating-system shortcuts usable.

Acceptance: desktop, menus, dialogs, and all existing apps use the same visual and interaction rules. Existing AI chat, debate, archive, and update behavior still works.

## Stage 2 — NES and Game Boy playback prototype

- [ ] Add Games to the desktop, Start menu, and taskbar.
- [ ] Provide Import ROM, a local game library, system selection or detection, and double-click-to-play.
- [ ] Evaluate EmulatorJS with pinned versions of the player and selected emulator cores.
- [ ] Package selected runtime files locally so playing an imported game does not depend on a remote CDN.
- [ ] Resolve distribution requirements before bundling: EmulatorJS is GPL-3.0-or-later, and individual cores have their own licenses. Choose a compliant distribution approach; the current releases-only repository arrangement may need to change.
- [ ] Run the emulator in an isolated game renderer without the desktop's privileged Electron bridge, provider credentials, or access to unrelated files.
- [ ] Scope any WebAssembly, worker, content-security-policy, and controller permissions to the game renderer rather than weakening the desktop's policy.
- [ ] Validate imported files, constrain file sizes, and keep arbitrary filesystem paths out of renderer requests.
- [ ] Support one running game initially, with keyboard controls, sound, pause, and fullscreen.
- [ ] Handle unsupported and damaged ROMs without freezing the desktop.
- [ ] Test with homebrew or other games for which use and redistribution are permitted. User ROMs remain local.

Acceptance: import and play permitted NES and Game Boy test games offline without disrupting the desktop or AI applications.

## Stage 3 — Game library, controllers, and durable saves

- [ ] Expand the supported set to SNES, Game Boy Advance, and Sega Genesis after the prototype passes.
- [ ] Add search, favorites, and recently played games.
- [ ] Add controller detection, configurable mappings, and clear controller-disconnection feedback.
- [ ] Store each game's identity using a file hash so renaming a ROM does not lose its saves.
- [ ] Store ROMs, library metadata, normal game saves, and save states outside the application installation folder.
- [ ] Persist game data to stable disk-backed storage, independently of the desktop backend's changing local port.
- [ ] Add save-state slots and save import/export.
- [ ] Flush saves before closing a game; use atomic writes and retain backups.
- [ ] Track the emulator/core version associated with save states and explain compatibility limits when a core changes.
- [ ] Pause minimized games by default, with an option to change that behavior.
- [ ] Release held keys when focus changes and prevent game shortcuts from typing into AI chat or Notepad.
- [ ] Ensure ROMs and saves are excluded from source control, release uploads, logs, and AI request context.

Acceptance: save, close the entire application, reopen it, and resume successfully using both keyboard and controller. Renaming a ROM preserves its association with existing saves.

## Stage 4 — Explorer-style polish and release

- [ ] Style the Games library like a classic Explorer folder, with list/icon views, status information, and game properties.
- [ ] Give game windows consistent menus, resizing, taskbar behavior, and fullscreen restoration.
- [ ] Test display scaling, keyboard focus, controller loss, audio behavior, and fullscreen transitions.
- [ ] Test gameplay alongside AI conversations for responsiveness and resource use.
- [ ] Verify updates preserve conversations, notes, account connection settings, imported ROMs, and saves.
- [ ] Include required emulator/core license notices and any required source distribution.
- [ ] Publish a new version through the established GitHub Releases update channel, after the licensing and acceptance checks pass.
- [ ] Check update discovery and the upgrade path from the previous installed version.

Acceptance: an installed release can be upgraded and reopened with all user data intact. Gameplay and existing AI applications remain functional.

## Implementation areas

- Desktop look and navigation: public/index.html, public/desktop.css, public/desktop.js, and public/window-manager.js.
- Native application and controlled file import: desktop/main.cjs and desktop/preload.cjs.
- New game library, player, and save modules, separated from AI conversation code.
- Game data belongs in dedicated disk-backed storage; extend desktop/storage.cjs only for small app-owned settings where appropriate.
- Server asset handling and narrowly scoped emulator runtime policy: server.mjs.
- Packaging, license notices, and release validation: package.json, build/, scripts/, and test/.

These are proposed implementation areas, not changes already made.

## First milestone

Deliver the Windows 98 desktop foundation plus a small NES/Game Boy Games prototype. Validate reliable local playback before adding more systems.

## Deferred work

Multiplayer/netplay, achievements, online game discovery, automatic cover-art services, multiple concurrent games, and more demanding console systems are later enhancements.

## Reference documentation

- [EmulatorJS setup](https://emulatorjs.org/docs/getting-started/)
- [EmulatorJS documented options](https://emulatorjs.org/docs/options/)
- [EmulatorJS license](https://github.com/EmulatorJS/EmulatorJS/blob/main/LICENSE)

This roadmap records intended work. It does not mark the emulator, Games app, or Windows 98 refinements as implemented.
